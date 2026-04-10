---
name: learn-quiz
description: Quiz mode for /learn — standalone (5 questions) or reinforcement (3 questions post-exercise), calibrated to detected user level
---

# Learn Quiz

You are running the Claude Code quiz. Follow these instructions exactly.

## Mode Detection

You will be invoked in one of two modes:

- **Standalone**: Called from `SKILL.md` after silent diagnosis → 5 questions calibrated to detected level
- **Reinforcement**: Called from `learn-exercise.md` after an exercise → 3 questions about the concept just practiced

The invoking skill will pass the mode and relevant context (level + topic if reinforcement).

## Question Design Principles

- **75%+ Apply level** — questions present scenarios, not just definitions. "You want X. What do you do?" not "What is X?"
- **Balanced answer positions** — correct answers distributed across A, B, C, D to prevent pattern-guessing
- **Full explanations** — each answer explains why the correct option works AND why each distractor fails

---

## Standalone Mode (5 questions)

### Question Banks by Level

#### Iniciante (0–3 points from diagnosis)

1. **Você abre uma sessão do Claude Code e percebe que ele responde em inglês, mesmo você preferindo português. Como resolver permanentemente?**
   - A) Digitar "sempre responda em português" no início de cada sessão
   - B) Alterar o idioma do sistema operacional
   - C) Adicionar a regra em `~/.claude/CLAUDE.md` — carregado automaticamente no início de toda sessão
   - D) Configurar o idioma no painel da conta Claude
   - **Answer: C** — CLAUDE.md global é lido em toda sessão automaticamente. **Por que A falha:** ter que digitar toda sessão é exatamente o problema a resolver. **Por que B falha:** idioma do OS não afeta o comportamento da CLI. **Por que D falha:** configurações de conta não controlam idioma de resposta no terminal.

2. **O que é uma skill no Claude Code?**
   - A) Um arquivo markdown com frontmatter YAML que dá ao Claude instruções especializadas, invocado com `/nome-da-skill`
   - B) Um script Python que estende as capacidades do modelo
   - C) Um modelo fine-tuned para um domínio específico
   - D) Uma extensão de browser que adiciona funcionalidades ao Claude Code
   - **Answer: A** — Skills são arquivos `.md` com frontmatter YAML em `~/.claude/skills/`. Claude os lê quando você invoca `/nome-da-skill`. **Por que B falha:** não é Python, é markdown. **Por que C falha:** não é fine-tuning — é instrução em texto. **Por que D falha:** Claude Code é uma CLI, não um browser.

3. **Você quer que o Claude não use comentários óbvios no código, mas apenas em um projeto específico, não globalmente. Onde colocar essa regra?**
   - A) `~/.claude/CLAUDE.md` — aplica a todos os projetos
   - B) `~/CLAUDE.md` no diretório home
   - C) Em um arquivo `.env` no projeto
   - D) `.claude/CLAUDE.md` dentro do diretório do projeto
   - **Answer: D** — Project-level CLAUDE.md só é carregado quando você trabalha naquele diretório. **Por que A falha:** escopo global — afetaria todos os projetos. **Por que B falha:** Claude não lê CLAUDE.md solto na home. **Por que C falha:** `.env` é para variáveis de ambiente, não instruções do Claude.

4. **Um colega quer que o Claude use sempre Conventional Commits. O que você recomenda como solução permanente?**
   - A) Enviar a ele um script bash que valida commits antes do push
   - B) Adicionar uma regra de formato de commit em `~/.claude/CLAUDE.md` dele
   - C) Instalar um linter de commits globalmente no sistema
   - D) Claude não consegue seguir padrões de commit automaticamente
   - **Answer: B** — Regras de workflow e formato vão no CLAUDE.md — Claude as segue em toda sessão sem repetição. **Por que A falha:** script resolve o sintoma, não ensina o Claude. **Por que C falha:** linter exige config por projeto e não muda o comportamento do Claude. **Por que D falha:** CLAUDE.md resolve exatamente isso.

5. **Você instala uma skill e invoca com `/minha-skill` mas recebe "unknown skill". Qual é a causa mais provável?**
   - A) Skills precisam ser ativadas nas configurações do Claude
   - B) Skills só funcionam com Claude Code pago
   - C) O arquivo da skill não está em `~/.claude/skills/` ou o campo `name` no frontmatter não corresponde ao que você invocou
   - D) É necessário reiniciar o terminal para skills serem reconhecidas
   - **Answer: C** — Claude Code lê skills de `~/.claude/skills/`. Se o arquivo não está lá, ou o `name` no frontmatter é diferente, a skill não é encontrada. **Por que A falha:** não há processo de ativação. **Por que B falha:** skills funcionam em qualquer plano. **Por que D falha:** não é necessário reiniciar.

---

#### Intermediário (4–6 points from diagnosis)

1. **Você quer receber uma notificação no celular toda vez que o Claude terminar uma tarefa longa. Qual hook e evento usar?**
   - A) `PreToolUse` com um `command` que verifica se a resposta vai ser longa
   - B) `Stop` com um `command` que envia push notification via CLI (ex: `ntfy`, `osascript`)
   - C) `SessionStart` com webhook que monitora duração da sessão
   - D) `PostToolUse` com polling para detectar quando o Claude para de usar ferramentas
   - **Answer: B** — `Stop` dispara exatamente quando o Claude termina a resposta — evento correto para "tarefa concluída". **Por que A falha:** `PreToolUse` dispara antes do uso de ferramenta, não no término. **Por que C falha:** `SessionStart` dispara no início da sessão. **Por que D falha:** `PostToolUse` dispara após cada tool call individual, não ao término da resposta completa.

2. **Qual é a diferença fundamental entre um hook `type: command` e `type: prompt`?**
   - A) `command` é mais rápido; `prompt` é mais preciso
   - B) `command` funciona no macOS; `prompt` é cross-platform
   - C) `command` executa antes do tool use; `prompt` executa depois
   - D) `command` executa um processo externo no shell; `prompt` injeta texto no contexto do Claude para que ele raciocine antes de agir
   - **Answer: D** — Essa é a distinção central: `command` = processo externo, `prompt` = raciocínio do LLM. **Por que A falha:** diferença de velocidade não é a característica definidora. **Por que B falha:** ambos funcionam cross-platform. **Por que C falha:** ambos podem ser configurados em qualquer evento, inclusive `PreToolUse`.

3. **Sua equipe tem 5 devs. Você quer compartilhar regras do Claude Code específicas do projeto via git. O que commitar?**
   - A) `.claude/CLAUDE.md` na raiz do projeto — escopo de projeto, rastreável pelo git
   - B) `~/.claude/CLAUDE.md` — compartilha as configurações globais de todos
   - C) `~/.claude/settings.json` — compartilha hooks e configurações pessoais
   - D) Um arquivo `claude.config.js` na raiz do projeto
   - **Answer: A** — Project-level CLAUDE.md vive no repo, é rastreável pelo git e só aplica naquele projeto. **Por que B falha:** `~/.claude/` é pessoal/local — errado compartilhar. **Por que C falha:** settings.json contém hooks e chaves pessoais — não deve ser versionado. **Por que D falha:** `claude.config.js` não é um formato reconhecido pelo Claude Code.

4. **Um hook `PreToolUse` com matcher `Bash` roda um script de segurança. O script detecta `rm -rf /` e faz `exit 1`. O que acontece?**
   - A) O Claude Code executa o comando mesmo assim, mas registra um aviso
   - B) O Claude pede confirmação ao usuário antes de continuar
   - C) O tool use é bloqueado e o stdout/stderr do script é exibido ao Claude como razão do bloqueio
   - D) O Claude desativa todos os hooks pelo resto da sessão
   - **Answer: C** — `exit 1` de um hook `PreToolUse` bloqueia o tool use e retorna a saída do script como razão. **Por que A falha:** `exit 1` é projetado especificamente para bloquear, não apenas avisar. **Por que B falha:** confirmação de usuário é comportamento de permission prompt, não de hook. **Por que D falha:** um hook bloqueado não afeta os outros.

5. **Você quer uma skill disponível apenas no projeto atual, não globalmente. Onde criar o arquivo?**
   - A) `~/.claude/skills/nome-do-projeto/` — subpasta com nome do projeto
   - B) `.claude/skills/` dentro do diretório do projeto
   - C) `~/.config/claude/skills/`
   - D) Skills globais e de projeto usam o mesmo diretório; você diferencia pelo frontmatter
   - **Answer: B** — Skills em `.claude/skills/` dentro do diretório do projeto só ficam disponíveis naquele projeto. **Por que A falha:** subpastas em `~/.claude/skills/` não criam escopo de projeto — ainda são globais. **Por que C falha:** Claude Code não lê skills de `~/.config/`. **Por que D falha:** são diretórios diferentes, não frontmatter diferente.

---

#### Avançado (7–9 points from diagnosis)

1. **Você projeta um sistema multi-agente para analisar um repo: Agente A (arquitetura), B (segurança), C (testes). O que cada agente deve receber?**
   - A) O histórico completo da conversa pai para ver todas as decisões anteriores
   - B) Acesso irrestrito a todos os arquivos do repositório
   - C) Apenas os arquivos e instruções relevantes para sua análise — nada além disso
   - D) Os resultados dos outros agentes antes de começar sua análise
   - **Answer: C** — Contexto mínimo e preciso: subagentes não devem receber ruído de trabalho não relacionado. **Por que A falha:** histórico completo = ruído de conversas anteriores irrelevantes. **Por que B falha:** acesso irrestrito desperdiça contexto e confunde o agente. **Por que D falha:** contaminar com resultados alheios antes da análise derrota o isolamento.

2. **Seu CLAUDE.md global tem 500 linhas e o Claude ignora algumas regras do meio do arquivo. O que fazer?**
   - A) Dividir em CLAUDE.md global (<100 linhas, regras universais) + `.claude/CLAUDE.md` por projeto (contexto específico)
   - B) Aumentar o context window em settings.json
   - C) Mover todas as regras para um arquivo de skill
   - D) Formatar cada regra em negrito para se destacar
   - **Answer: A** — Dividir por escopo mantém cada arquivo focado e curto — Claude segue arquivos estruturados e curtos com mais confiabilidade. **Por que B falha:** context window não melhora instruction following de um arquivo sobrecarregado. **Por que C falha:** skills são para tarefas, não para regras comportamentais persistentes. **Por que D falha:** formatação não compensa volume excessivo.

3. **Você quer que o Claude verifique se cada Bash é reversível antes de executar, sem rodar script externo. Qual abordagem?**
   - A) Hook `Stop` com shell script que analisa o último comando executado
   - B) Script Python que intercepta stdin antes do Claude receber
   - C) Configurar `"permissions": { "bash": "ask" }` em settings.json
   - D) Hook `PreToolUse` com `type: prompt` instruindo o Claude a avaliar reversibilidade antes de prosseguir
   - **Answer: D** — Prompt-type hooks injetam raciocínio no contexto do Claude antes do tool rodar — sem processo externo. **Por que A falha:** `Stop` dispara após conclusão, não antes. **Por que B falha:** interceptar stdin não é como hooks do Claude Code funcionam. **Por que C falha:** `ask` em permissions pede confirmação ao usuário, não raciocínio do Claude.

4. **Em um workflow pai + subagentes, o pai recebe resultados de 3 subagentes e precisa sintetizar. Qual é o constraint crítico?**
   - A) Cada subagente deve rodar sequencialmente para evitar conflitos
   - B) O prompt de síntese do pai deve incluir todos os outputs explicitamente — o pai não tem memória de ter despachado os subagentes
   - C) Subagentes compartilham automaticamente o context window do pai
   - D) O pai deve re-rodar subagentes com falha antes de sintetizar
   - **Answer: B** — Cada chamada de `Agent` começa do zero — o pai deve incluir explicitamente todos os outputs no contexto de síntese. **Por que A falha:** subagentes devem rodar em paralelo. **Por que C falha:** contextos são isolados, nada é compartilhado. **Por que D falha:** síntese acontece com tratamento adequado de falhas, sem obrigação de re-run.

5. **Seu hook `PostToolUse` detecta 80% de contexto usado e injeta um aviso. O Claude continua sem reagir. Causa e solução?**
   - A) O hook não está disparando — verificar o nome do evento em settings.json
   - B) Claude ignora hooks `PostToolUse` por design
   - C) O aviso é injetado mas deprioritizado mid-task; adicionar hook `PreCompact` com `type: prompt` para forçar revisão antes da compressão
   - D) Reduzir o threshold para 50% para dar mais tempo de reação
   - **Answer: C** — Avisos mid-task são frequentemente depriorizados; `PreCompact` é o momento certo para forçar gestão de contexto. **Por que A falha:** se outros PostToolUse hooks funcionam, o evento dispara normalmente. **Por que B falha:** `PostToolUse` injeta `additionalContext` corretamente. **Por que D falha:** mudar threshold não resolve o Claude depriorizá-lo.

---

## Reinforcement Mode (3 questions post-exercise)

Based on the topic practiced, select 3 relevant questions:

### After CLAUDE.md exercise
- Use Iniciante Q3, Q4, and Intermediário Q3

### After hooks exercise (Intermediário)
- Use Intermediário Q1, Q4, and ask: **"Qual evento você usaria para rodar um script antes de cada ferramenta Bash?"** (Answer: `PreToolUse` com matcher `Bash`)

### After hooks avançados exercise (frontier)
- Use Intermediário Q2, Q4, then ask: **"Por que usar `type: prompt` em vez de `type: command` para revisar comandos Bash?"** (Answer: `prompt` não roda processo externo — o Claude raciocina diretamente, sem latência de shell e entendendo o contexto completo)

### After skills exercise
- Use Iniciante Q2, Q5, and ask: **"Quais campos de frontmatter são obrigatórios em todo arquivo de skill?"** (Answer: `name` e `description`)

### After commits exercise
- Use Iniciante Q4, then ask: **"Qual prefixo de tipo usar para um bug fix em Conventional Commits?"** (Answer: `fix`), then: **"Qual a regra do modo imperativo?"** (Answer: "add", não "added" ou "adds")

### After agents exercise (Intermediário/Avançado)
- Use Avançado Q1, Q4, and ask: **"Por que subagentes devem receber contexto mínimo e não o histórico completo?"** (Answer: contexto mínimo mantém o agente focado na subtarefa, evita confusão com informações irrelevantes e economiza tokens)

### After commits avançado exercise (frontier)
- Use Iniciante Q4, then ask: **"Em qual evento de hook você interceptaria um `git commit` para validar a mensagem?"** (Answer: `PreToolUse` com matcher `Bash`), then: **"Por que `type: prompt` é melhor que `type: command` para validar commits?"** (Answer: `prompt` entende contexto e pode sugerir correção; `command` apenas bloqueia ou passa)

### After context exercise (frontier)
- Use Avançado Q5, then ask: **"Qual hook é o momento ideal para salvar decisões críticas antes de uma compactação?"** (Answer: `PreCompact` com `type: prompt`), then ask:

**"Você precisa rodar uma análise pesada em um repositório grande usando Claude Code. São 14h BRT de uma terça-feira. O que fazer?"**
- A) Rodar agora — a análise vai funcionar normalmente em qualquer horário
- B) Esperar até depois das 16h BRT para evitar o peak hours e preservar mais da janela de 5 horas
- C) Dividir em subagentes para contornar o limite
- D) Atualizar para o plano Max — isso remove o peak hours penalty

**Answer: B** — Das 10h às 16h BRT (5am–11am PT) nos dias úteis, você consome a janela de 5 horas mais rápido. Esperar até depois das 16h preserva mais da janela para tarefas intensivas. **Por que A falha:** o horário importa — ~7% dos usuários Pro atingem limites que não atingiriam fora do peak. **Por que C falha:** subagentes consomem da mesma janela, não contornam o limite. **Por que D falha:** todos os planos (Free, Pro e Max) são afetados pelo peak hours.

---

## Quiz Delivery Format

Present each question as:

```
**Pergunta N de N**

[Texto da pergunta]

A) [Opção]
B) [Opção]
C) [Opção]
D) [Opção]
```

After the user answers:
- If correct: `Correto! [Explicação — por que a resposta certa funciona e por que as outras falham]`
- If incorrect: `Não foi dessa vez. A resposta é [X]. [Explicação completa]`

After all questions, show:
```
Quiz completo: N/N corretas

[Se score < 60%]: Vale revisitar esses tópicos. Tente /learn <tópico> para praticar hands-on.
[Se score 60-80%]: Boa base! Alguns gaps para preencher — revise as áreas mais fracas.
[Se score > 80%]: Conhecimento sólido. Você está pronto para o próximo nível.
```

If reinforcement mode, add:
```
Quer continuar aprendendo? Use /learn path para ver seu roadmap completo.
```
