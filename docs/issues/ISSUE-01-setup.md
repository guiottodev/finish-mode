# Issue 1 — Setup do app (Vite + TS + PWA)

**Título sugerido:** `[v1] 1) Setup do app — Vite + TS + PWA (skeleton)`

**Labels:** `feature`, `v1`, `foundation`

---

**Parent:** [EPIC] Finish Mode v1 — Vertical Slice [#1](https://github.com/guiottodev/finish-mode/issues/1)

**Referências:** [ADR-001 (stack)](https://github.com/guiottodev/finish-mode/blob/main/docs/ADR-001-stack-v1.md) · [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md)

---

## Objetivo

Criar o app web base (rodando) e preparar para PWA, conforme stack definida no ADR-001 (React + Vite + TypeScript, CSS Modules, vite-plugin-pwa).

## Escopo

- Criar projeto **Vite + TypeScript** (template React)
- Adicionar **PWA** (ex.: [vite-plugin-pwa](https://github.com/vite-pwa/vite-plugin-pwa))
- Rotas/telas vazias: **Home**, **Criar Missão**, **Run**, **Debrief**, **Histórico**
- Estrutura de pastas: `src/domain`, `src/storage`, `src/ui`, `src/pages` (ou `src/routes`)

## Critérios de aceite

- [ ] App sobe localmente sem erros (`pnpm dev` ou equivalente)
- [ ] Existe navegação entre as 5 telas (conteúdo placeholder ok)
- [ ] Manifest PWA configurado (nome, ícones placeholder ok)
- [ ] Service worker básico ativo em build (offline perfeito não é obrigatório ainda)

## Tarefas

- [ ] `npm create vite@latest` (ou `pnpm create vite`) + template React + TypeScript
- [ ] Instalar e configurar `vite-plugin-pwa`
- [ ] Criar rotas + layout mínimo (React Router ou similar)
- [ ] Criar pastas: `src/domain`, `src/storage`, `src/ui`, `src/pages`

## DoD (issues)

Conforme [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md): build passa, fluxo testado manualmente (navegar entre telas), sem TODOs críticos.
