# Finish Mode — Definition of Done (Issues) v1

**Objetivo:** fechar issues com **clareza de completude** (sem “quase pronto”).  
**Inspiração:** DoD cria transparência e entendimento comum do que é “Done” (Scrum Guide / Scrum.org).

---

## DoD mínimo (todas as issues)

- [ ] Implementado conforme escopo + critérios de aceite da issue.
- [ ] `pnpm build` (ou equivalente) passa + TypeScript sem erros.
- [ ] Fluxo principal da issue testado manualmente e descrito na própria issue (passos + resultado esperado).
- [ ] Sem TODOs “críticos” escondidos; se existir dívida, virar issue nova.

---

## DoD recomendado (quando fizer sentido)

- [ ] Teste automatizado adicionado/ajustado (unit/integration) **ou** justificativa escrita do porquê não.
- [ ] Docs atualizados se a change altera comportamento (PRD / GLOSSARY / README / DATA-MODEL / ADR).

---

## Padrão de PR (se usar PRs)

- [ ] Link da issue no PR.
- [ ] Checklist do DoD preenchido no PR/issue.

---

## Referências

- Issues devem alinhar ao **PRD** (§19 para critérios de “feito” do v1).
- Stack e persistência: **ADR-001**.
- Entidades e invariantes: **DATA-MODEL-v1**.
