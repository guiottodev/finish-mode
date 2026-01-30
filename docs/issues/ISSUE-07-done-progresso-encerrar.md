# Issue 7 — Done + progresso + Encerrar no DoD mínimo + cooldown 24h

**Título sugerido:** `[v1] 7) Done + progresso + encerrar no DoD mínimo + cooldown 24h`

**Labels:** `feature`, `v1`

---

**Parent:** [EPIC] Finish Mode v1 — Vertical Slice [#1](https://github.com/guiottodev/finish-mode/issues/1)

**Referências:** [PRD §5.2, §15, §19](https://github.com/guiottodev/finish-mode/blob/main/docs/PRD.md) · [DATA-MODEL-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/DATA-MODEL-v1.md) · [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md)

---

## Objetivo

Concluir micro-ações (Done) e **encerrar missão no DoD mínimo** (manual), aplicando cooldown 24h. CTA “Encerrar missão (Mínimo)” disponível na **Home** e no **Debrief** quando `canCloseMissionMin(mission)`.

## Escopo

- **Botão Done:** marca micro-ação atual como `done`; atualiza “próxima micro-ação” na Home
- **Progresso simples:** exibir X/Y como **micro-ações concluídas vs. total de micro-ações** da missão (DoD mínimo é checado separadamente)
- **Encerrar missão:**
  - Permitido quando `dodMin` está 100% marcado (manual)
  - Ao encerrar: setar `closedAt = now`, `cooldownUntil = now + 24h` e `status: 'closed'`
- **Onde aparece o CTA “Encerrar missão (Mínimo)”:** na **Home** (issue 4) quando não há micro-ação pendente e `canCloseMissionMin(mission)`; e no **Debrief** (issue 9) quando `canCloseMissionMin(mission)`. Implementar `canCloseMissionMin(mission)` e `closeMissionMin(mission)` nesta issue; consumo na Home e no Debrief nas respectivas issues.

## Critérios de aceite

- [ ] Done atualiza estado da micro-ação e a “próxima micro-ação” na Home é recalculada corretamente
- [ ] Encerramento só aparece quando DoD mínimo está completo (`canCloseMissionMin(mission) === true`)
- [ ] Ao encerrar, `closedAt`, `cooldownUntil` e `status: 'closed'` persistidos; missão some da Home e aparece no Histórico (issue 16)
- [ ] CTA “Encerrar missão (Mínimo)” fica disponível na **Home** e no **Debrief** quando `canCloseMissionMin(mission)` (coordenar com issues 4 e 9)

## Tarefas

- [ ] Implementar `markMicroActionDone(missionId, microActionId)` (ou equivalente)
- [ ] Implementar `canCloseMissionMin(mission)`: todos os itens de `dodMin` com `done: true`
- [ ] Implementar `closeMissionMin(mission)`: setar `status: 'closed'`, `closedAt = now`, `cooldownUntil = now + 24h`, persistir
- [ ] Exibir progresso (X/Y) na Home e onde fizer sentido

## DoD (issues)

Conforme [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md): build passa, fluxo testado manualmente (Done → progresso → encerrar → cooldown → Histórico), sem TODOs críticos.
