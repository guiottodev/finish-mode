# Issue 16 — Histórico de finais (últimas 5 missões encerradas)

**Título sugerido:** `[v1] 16) Histórico de finais (últimas 5)`

**Labels:** `feature`, `v1`

---

**Parent:** [EPIC] Finish Mode v1 — Vertical Slice [#1](https://github.com/guiottodev/finish-mode/issues/1)

**Referências:** [PRD §19](https://github.com/guiottodev/finish-mode/blob/main/docs/PRD.md) · [DATA-MODEL-v1 (Mission)](https://github.com/guiottodev/finish-mode/blob/main/docs/DATA-MODEL-v1.md) · [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md)

---

## Objetivo

Reforçar identidade de **finalização**: tela com últimas missões **encerradas**, sem ranking/streak/comparação (PRD §19).

## Escopo

- **“Missões encerradas”** = missões com `status === 'closed'` (encerrada). Usar `closedAt` para ordenação por data de fechamento.
- **Home** não lista missões encerradas — só a **missão não-encerrada** (ativa/bloqueada/pausa) ou estado vazio.
- **Tela Histórico de finais:**
  - Lista das **últimas 5** missões encerradas (título + data de encerramento `closedAt`)
  - Sem ranking, streak ou comparação
  - Acesso: link na Home ou no layout (ex.: “Histórico”)

## Critérios de aceite

- [ ] Lista mostra **apenas** missões com `status === 'closed'` e limita a **5** itens
- [ ] Missões encerradas **não** aparecem na Home (Home só exibe missão não-encerrada ou vazio)
- [ ] Ordenação por `closedAt`; mais recente primeiro
- [ ] Sem métricas tóxicas (sem streak, ranking, comparação)

## Tarefas

- [ ] Query: usar índice composto `[status+closedAt]` para listar as 5 mais recentes (ex.: `missions.where('[status+closedAt]').between(['closed', 0], ['closed', Number.MAX_SAFE_INTEGER]).reverse().limit(5)`)
- [ ] Tela/página Histórico: renderizar lista (título + data)
- [ ] Navegação: link “Histórico” na Home ou no layout
- [ ] Opcional: ao clicar em uma missão encerrada, exibir detalhe e opção “Reabrir” (issue 14)

## DoD (issues)

Conforme [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md): build passa, fluxo testado manualmente (encerrar missão → ver no Histórico; Home sem encerradas), sem TODOs críticos.
