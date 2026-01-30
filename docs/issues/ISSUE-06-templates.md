# Issue 6 — Templates v1 + geração de Micro-ações (artefato obrigatório)

**Título sugerido:** `[v1] 6) Templates v1 + geração de micro-ações (artefato obrigatório)`

**Labels:** `feature`, `v1`

---

**Parent:** [EPIC] Finish Mode v1 — Vertical Slice [#1](https://github.com/guiottodev/finish-mode/issues/1)

**Referências:** [PRD §7.1, §5.3](https://github.com/guiottodev/finish-mode/blob/main/docs/PRD.md) · [DATA-MODEL-v1 (MicroAction)](https://github.com/guiottodev/finish-mode/blob/main/docs/DATA-MODEL-v1.md) · [GLOSSARY](https://github.com/guiottodev/finish-mode/blob/main/docs/GLOSSARY.md) · [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md)

---

## Objetivo

Aplicar um template fixo e gerar micro-ações com **artefato sempre presente** (regra de ouro do PRD).

## Escopo

- **Catálogo de templates (v1 fixo):**
  - Pelo menos **1 template completo** (ex.: Documentação — usuário/técnica)
  - Demais podem ser “mínimos” (ex.: Polimento, Revisão, QA, Entrega com 2–3 micro-ações cada)
- **`applyTemplate(missionId, templateId)`** cria `microActions[]` com:
  - `text`, `artifact`, `estMinutes`, `state: 'todo'`, `order`
- **Regra:** nenhuma micro-ação sem `artifact` (validação no domínio)

## Critérios de aceite

- [ ] Ao criar missão (issue 5) e escolher template, micro-ações são geradas e aparecem na Home como próxima ação
- [ ] Validação impede criação de micro-ação sem `artifact`
- [ ] Todas as micro-ações geradas têm `artifact` preenchido (string concreta, ex.: “rascunho salvo”, “checklist marcado”)

## Tarefas

- [ ] Criar `src/domain/templates.ts` (arrays fixos de micro-ações por template)
- [ ] Implementar função `applyTemplate(missionId, templateId)` (persiste via `microActionsRepo`)
- [ ] Integrar no fluxo “Criar missão”: após salvar missão, aplicar template escolhido e redirecionar para Home

## DoD (issues)

Conforme [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md): build passa, fluxo testado manualmente (criar missão + template → ver micro-ações na Home), sem TODOs críticos.
