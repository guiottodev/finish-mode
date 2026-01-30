# Glossário — Finish Mode (v1.0)

> Objetivo: padronizar linguagem do produto e evitar interpretações diferentes na implementação e no copy.  
> Regra: se um termo mudar no PRD, atualize aqui no mesmo PR.

---

## Missão
**Definição (v1.0):** Contêiner de fechamento. Representa algo que precisa ser **encerrado** (não é uma tarefa isolada).  
**Campos típicos:** `title`, `outcome`, `minCommitment`, `dodMin/dodGood/dodPremium`, `microActions[]`, `status`.  
**Exemplo:** “Finalizar onboarding do Finish Mode”.

**Notas/TODO (se quiser ajustar):**
- [ ] Como você quer descrever “Missão” em uma frase para usuário final?

---

## Compromisso mínimo (Min Commitment)
**Definição (v1.0):** “O menor resultado que você aceita entregar” antes da missão ficar ativa (contrato psicológico).  
**Para que serve:** ancorar o DoD mínimo e reduzir abandono/reinterpretação do “feito”.  
**Exemplo:** “Ter o fluxo principal rodando com 1 run concluído.”

**Notas/TODO:**
- [ ] Qual frase padrão o app sugere aqui?

---

## DoD — Definition of Done (Mínimo / Bom / Premium)
**Definição (v1.0):** Critério de “feito” da missão em 3 níveis.  
- **Mínimo:** aceitável, pode estar feio, mas entrega valor (**obrigatório para encerrar**)  
- **Bom:** padrão esperado (opcional após mínimo)  
- **Premium:** polimento extra (opcional após bom)  
**Formato recomendado:** checklist `[{ text, done }]`.

**Notas/TODO:**
- [ ] Exemplos de DoD mínimo que você mais usaria (1–3)?

---

## Micro-ação
**Definição (v1.0):** Unidade real de trabalho dentro da missão. Sempre concreta (verbo + objeto).  
**Regras:**  
- 5–15 min (`estMinutes`)  
- estado claro (todo/doing/done)  
- **sempre tem Artefato**

**Exemplo:** “Escrever um rascunho feio do README (5 min).”

**Notas/TODO:**
- [ ] Como você quer nomear “Micro-ação” na UI? (micro-ação / passo / ação)

---

## Artefato
**Definição (v1.0):** Algo concreto que passa a existir quando a micro-ação termina.  
**Regra:** nenhuma micro-ação pode existir sem artefato.  
**Exemplos:** “rascunho salvo”, “checklist marcado”, “comentário criado”, “arquivo criado”.

**Notas/TODO:**
- [ ] Exemplos de artefatos por template (Doc/QA/Polimento)?

---

## Run (sessão ritual de foco)
**Definição (v1.0):** Modo fechado de execução (não é só timer). Durante o Run, o usuário vê poucas opções e executa a micro-ação atual.  
**Preset padrão:** **12–3–12** (12 min foco, 3 min pausa, 12 min foco).  
**Ações típicas no Run:** Done, Dividir, Start Ridículo, Rascunho feio, Bloquear, Capturar ideia.

**Notas/TODO:**
- [ ] Você quer manter o nome “Run” na UI ou traduzir? (Run / Sessão / Modo foco)

---

## Preset (do Run)
**Definição (v1.0):** Configuração do ritual de foco (ex.: 12–3–12).  
**Para que serve:** tornar o início previsível e reduzir decisão.

**Exemplos:**  
- 12–3–12 (padrão)  
- (Opcional futuro) 8–2–8, 25–5–25

---

## Template
**Definição (v1.0):** Sequência padrão de micro-ações para um tipo recorrente de fechamento (documentar, revisar, QA…).  
**Regra v1.0:** template é **sequência fixa**, com artefatos típicos.

**Templates v1.0 (mínimos):**
- Documentação (usuário / técnica)
- Polimento (UI / texto / regras)
- Revisão (consistência / edge cases)
- QA (smoke / regressão curta)
- Entrega (confirmar envio/publicação)

---

## Start Ridículo
**Definição (v1.0):** Mecanismo anti-trava que reduz a ação para algo quase impossível de falhar (iniciar > terminar).  
**Exemplos:** “abrir o arquivo”, “colocar placeholder”, “escrever 1 bullet ruim”.

---

## Rascunho feio (Fallback universal)
**Definição (v1.0):** Airbag do sistema: cria uma micro-ação automática de 5 min para gerar um artefato “feio, mas existente”.  
**Objetivo:** quebrar travamento mesmo quando template falha.

---

## Clareza em 30 segundos
**Definição (v1.0):** Mini-diagnóstico (1 pergunta) que mapeia travamento → resposta do sistema.  
**Travamentos (v1.0):**
- não sei por onde começar
- está grande demais
- quero perfeito
- depende de alguém
- não sei se está bom

**Resposta do sistema:** cria micro-ação mínima / propõe dividir / bloqueia com ação / checklist objetivo.

---

## Bloqueada (Missão bloqueada)
**Definição (v1.0):** Estado da missão quando depende de algo externo.  
**Campos:** `blockedReason` + `unblockAction`.  
**Regra v1.0:** missão bloqueada **não inicia Run**; Home mostra a ação de desbloqueio.

---

## Pausa curta
**Definição (v1.0):** Pausa consciente do trabalho na missão atual.  
**Regra v1.0:** pausa curta **não libera outra missão** (continua existindo só uma missão não-encerrada).

---

## Loop (fuga sofisticada)
**Definição (v1.0):** Padrão de troca/divisão sem conclusão dentro de um Run (ou repetido).  
**Sinais:** `swapsCount`, `splitsCount`, ausência de “Done”.  
**Intervenção:** reduzir opções + sugerir Start Ridículo / Rascunho feio.

---

## Ansiedade (controle de dificuldade)
**Definição (v1.0):** Slider 0–10 que ajusta o tamanho das micro-ações e a quantidade de opções no Run.  
**Regra v1.0 (faixa 7–10):** novas micro-ações/divisões com `estMinutes ≤ 5`.

---

## Debrief
**Definição (v1.0):** Tela/etapa de fechamento do Run.  
**Mostra:** o que foi feito, progresso, e a “próxima micro-ação” pronta (ou opção de encerrar missão se DoD mínimo atingido).

---

## Cooldown (reabertura com fricção)
**Definição (v1.0):** Janela após encerrar uma missão (ex.: 24h) para evitar reabrir por culpa.  
**Regra v1.0:** reabrir antes do cooldown exige 1 frase de motivo + gera micro-ação mínima.

---

## Histórico de finais
**Definição (v1.0):** Histórico que mostra apenas **missões encerradas** (não lista de tarefas).  
**Objetivo:** reforçar identidade “eu termino”.

---

## Inbox de ideias
**Definição (v1.0):** Caixa de captura rápida (1 linha) para não interromper o Run.  
**Regra v1.0:** ideia não vira micro-ação automaticamente; só pode ser promovida quando missão estiver encerrada/bloqueada.

---

# TODO: Termos extras (se você quiser adicionar)
- [ ] “Home”
- [ ] “Uma missão por vez” (invariante)
- [ ] “Artefato mínimo”
- [ ] “Checklist DoD (formato e exemplos)”
