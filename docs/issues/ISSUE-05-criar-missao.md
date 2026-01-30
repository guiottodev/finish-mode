# Issue 5 — Criar Missão (title / outcome / compromisso mínimo + DoD checklist)

**Título sugerido:** `[v1] 5) Criar Missão — title/outcome/compromisso mínimo + DoD (checklist)`

**Labels:** `feature`, `v1`

---

**Parent:** [EPIC] Finish Mode v1 — Vertical Slice [#1](https://github.com/guiottodev/finish-mode/issues/1)

**Referências:** [PRD §3.5, §5.1, §5.2, §10.2](https://github.com/guiottodev/finish-mode/blob/main/docs/PRD.md) · [DATA-MODEL-v1 (Mission)](https://github.com/guiottodev/finish-mode/blob/main/docs/DATA-MODEL-v1.md) · [GLOSSARY](https://github.com/guiottodev/finish-mode/blob/main/docs/GLOSSARY.md) · [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md)

---

## Objetivo

Permitir **criar missão** com contrato psicológico (compromisso mínimo) e **DoD em 3 níveis** (checklists), salvando no IndexedDB como única missão não-encerrada.

## Escopo

- **Formulário:**
  - `title` (curto)
  - `outcome` (1 frase)
  - `compromisso mínimo` (1 frase) — “Qual é o menor resultado que você aceita entregar?”
  - **DoD em 3 níveis:** salvar os 3 checklists `dodMin`, `dodGood`, `dodPremium` (formato `[{ text, done }]`). Ao menos `dodMin` editável no form; good/premium podem ser editáveis ou placeholders.
- **Progressive disclosure no uso** (fluxo após criar — ver issues 7 e 9):
  - Usuário só é obrigado ao **Mínimo** para encerrar.
  - Ao concluir o Mínimo, o sistema pergunta: **“Encerrar aqui (Mínimo) ou seguir para Bom?”** (onde: Debrief — issue 9 — e/ou Home quando `canCloseMissionMin`).
  - Se escolher “Bom”, liberar marcação do `dodGood`.
  - Após completar “Bom”, oferecer “Premium” como opcional.
- **Ao salvar:** missão criada com `status: 'active'` e vira a **única não-encerrada** (invariante — issue 2)
- **Template:** escolha de template aplicada na issue 6; nesta issue o foco é persistir a missão com os campos acima (micro-ações virão da issue 6)

## Critérios de aceite

- [ ] Missão salva no IndexedDB com todos os campos obrigatórios do DATA-MODEL-v1
- [ ] Ao salvar, a nova missão vira a **única não-encerrada** (qualquer outra fica `paused` ou erro controlado, conforme decisão da issue 2)
- [ ] `dodMin`, `dodGood`, `dodPremium` são arrays `[{ text: string, done: boolean }]`; ao menos `dodMin` editável no form
- [ ] Ao concluir `dodMin`, aparece a pergunta **“Encerrar aqui (Mínimo) ou seguir para Bom?”** (implementação na issue 7/9; critério de aceite do fluxo completo)
- [ ] “Bom” só fica interativo após o mínimo; “Premium” só após “Bom”
- [ ] Validações mínimas: title e outcome não vazios; compromisso mínimo não vazio
- [ ] Após criar, redirecionar para Home (onde a próxima ação aparecerá após issue 6 gerar micro-ações)

## Tarefas

- [ ] Form: campos title, outcome, compromisso mínimo, checklist DoD mínimo (itens editáveis); dodGood/dodPremium como campos (editáveis ou placeholders)
- [ ] Validações mínimas (required, trim)
- [ ] Chamar `missionsRepo` (e garantir invariante) + persistir `createdAt`/`updatedAt`
- [ ] Navegação pós-criação: ir para Home (ou para passo “aplicar template” se unificar com issue 6 no fluxo)

## DoD (issues)

Conforme [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md): build passa, fluxo testado manualmente (criar missão → ver na Home após refresh), sem TODOs críticos.
