# Issue 14 — Reabrir com cooldown + fricção (“por que reabrir?”)

**Título sugerido:** `[v1] 14) Reabrir com cooldown + motivo`

**Labels:** `feature`, `v1`

---

**Parent:** [EPIC] Finish Mode v1 — Vertical Slice [#1](https://github.com/guiottodev/finish-mode/issues/1)

**Referências:** [PRD §15](https://github.com/guiottodev/finish-mode/blob/main/docs/PRD.md) · [DATA-MODEL-v1 (Mission)](https://github.com/guiottodev/finish-mode/blob/main/docs/DATA-MODEL-v1.md) · [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md)

---

## Objetivo

Proteger o **fechamento** e evitar reabrir por culpa: reabrir **sempre** exige **1 frase** (motivo) e cria **1 micro-ação mínima** de retorno (PRD §15).

## Escopo

- **Reabrir** = voltar uma missão `status: 'closed'` para `status: 'active'` (independente do cooldown)
- **Fricção:** reabrir exige **1 frase** (“por que reabrir?”) — campo obrigatório; sem motivo não prossegue
- **Ao reabrir:**
  - `status` volta a `active`
  - Criar **1 micro-ação mínima de retorno** (Start ridículo) com artefato obrigatório; essa micro-ação aparece como **próxima ação** na Home
## Critérios de aceite

- [ ] Reabrir **sem** motivo não prossegue (validação no form/modal), mesmo após o cooldown
- [ ] Ao reabrir, missão volta a `active` e **1 micro-ação mínima** (Start ridículo) é criada e aparece como próxima ação na Home
- [ ] Invariante “uma missão não-encerrada” mantida (reabrir = reativar a única encerrada; issue 2)

## Tarefas

- [ ] Onde oferecer reabertura: Histórico (issue 16) ou detalhe da missão encerrada; modal/tela “Reabrir missão” com campo “Por que reabrir?”
- [ ] Implementar `reopenMission(missionId, reason)`: setar `status: 'active'`, criar 1 micro-ação Start ridículo, persistir
- [ ] Garantir que a nova micro-ação seja a “próxima” na Home (order e state corretos)

## DoD (issues)

Conforme [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md): build passa, fluxo testado manualmente (encerrar → reabrir com motivo → ver micro-ação mínima na Home), sem TODOs críticos.
