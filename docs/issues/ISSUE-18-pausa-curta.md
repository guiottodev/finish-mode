# Issue 18 — Pausa curta (status `paused`) + retomar

**Título sugerido:** `[v1] 18) Pausa curta — status paused + retomar`

**Labels:** `feature`, `v1`, `behavior`

---

**Parent:** [EPIC] Finish Mode v1 — Vertical Slice [#1](https://github.com/guiottodev/finish-mode/issues/1)

**Referências:** [PRD §3.3, §3.7](https://github.com/guiottodev/finish-mode/blob/main/docs/PRD.md) · [DATA-MODEL-v1 (Mission)](https://github.com/guiottodev/finish-mode/blob/main/docs/DATA-MODEL-v1.md) · [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md)

---

## Objetivo

Permitir **pausa curta** da missão (status `paused`) sem abrir outra missão e com retorno simples.

## Escopo

- **Pausar por hoje:** CTA na Home quando missão está `active` → seta `status: 'paused'`.
- **Missão pausada:** Home mostra estado “Pausada” e CTA **“Retomar”** → seta `status: 'active'`.
- **Run indisponível** quando missão está `paused`.
- **Invariante:** pausa **não** libera outra missão (continua existindo apenas 1 missão não‑encerrada).

## Critérios de aceite

- [ ] Pausar altera status para `paused` e persiste
- [ ] Missão `paused` não inicia Run
- [ ] Retomar volta status para `active`
- [ ] Não é possível criar/promover nova missão enquanto houver missão `paused`

## Tarefas

- [ ] Implementar `pauseMission(missionId)` e `resumeMission(missionId)` no domínio/repo
- [ ] Home: CTA “Pausar por hoje” quando `active`; CTA “Retomar” quando `paused`
- [ ] Garantir que a regra “uma missão não‑encerrada” continue válida

## DoD (issues)

Conforme [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md): build passa, fluxo testado manualmente (pausar → ver Home pausada → retomar), sem TODOs críticos.
