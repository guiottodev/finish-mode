# Finish Mode — PRD/Especificação v1.0 

## Changelog desta revisão

Incluído/clarificado no v1.0:

- Matriz Travamento → Resposta do sistema (“Clareza em 30s”)
- Critério v1 para micro-ação grande demais
- Regras/limiares de detecção de loop
- Regras por faixa do slider de ansiedade
- Fluxo completo da Inbox de ideias
- Decisão do timer/ritual do Run e campos necessários
- Clarificação da “próxima ação” (removida ambiguidade de “amanhã”)
- Edge cases: missão bloqueada, pausa curta vs trocar de missão, DoD mínimo → bom/premium
- Escopo v1 de templates (sequência fixa) e persistência/offline
- Ajustes no modelo de dados (remover/definir campos ambíguos)
- Preset 12–3–12 explicado; regra estMinutes ≤ 5 na faixa Frágil; definição de run completion rate; formato de checklist do DoD

---

## 0) Definição do produto

Finish Mode é um copiloto de execução para terminar coisas já iniciadas, especialmente na fase de acabamento: polir, revisar, documentar, fechar pontas e entregar.

**Não é:** planner, backlog, gerenciador de projetos, app de ideias, ferramenta colaborativa.

---

## 1) Problema

Na fase “chata”, o bloqueio típico é:

- fricção de início
- ambiguidade do “feito”
- baixa recompensa imediata
- fuga sofisticada (troca, reorganiza, “pesquisa”, microvitória vazia)

**Hipótese:** remover escolha + definir “mínimo aceitável” + exigir artefato por micro-ação aumenta fechamento.

---

## 2) Persona

**Primária:** competente travado no acabamento; boa capacidade, baixa tolerância a ambiguidade e repetição; tende a fugir sofisticadamente.

**Anti-persona:** quer customização infinita, backlog completo, colaboração, planejamento semanal.

---

## 3) Princípios não negociáveis

### 3.1 Visibilidade mínima

O usuário vê apenas: missão ativa, micro-ação atual, próxima micro-ação, progresso.

### 3.2 Próxima ação explícita

Se o sistema não souber, faz 1 pergunta única (≤10s).

### 3.3 Uma missão por vez (com estados)

Só existe 1 missão não-encerrada no sistema. Estados:

- **Ativa**
- **Bloqueada** (com motivo + ação de desbloqueio)
- **Pausa curta** (pausa do trabalho; não habilita outra missão)
- **Encerrada**

**Regra v1:** Pausa curta não permite iniciar outra missão. Para “mudar de tema”, o usuário precisa encerrar a missão atual ou marcá-la como bloqueada (com motivo real).

### 3.4 Execução > planejamento

O sistema recompensa: micro-ações concluídas, runs concluídos, missões encerradas.

### 3.5 Contrato psicológico (obrigatório)

Antes da missão ficar ativa:

*“Qual é o menor resultado que você aceita entregar?”*

Isso vira o Compromisso Mínimo e ancora o DoD mínimo.

### 3.6 Nenhuma micro-ação sem artefato (obrigatório)

Toda micro-ação precisa declarar o artefato: *“o que vai existir no mundo quando terminar?”*.

---

## 4) Conceitos (glossário curto)

| Termo | Definição |
|--------|-----------|
| **Missão** | Contêiner de fechamento (não tarefa). |
| **Compromisso mínimo** | Menor entrega aceitável (contrato psicológico). |
| **DoD** | Mínimo / bom / premium. |
| **Micro-ação** | Passo de 5–15 min com artefato. |
| **Artefato** | Coisa concreta criada/alterada (rascunho salvo, checklist marcado etc.). |
| **Run** | Ritual fechado de execução. |
| **Template** | Sequência padrão de fechamento (conteúdo do produto). |
| **Start Ridículo** | Micro-ação quase impossível de falhar. |
| **Rascunho feio** | Fallback universal automático. |

---

## 5) Estruturas centrais

### 5.1 Missão

**Campos:**

- title (curto)
- outcome (1 frase)
- minCommitment (1 frase)
- dodMin, dodGood, dodPremium (checklists)
- microActions[] (fila ordenada)
- status (ativa / bloqueada / pausa / encerrada)
- blockedReason + unblockAction (se bloqueada)
- cooldownUntil (se encerrada)

**Formato DoD:** dodMin, dodGood e dodPremium usam o mesmo formato de checklist: `[{ text: string, done: boolean }]` (equivalente à estrutura interna de um DoDLevel).

### 5.2 DoD (mínimo / bom / premium)

- Só o mínimo é necessário para encerrar.
- Ao concluir o mínimo, o sistema pergunta uma vez: *“Encerrar aqui (mínimo) ou seguir para ‘Bom’?”*
- *“Premium”* aparece apenas como opcional após *“Bom”*.

### 5.3 Micro-ação

**Campos:**

- text (verbo + objeto)
- artifact (string curta, concreta)
- estMinutes (fonte da verdade para tamanho)
- state (todo / doing / done)

**Regra de validade:** micro-ação sem artefato não é criada pelo motor.

---

## 6) Loop principal

1. Criar missão (title + outcome)
2. Definir compromisso mínimo (5s)
3. Aplicar template (gera micro-ações iniciais)
4. Start Run
5. Executar micro-ação
6. Debrief (feedback + próxima micro-ação pronta)
7. Encerrar ao atingir DoD mínimo (com opção de seguir para “Bom”)

---

## 7) Templates e geração (escopo v1 explícito)

### 7.1 Aplicar template (v1 = sequência fixa)

**No v1:**

- Template = sequência fixa de micro-ações + artefatos típicos.
- O usuário pode editar texto / artefato / estMinutes apenas na criação da missão (antes do primeiro Run).
- Durante o Run, edição livre não existe (só dividir / fallback / start ridículo).

**Templates v1 mínimos:**

- Documentação (usuário / técnica)
- Polimento (UI / texto / regras)
- Revisão (consistência / edge cases)
- QA (smoke / regressão curta)
- Entrega (confirmar envio/publicação)

---

## 8) Clareza em 30 segundos (matriz Travamento → Ação)

Quando o sistema precisa decidir *“o que fazer agora”*, ele pergunta:

*“Qual o travamento agora?”* e aplica a matriz abaixo:

| Travamento | Resposta do sistema (v1) | Saída obrigatória |
|------------|---------------------------|-------------------|
| Não sei por onde começar | Cria 1 micro-ação mínima com artefato (Start Ridículo por padrão) | 1 artefato |
| Está grande demais | Oferece Dividir em 3 (listar → esboçar → preencher) | 3 micro-ações + 3 artefatos |
| Quero perfeito | Força DoD mínimo em evidência + cria “Rascunho feio (5 min)” | 1 artefato “feio” |
| Depende de alguém | Propõe Bloquear + define unblockAction (ex.: “mandar msg X”) | Ação de desbloqueio |
| Não sei se está bom | Gera micro-ação de checagem objetiva (ex.: checklist mínimo) | Checklist marcado |

---

## 9) Divisão automática (quando algo é “grande demais”)

### Critério v1 (único e explícito)

Uma micro-ação é “grande demais” quando:

- **estMinutes > 15** OU
- usuário clica **✂️ Dividir**

**Comportamento:**

- O sistema substitui por 3–4 micro-ações no molde: **listar → esboçar → preencher → revisar**.
- Cada uma com artefato próprio.

---

## 10) Run (timer/ritual — decisão v1)

### 10.1 O que é Run no v1

Run é um modo de foco com ritual fixo; o sistema faz prompts no fim do ciclo.

**Decisão v1:** Timer fixo por preset (não só “tempo decorrido”).

**Preset padrão (12–3–12):** 12 minutos de foco, 3 minutos de pausa, 12 minutos de foco (duas rodadas).

Ao fim de cada foco: prompt com 2 opções:

- *“Fechar este ciclo”* (vai para pausa ou Debrief se marcou Done)
- *“Continuar”* (inicia próximo foco)

**O Run termina quando:**

- usuário marca Done na micro-ação e chega ao prompt de fim de foco → vai para Debrief, ou
- usuário escolhe *“Encerrar Run agora”* (registrado como abortado).

### 10.2 Ações permitidas no Run

- ✅ Done  
- ✂️ Dividir  
- 🧊 Start Ridículo  
- 🛟 Rascunho feio (fallback universal)  
- ⛔ Bloquear  
- 💡 Capturar ideia (1 linha e volta)

### 10.3 Campos necessários no modelo

- runPresetId (ex.: “12-3-12”)
- completed (true/false)
- aborted (true/false)
- swapsCount, splitsCount  

*Run.cycles* removido no v1 (ou substituído por logs só se necessário depois).

---

## 11) Detecção de loop (limiares v1)

**Definição v1 de loop** (durante um único Run):

- **swapsCount ≥ 3** OU  
- **splitsCount ≥ 2** OU  
- **(swapsCount + splitsCount ≥ 4)** E nenhuma micro-ação concluída no Run  

**Intervenção por ambiente (sem bronca):**

- reduz opções visíveis (esconde “trocar” se existir)
- destaca “Rascunho feio” e “Start Ridículo”
- encurta próximo preset (ex.: 8–2–8) apenas para o próximo Run

---

## 12) Slider de ansiedade (regras v1)

| Faixa | estMinutes | Botões visíveis | Ênfase |
|--------|------------|------------------|--------|
| **0–3 (Normal)** | máximo: 15 | todos | concluir |
| **4–6 (Cautela)** | máximo recomendado: 10 (motor sugere dividir acima disso) | todos; destaca “Dividir” | concluir com mínimo |
| **7–10 (Fragil)** | micro-ações padrão: 5 min | ✅ Done, 🧊 Start Ridículo, 🛟 Rascunho feio, 💡 Capturar ideia (Dividir só após 1 conclusão ou via prompt “está grande?”) | iniciar e gerar artefato |

**Regra explícita na faixa 7–10 (Fragil):** Nesta faixa, toda nova micro-ação gerada (incluindo divisões sugeridas pelo sistema) deve ter **estMinutes ≤ 5**.

Após 1 Run concluído em 7–10, o app sugere “recalibrar” (1 clique).

---

## 13) Inbox de ideias (fluxo v1 explícito)

### 13.1 Capturar ideia

Durante o Run: *“Capturar ideia”* salva em IdeaInbox (texto curto) e retorna imediatamente ao Run. Não vira micro-ação automaticamente.

### 13.2 Quando a Inbox aparece

- Acessível pela Home e no Debrief.
- Não aparece como lista longa (mostrar no máximo 5 recentes).

### 13.3 Como uma ideia vira trabalho

**Regra v1:**

- Só é possível *“Promover”* uma ideia para nova missão quando a missão atual estiver **encerrada** ou **bloqueada**.
- Se promovida, o sistema cria uma missão nova com: outcome = ideia, compromisso mínimo pedido (5s), template escolhido.
- Isso preserva “uma missão” e evita inbox virar rota de fuga dentro da missão ativa.

---

## 14) Missão bloqueada (edge case definido)

- Se **status = Bloqueada**, o usuário **não inicia Run**.
- A Home mostra: *“Bloqueada: [motivo]”* e CTA único: *“Desbloquear: [unblockAction]”*.
- Ao executar a ação de desbloqueio, usuário marca *“Desbloqueei”* → missão volta a **Ativa**.

---

## 15) Encerramento e reabertura (cooldown)

- Ao atingir DoD mínimo, o sistema pergunta: *“Encerrar (mínimo) agora?”* / *“Continuar para Bom”*.
- Se encerrar: define **cooldownUntil = now + 24h**.
- **Reabrir antes do cooldown:** exige 1 frase *“por que reabrir?”*; cria automaticamente uma micro-ação mínima de retorno (artefato obrigatório).

---

## 16) “Próxima ação” (sem ambiguidade de “amanhã”)

**No v1**, “Próxima ação” significa sempre:

- a **primeira micro-ação pendente** da missão ativa (fila da missão).

Se a missão for encerrada:

- Home fica sem missão ativa até o usuário criar outra.
- A ideia de “próxima ação de amanhã fora da missão” fica **fora do v1** para evitar ambiguidade.

---

## 17) Persistência e offline (não funcional — escopo v1)

**Decisão v1:** local-first + offline (PWA).

- Dados persistem no dispositivo (ex.: IndexedDB / local DB).
- Export/import simples opcional (se quiser backup).
- Sync multi-dispositivo fica **fora do v1** (explicitamente).

---

## 18) Modelo de dados (ajustes finais)

- **DoDLevel.criteria[]** (e dodMin, dodGood, dodPremium): checklist `[{ text: string, done: boolean }]`.
- **MicroAction.estMinutes** é fonte da verdade para “grande demais”.
- **Run** inclui: runPresetId, completed, aborted, swapsCount, splitsCount.
- **Run.cycles** removido no v1 (ou definido só se necessário com log de segmentos).

---

## 19) Critérios de “feito” do produto (mínimo testável v1)

O v1 está pronto quando um usuário consegue:

1. Criar missão (com compromisso mínimo)
2. Gerar micro-ações via template (com artefatos)
3. Iniciar Run (preset fixo)
4. Concluir pelo menos 1 micro-ação (Done)
5. Ver Debrief com próxima ação
6. Encerrar missão no DoD mínimo e ver cooldown

---

## 20) Métricas (ligadas ao valor)

- **Run completion rate:** “runs concluídos” = runs em que o usuário chegou ao Debrief; “runs iniciados” incluem runs concluídos e abortados (abortados entram no denominador, não no numerador).
- **Time to first win**
- **Mission closure rate**
- **swaps/splits por run** (loop)
- **reaberturas dentro do cooldown**

---
