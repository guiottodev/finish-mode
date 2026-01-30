# Issue 12 — Clareza em 30s (matriz travamento → resposta do sistema)

**Título sugerido:** `[v1] 12) Clareza em 30s — matriz travamento → resposta`

**Labels:** `feature`, `v1`, `behavior`

---

**Parent:** [EPIC] Finish Mode v1 — Vertical Slice [#1](https://github.com/guiottodev/finish-mode/issues/1)

**Referências:** [PRD §8](https://github.com/guiottodev/finish-mode/blob/main/docs/PRD.md) · [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md)

---

## Objetivo

Quando o sistema não sabe “o próximo passo” (usuário travado), perguntar **uma coisa** e agir conforme a matriz travamento → resposta (PRD §8).

## Escopo

- **Modal ou tela** com a pergunta: “Qual o travamento agora?” e **5 opções:**
  - Não sei por onde começar
  - Está grande demais
  - Quero perfeito
  - Depende de alguém
  - Não sei se está bom
- **Ação do sistema (v1), por opção:**
  - **Por onde começar** → criar/acionar **Start ridículo** (1 micro-ação mínima + artefato)
  - **Grande demais** → **Dividir em 3–4** (listar → esboçar → preencher → revisar)
  - **Perfeito** → **Rascunho feio** (micro-ação 5 min, artefato “feio”)
  - **Depende de alguém** → **Bloquear** (motivo + ação de desbloqueio)
  - **Não sei se está bom** → micro-ação de **checagem objetiva** (ex.: checklist mínimo) ou DoD mínimo em evidência
- **Retorno:** após escolher 1 item, o sistema cria/aciona a micro-ação correspondente e retorna ao fluxo (Home ou Run)

## Critérios de aceite

- [ ] Escolher 1 travamento resulta na ação correta (Start ridículo, Dividir, Rascunho feio, Bloquear ou checklist)
- [ ] Usuário retorna à Home ou ao Run com a próxima ação já definida
- [ ] Acesso: opcional na Home quando não há micro-ação pendente (CTA “Clareza em 30s” — issue 4)

## Tarefas

- [ ] Tela/modal “Clareza em 30s” com 5 opções (copy do PRD §8)
- [ ] Mapear cada opção para ação do domínio (reutilizar funções já implementadas: Start ridículo, Rascunho feio, Dividir, Bloquear, checklist)
- [ ] Após ação: persistir micro-ação (se criada) e navegar para Home ou Run
- [ ] Integrar CTA na Home (issue 4) quando aplicável

## DoD (issues)

Conforme [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md): build passa, fluxo testado manualmente (abrir Clareza em 30s → escolher opção → ver próxima ação), sem TODOs críticos.
