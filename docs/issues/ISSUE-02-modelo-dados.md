# Issue 2 — Modelo de dados (TS) + IndexedDB (Dexie) + invariantes

**Título sugerido:** `[v1] 2) Modelo de dados (TS) + IndexedDB (Dexie) + invariantes`

**Labels:** `feature`, `v1`, `foundation`

---

**Parent:** [EPIC] Finish Mode v1 — Vertical Slice [#1](https://github.com/guiottodev/finish-mode/issues/1)

**Referências:** [DATA-MODEL-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/DATA-MODEL-v1.md) · [ADR-001](https://github.com/guiottodev/finish-mode/blob/main/docs/ADR-001-stack-v1.md) · [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md)

---

## Objetivo

Implementar tipos TypeScript + persistência local com Dexie e garantir a regra **“uma missão não-encerrada”** (invariante no write-path).

## Contexto

Dexie simplifica o uso de IndexedDB e reduz a complexidade da API nativa ([dexie.org](https://dexie.org/)).

## Escopo

- **Tipos/entidades** (conforme DATA-MODEL-v1):
  - `Mission`, `MicroAction`, `Run`, `IdeaInboxItem`, `UserSettings`
- **Storage com Dexie:** repositórios simples
  - `missionsRepo`, `microActionsRepo`, `runsRepo`, `ideasRepo`, `settingsRepo`
- **Invariante:** só pode existir **1 missão não-encerrada** (status `active` / `blocked` / `paused`). Garantida na camada de domínio/repositório (único write-path) — ver DATA-MODEL-v1.

## Critérios de aceite

- [ ] Criar/ler/atualizar/deletar entidades persistem entre refresh
- [ ] Tentar criar 2ª missão não-encerrada resulta em **erro controlado** (ex.: “Já existe uma missão ativa”) — **sem auto-pause no v1**
- [ ] Seeds simples (opcional): inserir `UserSettings` default (`anxietyLevel: 0`, `runPresetId: '12-3-12'`)

## Tarefas

- [ ] Definir schemas Dexie (stores + índices conforme DATA-MODEL-v1)
- [ ] Implementar tipos TS para todas as entidades
- [ ] Implementar funções CRUD e queries (ex.: `getActiveOrLastMission()`, `getNextMicroAction(missionId)`)
- [ ] Implementar invariante em `missionsRepo.createMission()` (ou no domínio antes de persistir): bloquear criação se existir missão com `status !== 'closed'`

## DoD (issues)

Conforme [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md): build passa, fluxo testado manualmente (CRUD + tentativa de 2ª missão), sem TODOs críticos.
