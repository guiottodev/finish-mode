# Issue 11 — Detecção de loop + intervenção silenciosa

**Título sugerido:** `[v1] 11) Detecção de loop + intervenção silenciosa`

**Labels:** `feature`, `v1`, `behavior`

---

**Parent:** [EPIC] Finish Mode v1 — Vertical Slice [#1](https://github.com/guiottodev/finish-mode/issues/1)

**Referências:** [PRD §11](https://github.com/guiottodev/finish-mode/blob/main/docs/PRD.md) · [DATA-MODEL-v1 (Run)](https://github.com/guiottodev/finish-mode/blob/main/docs/DATA-MODEL-v1.md) · [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md)

---

## Objetivo

Detectar **fuga sofisticada** (muitos swaps/splits sem conclusão) e alterar o **ambiente** sem bronca — reduzir opções e destacar fallbacks (PRD §11).

## Escopo

- **Definir loop quando (v1), durante um único Run:**
  - `swapsCount >= 3` **OU**
  - `splitsCount >= 2` **OU**
  - `(swapsCount + splitsCount >= 4)` **E** nenhuma micro-ação concluída no Run
- **Intervenção por ambiente (sem bronca):**
  - Reduzir botões visíveis (ex.: esconder “Trocar” se existir; no v1 já não existe — garantir que Dividir fique condicional ou em evidência reduzida)
  - Destacar **Rascunho feio** e **Start ridículo**
- **Registro:** evento de loop pode ser registrado no Run (ou log) para debug/telemetria futura

**Fora do v1:** encurtar o próximo preset como intervenção extra (ex.: 8–2–8).

## Critérios de aceite

- [ ] Ao atingir os limiares de loop, a UI muda automaticamente (menos opções, destaque para Rascunho feio e Start ridículo)
- [ ] Intervenção é silenciosa (sem mensagem moralizante)
- [ ] Opcional: evento de loop registrado (campo ou log) para análise posterior

## Tarefas

- [ ] Função no domínio: `isLoopDetected(run)` conforme limiares do PRD §11
- [ ] No Run: ao atualizar swapsCount/splitsCount (ou ao renderizar), verificar loop e passar estado “em loop” para a UI
- [ ] UI: quando em loop, reduzir opções visíveis e destacar Rascunho feio e Start ridículo

## DoD (issues)

Conforme [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md): build passa, fluxo testado manualmente (simular swaps/splits até limiar → ver intervenção), sem TODOs críticos.
