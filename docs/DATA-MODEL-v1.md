# Finish Mode — Data Model v1 (Source of Truth)

Este documento define as entidades, campos e **índices** do v1.

**Regra:** indexar apenas o que será usado em consultas (where/orderBy).  
**Dexie schema:** `++` autoinc, `&` unique, `*` multiEntry, `[A+B]` compound.  
Ref: [Dexie Version.stores](https://dexie.org/docs/Version/Version.stores()) / [Compound Index](https://dexie.org/docs/Compound-Index).

---

## Convenções

- **IDs:** string (ex.: `crypto.randomUUID()`).
- **Datas:** number (epoch ms) para simplicidade no v1.
- **ChecklistItem:** `{ text: string; done: boolean }`.

---

## Entidades

### Mission

**Descrição:** contêiner de execução. No v1 existe **apenas uma** missão não-encerrada (ativa/bloqueada/pausa).

**Invariante (Missão única):** é garantida na camada de domínio/repositório (único write-path) — toda criação/reativação/mudança de status de Mission valida que não existe outra Mission com `status !== 'closed'` antes de persistir.

| Campo | Tipo | Obrigatório | Observações |
|-------|------|-------------|-------------|
| id | string | ✅ | PK |
| title | string | ✅ | curto |
| outcome | string | ✅ | 1 frase |
| minCommitment | string | ✅ | “menor resultado aceitável” |
| status | 'active' \| 'blocked' \| 'paused' \| 'closed' | ✅ | |
| blockedReason | string | ❌ | se blocked |
| unblockAction | string | ❌ | se blocked |
| cooldownUntil | number | ❌ | ms; usado ao fechar |
| dodMin | ChecklistItem[] | ✅ | |
| dodGood | ChecklistItem[] | ✅ | |
| dodPremium | ChecklistItem[] | ✅ | |
| createdAt | number | ✅ | |
| updatedAt | number | ✅ | |

**Regras de domínio**

- Se `status === 'blocked'`: `blockedReason` e `unblockAction` devem existir.
- Se `status === 'closed'`: `cooldownUntil` pode existir (para reabrir com fricção).

---

### MicroAction

**Descrição:** unidade real de trabalho dentro de uma missão.

| Campo | Tipo | Obrigatório | Observações |
|-------|------|-------------|-------------|
| id | string | ✅ | PK |
| missionId | string | ✅ | FK lógica |
| order | number | ✅ | ordenação na missão |
| text | string | ✅ | verbo + objeto |
| artifact | string | ✅ | “o que vai existir no mundo” |
| estMinutes | number | ✅ | 5–15 padrão; ansiedade alta limita |
| state | 'todo' \| 'doing' \| 'done' | ✅ | |
| createdAt | number | ✅ | |
| updatedAt | number | ✅ | |

**Invariantes**

- Toda micro-ação tem `artifact` (regra de ouro do PRD).
- `estMinutes` guia “grande demais” e divisão (§9 PRD).

---

### Run

**Descrição:** sessão de foco (ritual). Preset padrão: 12–3–12.

| Campo | Tipo | Obrigatório | Observações |
|-------|------|-------------|-------------|
| id | string | ✅ | PK |
| missionId | string | ✅ | |
| runPresetId | string | ✅ | ex.: '12-3-12' |
| startedAt | number | ✅ | |
| endedAt | number | ❌ | |
| completed | boolean | ✅ | “chegou no Debrief” |
| aborted | boolean | ✅ | abortado conta no denominador (métrica) |
| swapsCount | number | ✅ | v1: só Start Ridículo / Rascunho feio |
| splitsCount | number | ✅ | Dividir |
| microActionId | string | ❌ | (opcional) qual micro-ação estava ativa |

---

### IdeaInbox

**Descrição:** ideias capturadas durante o Run; promover só quando missão encerrada ou bloqueada.

| Campo | Tipo | Obrigatório | Observações |
|-------|------|-------------|-------------|
| id | string | ✅ | PK |
| text | string | ✅ | 1 linha |
| createdAt | number | ✅ | |
| linkedMissionId | string | ❌ | referência opcional |

---

### UserSettings

**Descrição:** singleton. Ansiedade 0–10 e preset do Run.

| Campo | Tipo | Obrigatório | Observações |
|-------|------|-------------|-------------|
| id | 'singleton' | ✅ | chave fixa |
| anxietyLevel | number | ✅ | 0–10 |
| runPresetId | string | ✅ | default '12-3-12' |
| createdAt | number | ✅ | |
| updatedAt | number | ✅ | |

---

## Índices (Dexie schema)

Proposta v1 — só o que será consultado:

| Store | Schema (índices) |
|-------|-------------------|
| missions | `id, status, cooldownUntil, createdAt` |
| microActions | `id, missionId, [missionId+order], state, createdAt` |
| runs | `id, missionId, startedAt, runPresetId` |
| ideaInbox | `id, createdAt, linkedMissionId` |
| userSettings | `id` |

---

## Consultas previstas (para validar índices)

- **Home:** carregar missão não-encerrada por `status` (active/blocked/paused).
- **Próxima micro-ação:** primeira `microActions` com `missionId` e `state = 'todo'`, ordenada por `[missionId+order]`.
- **Histórico:** últimas missions com `status = 'closed'` por `createdAt` ou `updatedAt`.
- **Inbox:** últimas ideias por `createdAt` (máx. 5).
