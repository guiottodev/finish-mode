# Issue 13 — Missão bloqueada (UX + desbloqueio)

**Título sugerido:** `[v1] 13) Missão bloqueada — UX + desbloqueio`

**Labels:** `feature`, `v1`

---

**Parent:** [EPIC] Finish Mode v1 — Vertical Slice [#1](https://github.com/guiottodev/finish-mode/issues/1)

**Referências:** [PRD §14](https://github.com/guiottodev/finish-mode/blob/main/docs/PRD.md) · [DATA-MODEL-v1 (Mission)](https://github.com/guiottodev/finish-mode/blob/main/docs/DATA-MODEL-v1.md) · [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md)

---

## Objetivo

Tornar o **bloqueio** explícito e **impedir Run** quando a missão está bloqueada (PRD §14).

## Escopo

- **Se missão está bloqueada** (`status === 'blocked'`):
  - **Home** mostra: “Bloqueada: [motivo]” e CTA único **“Desbloquear: [unblockAction]”**
  - **Start Run** indisponível (não inicia Run nesse estado)
  - Botão **“Desbloqueei”**: usuário marca que executou a ação de desbloqueio → missão volta a `status: 'active'`
- Bloquear é acionado no Run (issue 8) ou via Clareza em 30s (issue 12); nesta issue o foco é a **UX da Home** com missão bloqueada e o fluxo de desbloqueio.

## Critérios de aceite

- [ ] Missão bloqueada **nunca** inicia Run (botão Start desabilitado ou escondido)
- [ ] Home exibe motivo e ação de desbloqueio de forma clara
- [ ] Ao clicar “Desbloqueei”, status volta a `active` e o fluxo normal retorna (Start Run disponível)

## Tarefas

- [ ] Na Home: quando `mission.status === 'blocked'`, renderizar bloco “Bloqueada” + motivo + unblockAction + botão “Desbloqueei”
- [ ] Desabilitar ou esconder “Start Run” quando missão bloqueada
- [ ] Implementar `unblockMission(missionId)` ou equivalente: setar `status: 'active'`, persistir
- [ ] Garantir que `blockedReason` e `unblockAction` existam quando status é `blocked` (validação na ação Bloquear — issue 8)

## DoD (issues)

Conforme [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md): build passa, fluxo testado manualmente (bloquear missão → ver Home bloqueada → Desbloqueei → Run disponível), sem TODOs críticos.
