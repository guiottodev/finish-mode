# [EPIC] Finish Mode v1 — Vertical Slice (atingir critérios do §19)

**Labels:** `epic`, `v1`  
**Referências:** [PRD](docs/PRD.md) · [ADR-001](docs/ADR-001-stack-v1.md) · [DATA-MODEL-v1](docs/DATA-MODEL-v1.md) · [ISSUE-DOD-v1](docs/ISSUE-DOD-v1.md) · [GLOSSARY](docs/GLOSSARY.md)

---

## 1) Objetivo do Epic

Entregar um **v1 utilizável**, local-first (IndexedDB) e PWA, que cumpre os critérios testáveis do **§19 do PRD**.

**Hipótese v1:** Se o produto reduzir decisões (1 missão, 1 próxima ação), ritualizar execução (Run + Debrief) e permitir encerramento no DoD mínimo, então aumentamos fechamento de missões e diminuímos abandono.

---

## 2) Definição de Pronto do Epic (DoD)

- [ ] **Criar missão:** usuário consegue criar missão (title / outcome / compromisso mínimo) + aplicar template e gerar micro-ações (com artefato obrigatório).
- [ ] **Próxima ação + Done:** usuário vê a próxima micro-ação na Home e consegue marcar **Done**.
- [ ] **Run + Debrief:** usuário inicia **Run** com preset **12–3–12**, conclui pelo menos uma micro-ação e chega ao **Debrief**.
- [ ] **Encerrar + Histórico:** usuário encerra missão no **DoD mínimo** e a missão aparece no **Histórico de finais**.
- [ ] **Persistência:** reabrir o app mantém missão, micro-ações, runs e ideias (IndexedDB + `navigator.storage.persist()` conforme ADR-001).
- [ ] **PWA:** app instalável (manifest + service worker básico); estratégia offline v1 conforme ADR-001.
- [ ] **Roteiro de aceite (§19):** os 6 passos do PRD executados e aprovados.

---

## 3) Escopo v1 (controle de creep)

**MUST (sem isso não é v1)**  
Loop principal completo (criar missão → template → micro-ações → Run 12–3–12 → Done → Debrief → encerrar no mínimo → cooldown) + persistência local + PWA + invariante “uma missão não-encerrada” (DATA-MODEL-v1).

**SHOULD (entra se não atrasar MUST)**  
Slider de ansiedade (0–10) e regras 7–10 (≤5 min); detecção de loop + intervenção; missão bloqueada + desbloqueio; **pausa curta (status `paused`) + retomar**; Inbox + promover; reabrir com cooldown + motivo; Clareza em 30s (matriz).

**COULD (opcional v1)**  
Export/Import JSON (backup); priorizado como cinto de segurança para confiança em dados locais (risco de eviction).

**Fora de escopo**  
Sync multi-dispositivo, login, múltiplas missões ativas, planner semanal, gamificação pesada, IA “planejando a vida”. Lista completa de tarefas, tela de backlog, customização excessiva (PRD §0).

---

## 4) Princípios não negociáveis (referência)

- **Visibilidade mínima:** só missão ativa, micro-ação atual, próxima e progresso.
- **Próxima ação explícita:** primeira micro-ação pendente na fila (sem “gerar próxima” automático no v1).
- **Uma missão por vez:** garantida no write-path (DATA-MODEL-v1).
- **Artefato obrigatório:** toda micro-ação tem artefato.
- **Intervenção por ambiente:** anti-fuga altera opções/ambiente, não moraliza.
- **Válvulas de escape (PRD §3.7):** Bloquear = saída legítima; Pausa curta = “não hoje”; Reabrir com fricção = proteção contra culpa, não punição.

---

## 5) Stack e modelo (decisões fechadas)

- **Stack:** React + Vite + TypeScript, CSS Modules, Dexie (IndexedDB), vite-plugin-pwa → [ADR-001](docs/ADR-001-stack-v1.md).
- **Modelo:** entidades, campos e índices → [DATA-MODEL-v1](docs/DATA-MODEL-v1.md). Invariante “missão única” no domínio/repositório (único write-path).
- **Persistência:** `navigator.storage.persist()` no primeiro uso; quota/eviction como risco; export/import como válvula (ADR-001).
- **DoD das issues:** [ISSUE-DOD-v1](docs/ISSUE-DOD-v1.md).

---

## 6) Critérios de engenharia (prioridade v1)

Conforme [ISSUE-DOD-v1](docs/ISSUE-DOD-v1.md):

- **Motor de regras (domínio) testável e independente da UI:** transições de missão (ativa/bloqueada/pausa/closed), transições do Run (start → ciclo → done → debrief), contadores (swap/split), cálculo de próxima ação e de DoD mínimo atingido devem estar no domínio e testáveis sem UI.
- **Prioridade:** domínio + testes do domínio antes de polir UI; não começar pela UI bonita.
- Estrutura de pastas: `src/domain`, `src/storage`, `src/ui`, `src/pages` (ou `src/routes`).

---

## 7) Sub-issues (ordem sugerida)

**Fase 0 — Fundação**  
1. Setup do app (Vite + TS + PWA)  
2. Modelo de dados (TS) + IndexedDB (Dexie) + invariantes  
3. Preset 12–3–12 + timer (motor)

**Fase 1 — Fluxo mínimo**  
4. Home (estado vazio + missão única + próxima ação)  
5. Criar missão + compromisso mínimo + DoD (checklist)  
6. Templates v1 + geração de micro-ações (artefato obrigatório)  
7. Done + progresso + encerrar no DoD mínimo + cooldown

**Fase 2 — Run + Debrief**  
8. Tela Run (full-screen + ações essenciais)  
9. Debrief + Run abortado

**Fase 3–4 — Robustez e fechamento**  
10. Slider de ansiedade + regras 7–10 (≤5 min)  
11. Detecção de loop + intervenção  
12. Clareza em 30s (matriz travamento → resposta)  
13. Missão bloqueada + desbloqueio  
14. Reabrir com cooldown + motivo  
15. Inbox de ideias + promover  
16. Histórico de finais  
17. Export/Import (opcional v1)  
18. Pausa curta (status paused)

---

## 8) Roteiro de aceite (E2E humano — §19)

1. Abrir app → estado vazio + CTA “Criar missão”.  
2. Criar missão (title / outcome / compromisso mínimo) + selecionar template.  
3. Confirmar criação → micro-ações geradas (todas com artefato).  
4. Home mostra **próxima micro-ação**.  
5. Iniciar Run 12–3–12 → timer + micro-ação atual.  
6. Marcar Done → finalizar foco → ir para Debrief.  
7. Debrief mostra “feito” + próxima micro-ação.  
8. Completar DoD mínimo → sistema pergunta “Encerrar (Mínimo) ou seguir para Bom?”.  
9. Encerrar no mínimo → cooldown 24h → missão no Histórico.  
10. Fechar e reabrir navegador → estado preservado.

---

## 9) Checklist final do Epic

- [ ] MUST completo.  
- [ ] Roteiro de aceite (§19) aprovado.  
- [ ] Build + typecheck + lint passando.  
- [ ] Invariante “uma missão não-encerrada” validada.  
- [ ] PWA testada (instalação mínima em Chromium desktop).  
- [ ] Motor de regras (domínio) testável; prioridade domínio antes de UI respeitada.
