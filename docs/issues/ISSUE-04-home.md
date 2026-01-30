# Issue 4 — Home (estados e “próxima ação”)

**Título sugerido:** `[v1] 4) Home — estados e próxima ação`

**Labels:** `feature`, `v1`

---

**Parent:** [EPIC] Finish Mode v1 — Vertical Slice [#1](https://github.com/guiottodev/finish-mode/issues/1)

**Referências:** [PRD §3.1, §10.1](https://github.com/guiottodev/finish-mode/blob/main/docs/PRD.md) · [DATA-MODEL-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/DATA-MODEL-v1.md) · [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md)

---

## Objetivo

Tela **Home** com visibilidade mínima e **próxima micro-ação sempre explícita** (princípio do PRD).

## Escopo

- **Estado vazio:** “Nenhuma missão” + CTA “Criar missão”
- **Estado com missão única (não-encerrada):**
  - Título da missão + status
  - **“Próxima micro-ação”:** primeira micro-ação com estado `todo` ou `doing` (ordenada por `order`) — sempre que existir na fila
  - CTA “Start” (na Fase 2 leva ao Run; na Fase 1 pode levar a detalhe simples da micro-ação)
- **Sem lista gigante:** só missão ativa + próxima ação + progresso (ex.: X/Y micro-ações)
- **Sem micro-ação pendente:** mostrar “Encerrar missão (Mínimo)” se `canCloseMissionMin(mission)`; caso contrário, opcional: CTA “Clareza em 30s” (issue 12) como caminho de destrave — **não** “gerar próxima” automático no v1 (PRD)

## Critérios de aceite

- [ ] **“Próxima ação”** = primeira micro-ação pendente na fila, sempre que existir
- [ ] Sem pendentes: ou **“Encerrar missão (Mínimo)”** (se `canCloseMissionMin(mission)`), ou **“Clareza em 30s”** (se travado) — sem “gerar próxima” no v1
- [ ] Home mostra sempre **1 próxima ação** (ou CTA encerrar / Clareza em 30s quando aplicável)

## Tarefas

- [ ] Query: carregar missão não-encerrada + próxima micro-ação (usar índices do DATA-MODEL-v1)
- [ ] Render mínimo: estado vazio vs. estado com missão (título, status, próxima micro-ação, CTA Start)
- [ ] Exibir CTA “Encerrar missão (Mínimo)” quando não há micro-ação pendente e `canCloseMissionMin(mission)` (lógica da issue 7)
- [ ] Navegação: CTA “Criar missão” → tela Criar Missão (issue 5)

## DoD (issues)

Conforme [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md): build passa, fluxo testado manualmente (vazio → criar missão; com missão → ver próxima ação), sem TODOs críticos.
