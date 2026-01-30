# Issue 10 — Slider de ansiedade + regras de dificuldade (faixa 7–10 ≤ 5 min)

**Título sugerido:** `[v1] 10) Slider de ansiedade + regras 7–10 (≤5 min)`

**Labels:** `feature`, `v1`, `behavior`

---

**Parent:** [EPIC] Finish Mode v1 — Vertical Slice [#1](https://github.com/guiottodev/finish-mode/issues/1)

**Referências:** [PRD §12](https://github.com/guiottodev/finish-mode/blob/main/docs/PRD.md) · [DATA-MODEL-v1 (UserSettings)](https://github.com/guiottodev/finish-mode/blob/main/docs/DATA-MODEL-v1.md) · [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md)

---

## Objetivo

Reduzir fricção e ajustar dificuldade **sem “diagnóstico”**: slider 0–10 persiste e altera tamanho das micro-ações e opções no Run conforme faixa (PRD §12).

## Escopo

- **Slider 0–10** na Home (e opcionalmente no início do Run)
- Persistir em `UserSettings.anxietyLevel`
- **Regras v1 por faixa:**
  - **0–3 (Normal):** estMinutes máximo 15; todos os botões visíveis no Run
  - **4–6 (Cautela):** estMinutes máximo recomendado 10; motor sugere dividir acima disso; destaca “Dividir”
  - **7–10 (Fragil):** novas micro-ações e divisões com **estMinutes ≤ 5**; botões visíveis: Done, Start Ridículo, Rascunho feio, Capturar ideia; Dividir só após 1 conclusão ou via prompt “está grande?”
- Após 1 Run concluído com ansiedade 7–10: sugerir “recalibrar” (1 clique)

## Critérios de aceite

- [ ] Slider persiste entre sessões (`UserSettings.anxietyLevel`)
- [ ] Ao usar Rascunho feio ou Start ridículo na faixa 7–10, micro-ações geradas têm `estMinutes ≤ 5`
- [ ] UI do Run reduz opções conforme faixa (7–10: sem Dividir em evidência até 1 conclusão, ou conforme PRD §12)

## Tarefas

- [ ] Componente slider na Home (e opcionalmente no Run); ler/escrever `settingsRepo`
- [ ] Regras no domínio: ao criar micro-ação (rascunho feio, start ridículo, divisão), respeitar `anxietyLevel` (estMinutes ≤ 5 se 7–10)
- [ ] Ajustar UI do Run por faixa (botões visíveis conforme PRD §12)
- [ ] Sugestão “recalibrar” após Run concluído com ansiedade 7–10

## DoD (issues)

Conforme [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md): build passa, fluxo testado manualmente (slider 7–10 → Rascunho feio com ≤5 min; opções no Run), sem TODOs críticos.
