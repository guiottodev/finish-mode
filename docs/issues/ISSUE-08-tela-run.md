# Issue 8 — Tela Run (full-screen + ações essenciais)

**Título sugerido:** `[v1] 8) Tela Run — full-screen + ações essenciais`

**Labels:** `feature`, `v1`

---

**Parent:** [EPIC] Finish Mode v1 — Vertical Slice [#1](https://github.com/guiottodev/finish-mode/issues/1)

**Referências:** [PRD §10, §11](https://github.com/guiottodev/finish-mode/blob/main/docs/PRD.md) · [DATA-MODEL-v1 (Run)](https://github.com/guiottodev/finish-mode/blob/main/docs/DATA-MODEL-v1.md) · [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md)

---

## Objetivo

Ritual de execução **full-screen** com timer 12–3–12 e **poucas ações** (visibilidade mínima).

## Escopo

- **Renderizar:** micro-ação atual + artefato em destaque; timer 12–3–12 com fases (focus1 → break → focus2)
- **Ações (nesta ordem):**
  - **Done** — marca micro-ação como done; ao fim do ciclo de foco → transição para Debrief (issue 9)
  - **Dividir** — gera 3–4 micro-ações no molde listar → esboçar → preencher → revisar; incrementa `splitsCount`
  - **Rascunho feio** — cria micro-ação 5 min, artifact “rascunho salvo”; substitui foco na atual; incrementa `swapsCount`
  - **Start ridículo** — micro-ação mínima (ex.: “abrir arquivo e salvar”); substitui foco na atual; incrementa `swapsCount`
  - **Bloquear** — motivo + ação de desbloqueio; missão vira `blocked` e sai do Run
  - **Capturar ideia** — salva no Inbox (issue 15) e volta ao Run (não cria micro-ação)
- **Contadores no Run (v1):**
  - **No v1 não existe botão genérico “Trocar micro-ação”.**
  - `swapsCount` incrementa **apenas** quando **Start Ridículo** ou **Rascunho feio** substituem a micro-ação atual.
  - `splitsCount` incrementa em **Dividir**.
  - (Isso deixa a detecção de loop — issue 11 — coerente sem feature extra.)

## Critérios de aceite

- [ ] Usuário entra no Run e vê **uma micro-ação** em destaque + artefato
- [ ] Timer funciona e muda fases (focus1 → break → focus2); UI reflete fase atual e tempo restante
- [ ] Ao Done + fim de foco, há transição para Debrief (issue 9)
- [ ] Dividir cria micro-ações com `order` correto e incrementa `splitsCount`
- [ ] Start Ridículo e Rascunho feio incrementam `swapsCount`; não existe “Trocar” genérico

## Tarefas

- [ ] Ao iniciar Run: criar entidade `Run` (missionId, runPresetId, startedAt, completed: false, aborted: false, swapsCount: 0, splitsCount: 0)
- [ ] Persistir contadores `splitsCount` e `swapsCount` nas ações correspondentes
- [ ] Implementar ações no domínio (dividir, rascunho feio, start ridículo, bloquear, capturar ideia) e chamar na UI
- [ ] Integrar timer (issue 3) com eventos FOCUS_END / BREAK_END / RUN_END para transição ao Debrief

## DoD (issues)

Conforme [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md): build passa, fluxo testado manualmente (entrar no Run → Done → Debrief; Dividir; Rascunho feio / Start ridículo), sem TODOs críticos.
