# Issue 9 — Debrief + Run abortado

**Título sugerido:** `[v1] 9) Debrief + Run abortado`

**Labels:** `feature`, `v1`

---

**Parent:** [EPIC] Finish Mode v1 — Vertical Slice [#1](https://github.com/guiottodev/finish-mode/issues/1)

**Referências:** [PRD §10, §5.2, §20](https://github.com/guiottodev/finish-mode/blob/main/docs/PRD.md) · [DATA-MODEL-v1 (Run)](https://github.com/guiottodev/finish-mode/blob/main/docs/DATA-MODEL-v1.md) · [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md)

---

## Objetivo

Fechar ciclo do Run com **Debrief** (feedback + próxima ação) e definir **Run abortado** de forma clara para métricas.

## Escopo

- **Debrief aparece quando:**
  - o usuário concluiu **Done** na micro-ação **e**
  - o ciclo de foco termina (ou o usuário confirma “Fechar ciclo”)
- **Debrief mostra:**
  - micro-ação concluída
  - progresso (X/Y = micro-ações concluídas vs. total de micro-ações da missão)
  - **próxima micro-ação** pronta (ou mensagem “nenhuma pendente”)
  - **CTA “Encerrar missão (Mínimo)”** quando `canCloseMissionMin(mission)` (mesma regra da issue 7; CTA disponível na Home e no Debrief)
  - Opcional: pergunta **“Encerrar aqui (Mínimo) ou seguir para Bom?”** quando DoD mínimo acabou de ser completado (progressive disclosure — issue 5)
- **Run abortado:**
  - Sair do Run **sem** passar pelo Debrief e **sem** ter marcado Done no ciclo atual → `aborted: true`, `completed: false`
  - Runs concluídos = chegou ao Debrief; abortados contam como “iniciados” no denominador da métrica Run completion rate (PRD §20)
- **Persistência:** ao chegar ao Debrief, Run é atualizado (`completed: true`, `endedAt`); ao abortar, Run é atualizado (`aborted: true`)

## Critérios de aceite

- [ ] Runs **concluídos** = usuário chegou ao Debrief (Done + fim de ciclo)
- [ ] Runs **abortados** = saiu do Run sem Debrief e sem Done no ciclo; contam como iniciados na métrica
- [ ] Debrief sempre mostra próxima micro-ação (ou CTA encerrar se não houver pendentes e DoD mínimo ok)
- [ ] CTA “Encerrar missão (Mínimo)” exibido no Debrief quando `canCloseMissionMin(mission)` (coordenado com issue 7)

## Tarefas

- [ ] Transições: Run → Debrief (após Done + fim de foco); Run → Home (abortar / “Encerrar Run agora”)
- [ ] Persistência do Run: `completed`, `aborted`, `endedAt` ao fechar
- [ ] Tela Debrief: micro-ação concluída, progresso, próxima micro-ação, CTA encerrar (se aplicável)
- [ ] Botão “Encerrar Run agora” no Run (registra abortado e volta à Home)

## DoD (issues)

Conforme [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md): build passa, fluxo testado manualmente (Done → Debrief → próxima ação; abortar → Home), sem TODOs críticos.
