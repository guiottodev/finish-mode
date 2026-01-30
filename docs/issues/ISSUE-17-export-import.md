# Issue 17 — Export/Import (opcional v1) — backup JSON

**Título sugerido:** `[v1] 17) Export/Import (opcional) — backup JSON`

**Labels:** `feature`, `v1`, `optional`

---

**Parent:** [EPIC] Finish Mode v1 — Vertical Slice [#1](https://github.com/guiottodev/finish-mode/issues/1)

**Referências:** [PRD §17](https://github.com/guiottodev/finish-mode/blob/main/docs/PRD.md) · [ADR-001](https://github.com/guiottodev/finish-mode/blob/main/docs/ADR-001-stack-v1.md) · [DATA-MODEL-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/DATA-MODEL-v1.md) · [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md)

---

## Objetivo

Permitir **backup local** em JSON (local-first); válvula de segurança quando `navigator.storage.persist()` retorna false ou para recuperação (ADR-001, PRD §17). **Prioridade:** cinto de segurança para confiança em dados locais (risco de eviction/quota).

## Escopo

- **Export:** baixar arquivo JSON com dados das stores: missões, micro-ações, runs, ideias (Inbox), UserSettings. Formato legível e versionável (ex.: data de export + schema version).
- **Import:** carregar arquivo JSON; validação **mínima** (estrutura esperada, tipos básicos); **aviso** antes de sobrescrever (ex.: “Isso vai substituir seus dados locais”). Após import, app deve funcionar sem quebrar invariantes (ex.: no máximo 1 missão não-encerrada).
- **Comportamento pós-import (v1):** **substituir** dados locais (IndexedDB) pelos do JSON (sem merge).

## Critérios de aceite

- [ ] Export gera JSON válido contendo missões, micro-ações, runs, ideias, settings (ou subset definido)
- [ ] Import restaura dados e app volta a funcionar (Home, Run, Histórico etc. consistentes)
- [ ] Invariantes preservadas após import (ex.: apenas 1 missão não-encerrada; se JSON tiver mais de uma, normalizar no import)
- [ ] Aviso claro antes de import (risco de sobrescrever)

## Tarefas

- [ ] Função export: ler todas as stores Dexie, montar objeto JSON, trigger download (nome com data ex.: `finish-mode-backup-YYYY-MM-DD.json`)
- [ ] Função import: ler arquivo, validar estrutura mínima, transação Dexie para substituir dados; aviso em modal antes de executar
- [ ] Pós-import: garantir 1 missão não-encerrada (se JSON tiver várias ativas, manter apenas a mais recente como ativa e demais como paused ou closed)
- [ ] UI: botões Export e Import (ex.: em Configurações ou na Home, discreto)

## DoD (issues)

Conforme [ISSUE-DOD-v1](https://github.com/guiottodev/finish-mode/blob/main/docs/ISSUE-DOD-v1.md): build passa, fluxo testado manualmente (export → import → ver dados restaurados), sem TODOs críticos.
