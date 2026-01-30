# ADR-001 — Stack do Finish Mode v1 (PWA + Local-first)

**Status:** Accepted  
**Data:** 2026-01-30  
**Decisóres:** guiottodev  
**Contexto:** Finish Mode v1 precisa ser **PWA** (instalável) e **local-first** (persistência no dispositivo), com o menor risco de travar execução por decisões abertas.

---

## Contexto e problema

Precisamos escolher uma stack que:

- Rode como SPA e vire PWA (manifest + service worker básico).
- Persista dados localmente via IndexedDB com API simples.
- Seja rápida de implementar e manter (v1 sem excesso de infra).

Referências:

- [ADR como “decision log” e registro de trade-offs](https://adr.github.io/)
- [vite-plugin-pwa](https://github.com/vite-pwa/vite-plugin-pwa) — PWA em Vite, Workbox/offline
- [Dexie](https://dexie.org/) — IndexedDB offline-first, schema/indexes

---

## Decisão (Stack v1)

- **Framework:** React + Vite + TypeScript  
  Motivo: ecossistema já dominado → menor atrito no v1.
- **Build tool:** Vite (Vite 5+).
- **CSS:** CSS Modules (`*.module.css`)  
  Motivo: zero setup mental, escopo local por padrão; Vite suporta nativamente. Tailwind, se vier, entra como otimização, não pré-requisito.
- **PWA:** `vite-plugin-pwa` com configuração mínima (manifest + SW básico).
- **Persistência local:** Dexie (IndexedDB) como camada principal de dados. Schema/índices apenas para o que será consultado (regra oficial Dexie).
- **Linguagem:** TypeScript.

---

## Estratégia de persistência (risk-control)

- Dados no browser são **best-effort** por padrão e podem ser removidos sob pressão de storage (quota/evicção; Safari é agressivo).
- No primeiro uso (em HTTPS), o app chama `navigator.storage.persist()` e registra o resultado.
- Se `persist()` retornar `false`, o app deve tratar como “risco de perda” e recomendar backup (export/import) quando disponível.
- **COULD v1:** export/import JSON cedo, caso `persist()` negue ou para válvula de backup.

*(ADR como “decision log” existe para impedir redecidir isso toda semana.)*

---

## Consequências

**Positivas**

- Entrega rápida do v1 com base sólida (PWA + local-first).
- Menos decisões abertas por issue (stack fixa).
- Queries e migrações mais controláveis via schema/versioning do Dexie.

**Negativas / trade-offs**

- Sem sync multi-dispositivo no v1 (por escolha).
- Dados do browser podem ser best-effort; mitigação: `persist()` + export/import.
- Stack escolhida limita contribuições de quem prefere outro framework (aceito no v1).

---

## Alternativas consideradas

- **idb** (API mais baixa) no lugar de Dexie — descartado por ergonomia/velocidade.
- Framework diferente — descartado para evitar custo de troca no v1.
- Não fazer PWA no v1 — descartado porque o PRD pede instalabilidade.
- Tailwind no v1 — descartado; CSS Modules suficientes; Tailwind pode entrar depois.

---

## Notas de implementação

- VitePWA exige Vite 5+ (ver docs do plugin).
- Dexie: definir somente campos indexados; índices compostos via `[a+b]`.

---

## Links

- [ADR GitHub](https://adr.github.io/)
- [vite-plugin-pwa](https://github.com/vite-pwa/vite-plugin-pwa)
- [Dexie Version.stores()](https://dexie.org/docs/Version/Version.stores())
- [Dexie Compound Index](https://dexie.org/docs/Compound-Index)
- [MDN — Storage quotas and eviction](https://developer.mozilla.org/en-US/docs/Web/API/Storage_API/Storage_quotas_and_eviction_criteria)
