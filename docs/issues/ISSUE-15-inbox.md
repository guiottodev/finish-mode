# Issue 15 — Inbox de ideias (capturar e promover)

**Título sugerido:** `[v1] 15) Inbox de ideias — capturar e promover`

**Labels:** `feature`, `v1`

---

**Parent:** [EPIC] Finish Mode v1 — Vertical Slice [#1](https://github.com/guiottodev/finish-mode/issues/1)

**Referências:** [PRD §13](https://github.com/guiottodev/finish-mode/blob/main/docs/PRD.md) · [DATA-MODEL-v1 (IdeaInbox)](https://github.com/guiottodev/finish-mode/blob/main/docs/DATA-MODEL-v1.md) · [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md)

---

## Objetivo

**Capturar** ideias durante o Run sem interromper o fluxo; **promover** para nova missão **apenas quando não existir missão não-encerrada** (PRD §13).

## Escopo

- **Capturar ideia (no Run):** input 1 linha → salva em `IdeaInbox` (text, createdAt, `linkedMissionId` da missão atual quando existir) → retorna **imediatamente** ao Run. **Não** cria micro-ação automaticamente.
- **Listar:** até **5 ideias recentes** (ordenadas por createdAt); acessível na **Home** e no **Debrief** (link ou seção discreta).
- **Promover:** transformar uma ideia em **nova missão**. Só permitido quando **não existe missão não-encerrada** (ou seja, missão atual encerrada). Ao promover:
  - Criar nova missão com `outcome = texto da ideia` (ou título derivado)
  - Iniciar fluxo de **compromisso mínimo** + escolha de template (como em Criar missão — issues 5 e 6)
  - Remover a ideia do Inbox após promoção

## Critérios de aceite

- [ ] Captura no Run salva no Inbox e volta ao Run sem criar micro-ação
- [ ] Lista mostra no máximo 5 ideias recentes (Home e/ou Debrief)
- [ ] “Promover” só habilitado quando **não existe missão não-encerrada** (missão encerrada); ao promover, cria nova missão e inicia fluxo compromisso mínimo + template
- [ ] Ideia promovida é removida do Inbox

## Tarefas

- [ ] Ação “Capturar ideia” no Run (issue 8): modal/input 1 linha → `ideasRepo.add({ text, createdAt, linkedMissionId })` → fechar e voltar ao Run
- [ ] Componente/seção Inbox: listar últimas 5 (query por createdAt); exibir na Home e no Debrief
- [ ] Ação “Promover”: verificar que não há missão não-encerrada; criar missão a partir do texto; **remover ideia do Inbox**; redirecionar para fluxo Criar missão (compromisso mínimo + template) ou pré-preencher outcome e ir para Criar missão

## DoD (issues)

Conforme [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md): build passa, fluxo testado manualmente (capturar no Run → ver no Inbox; promover com missão encerrada → nova missão), sem TODOs críticos.
