# Issue 3 — Preset Run 12–3–12 + timer (motor)

**Título sugerido:** `[v1] 3) Preset Run 12–3–12 + timer (motor)`

**Labels:** `feature`, `v1`, `foundation`

---

**Parent:** [EPIC] Finish Mode v1 — Vertical Slice [#1](https://github.com/guiottodev/finish-mode/issues/1)

**Referências:** [PRD §10](https://github.com/guiottodev/finish-mode/blob/main/docs/PRD.md) · [DATA-MODEL-v1 (Run, UserSettings)](https://github.com/guiottodev/finish-mode/blob/main/docs/DATA-MODEL-v1.md) · [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md)

---

## Objetivo

Criar o motor de timer do Run com preset **12–3–12** e eventos consumíveis pela UI.

## Escopo

- **Preset:** `{ id: "12-3-12", focus1: 12, break: 3, focus2: 12 }` (minutos). 12 min foco, 3 min pausa, 12 min foco (duas rodadas).
- **Timer emite eventos:** `FOCUS_END`, `BREAK_END`, `RUN_END` (ou equivalente para UI assinar)
- **Persistência:** `UserSettings.runPresetId` existe e default = `12-3-12` (integrar com `settingsRepo`)

## Critérios de aceite

- [ ] Timer funciona em memória (v1): avança por fases e emite eventos
- [ ] UI consegue assinar eventos e renderizar estado (fase atual + tempo restante)
- [ ] `UserSettings.runPresetId` existe no modelo e default = `12-3-12`

## Tarefas

- [ ] Criar `src/domain/runTimer.ts` (máquina de estados simples: focus1 → break → focus2 → end)
- [ ] Integração mínima com `settingsRepo` (ler `runPresetId`; opcional: persistir ao trocar preset)

## DoD (issues)

Conforme [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md): build passa, timer testado manualmente (iniciar, ver fases e tempo), sem TODOs críticos.
