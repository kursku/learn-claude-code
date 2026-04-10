---
name: learn-exercise
description: Delivers a personalized Claude Code exercise based on user level (Iniciante/Intermediário/Avançado) or a specific topic. Runs the exercise live in the session, then offers learn-path and learn-quiz.
---

# Claude Code Exercise Delivery

You receive a level (Iniciante, Intermediário, or Avançado) and optionally a topic. Deliver the right exercise.

## Roteamento Nível × Tópico

Se um tópico foi passado junto com o nível, use esta tabela para escolher a seção correta:

| Tópico | Iniciante ou Intermediário | Avançado |
|--------|---------------------------|----------|
| `hooks` | → Seção Intermediário | → Seção Frontier: Hooks Avançados |
| `agents` | → Seção Intermediário (opção skill) | → Seção Avançado (multi-agent) |
| `skills` | → Seção Intermediário (opção skill) | → Seção Frontier: Publicar skill |
| `commits` | → Seção Iniciante (commit guiado) | → Seção Frontier: Commits Avançados |
| `claude-md` | → Seção Iniciante | → Seção Avançado (audit CLAUDE.md) |
| `context` | → Seção Frontier: Gestão de Contexto | → Seção Frontier: Gestão de Contexto |

Se nenhum tópico foi passado, use o nível para escolher o Quick Win Menu padrão abaixo.

## Quick Win Menu

Present exactly 3 options for the detected level. Let the user pick one.

### Se level = Iniciante (ou topic = claude-md)

> **Como funciona:** O Claude Code lê arquivos `CLAUDE.md` automaticamente no início de cada sessão. Isso significa que você pode ensinar o Claude a se comportar do jeito que você prefere — sem precisar repetir instruções toda vez. É como uma memória persistente entre sessões.

```
Vamos começar com um quick win! Escolha um exercício:

a) Criar seu primeiro CLAUDE.md — 3 regras que vão mudar como o Claude trabalha com você
b) Fazer seu primeiro commit guiado — vou te guiar pelo processo completo
c) Entender um arquivo do seu projeto — me diga um arquivo e vou explicar tudo
```

**Se escolher (a) — CLAUDE.md:**
1. Pergunte ao usuário: "Quais são 3 coisas que te incomodam quando você trabalha com IA?"
2. Transforme as respostas em regras no formato correto:
   ```markdown
   # Minhas preferências
   - [regra derivada da resposta 1]
   - [regra derivada da resposta 2]
   - [regra derivada da resposta 3]
   ```
3. Escreva o arquivo em `~/.claude/CLAUDE.md` usando a ferramenta Write
4. Mostre o resultado e explique: "Agora toda vez que você abrir o Claude Code, essas regras são carregadas automaticamente."
5. ✓ Micro-check: confirme com o usuário — "Essas 3 regras representam bem suas preferências? Podemos ajustar antes de salvar."

**Se escolher (b) — Commit:**
Invoque a skill `commit` se disponível, ou guie manualmente:
1. `git status` para ver o que está pendente
2. Explique o que cada arquivo modificado faz
3. Sugira uma mensagem de commit no formato Conventional Commits
4. Execute com confirmação do usuário

**Se escolher (c) — Explicar arquivo:**
1. Peça o caminho do arquivo
2. Leia o arquivo
3. Explique: o que faz, por que existe, como se encaixa no projeto

---

### Se level = Intermediário (ou topic = hooks para Iniciante/Intermediário)

> **Como funciona:** Hooks são comandos que o Claude Code executa automaticamente em eventos específicos da sessão — antes de usar uma ferramenta, ao terminar uma resposta, ao compactar contexto. Você configura uma vez em `~/.claude/settings.json` e ele roda em toda sessão sem você precisar lembrar.

```
Você já tem o básico. Hora de desbloquear automações! Escolha:

a) Configurar seu primeiro hook — o Claude te avisa quando termina uma tarefa
b) Criar uma skill personalizada — ensine o Claude a seguir seu próprio processo
c) Configurar um CLAUDE.md de projeto — regras específicas para este repositório
```

**Se escolher (a) — Hook:**
1. Explique: "Hooks são comandos que rodam automaticamente em eventos do Claude Code. Vamos adicionar uma notificação quando o Claude termina."
2. Mostre o JSON que será adicionado:
   ```json
   {
     "hooks": {
       "Stop": [{
         "matcher": "",
         "hooks": [{
           "type": "command",
           "command": "echo 'Claude terminou!' | powershell -Command \"[System.Windows.MessageBox]::Show('Claude terminou!')\" 2>/dev/null || osascript -e 'display notification \"Claude terminou!\"' 2>/dev/null || notify-send 'Claude terminou!' 2>/dev/null || true",
           "timeout": 5
         }]
       }]
     }
   }
   ```
3. ✓ Micro-check: "Faz sentido? O evento `Stop` dispara quando o Claude termina qualquer resposta — exatamente o que queremos."
4. Leia `~/.claude/settings.json`, faça merge do hook, escreva o arquivo
5. Confirme: "Hook adicionado. Na próxima vez que o Claude terminar uma resposta, você receberá uma notificação."

**Se escolher (b) — Skill:**
Invoque a skill `write-a-skill` se disponível, ou guie:
1. Pergunte: "Qual processo você repete muito que o Claude poderia automatizar?"
2. Crie um arquivo `.md` simples em `~/.claude/skills/` com frontmatter + instruções

**Se escolher (c) — Project CLAUDE.md:**
1. Crie `.claude/CLAUDE.md` no diretório atual
2. Adicione regras específicas do projeto (linguagem, padrões de commit, arquivos a ignorar)

---

### Intermediário × agents (Intermediário + topic = agents)

> **Como funciona:** Subagentes são instâncias isoladas do Claude que você dispara em paralelo via ferramenta `Agent` (Task). Cada um recebe apenas o contexto necessário para sua subtarefa — isso evita que o modelo se confunda com informações de outras tarefas e economiza tokens.

```
Você já usa o Claude. Hora de multiplicar sua capacidade! Escolha:

a) Entender subagentes — o que são e quando usar
b) Sua primeira tarefa paralela — pesquisa simultânea com 2 agentes
c) Padrão de orquestração — como estruturar um agente pai e filhos
```

**Se escolher (a) — O que são subagentes:**
1. Explique: "Subagentes são instâncias separadas do Claude, cada uma com contexto isolado. Você as dispara com a ferramenta `Agent` (Task) e cada uma executa uma subtarefa independente."
2. Mostre a diferença entre rodar tudo em uma sessão vs. delegar para agentes:
   - Uma sessão: contexto cresce, risco de confusão entre tarefas
   - Subagentes: cada agente foca apenas no que precisa saber
3. Casos de uso ideais: pesquisa paralela, revisão de código, geração de testes

**Se escolher (b) — Primeira tarefa paralela:**
1. Proponha um exemplo concreto: "Pesquise dois frameworks para mim ao mesmo tempo"
2. Mostre como estruturar o prompt para cada agente com contexto mínimo
3. Explique como o agente pai recebe os resultados e os consolida

**Se escolher (c) — Padrão de orquestração:**
1. Explique o padrão: agente orquestrador recebe a tarefa → decompõe em subtarefas → dispatcha agentes especializados → consolida resultados
2. Mostre um exemplo de decomposição real (ex: "Analise este repositório" → agente de arquitetura + agente de segurança + agente de testes)
3. Ofereça criar uma skill para este workflow

---

### Se level = Avançado (ou topic = agents)

> **Como funciona:** Usuários avançados já têm CLAUDE.md, hooks e skills configurados. O próximo salto é otimizar o que existe — revisar se as regras são específicas e acionáveis, identificar gaps nos hooks, e escalar com workflows multi-agente para tarefas complexas.

```
Você já domina o básico. Vamos otimizar! Escolha:

a) Revisar e melhorar seu CLAUDE.md — auditoria de boas práticas
b) Desenhar um workflow multi-agente — para uma tarefa real sua
c) Auditar seus hooks — identificar gaps e melhorias
```

**Se escolher (a) — Audit CLAUDE.md:**
1. Leia `~/.claude/CLAUDE.md`
2. Avalie contra estas boas práticas:
   - Regras são específicas e acionáveis (não vagas como "seja preciso")?
   - Tem seção de workflow de git?
   - Tem instruções de estilo de código?
   - Tem restrições de segurança (ex: nunca faça deploy sem confirmar)?
3. Sugira melhorias concretas e aplique com aprovação do usuário

**Se escolher (b) — Multi-agent:**
1. Pergunte: "Descreva uma tarefa complexa que você faz regularmente"
2. Decomponha em subtarefas paralelas
3. Mostre como chamar múltiplos agentes via `Task` tool
4. Ofereça criar um skill para esse workflow

**Se escolher (c) — Audit hooks:**
1. Leia `~/.claude/settings.json`
2. Liste hooks existentes por evento
3. Avalie:
   - Todos os hooks são do tipo `command`? Sugira evoluir para `prompt` ou `agent` nos casos adequados
   - Há duplicatas (mesmo matcher, mesmo comando)?
   - Eventos descobertos sem hook: `PreToolUse Bash` (segurança), `PreCompact` (salvar contexto)
4. Sugira melhorias com JSON concreto e aplique com aprovação do usuário

---

### Frontier — Hooks Avançados (Avançado + topic = hooks)

```
Você já domina hooks command. Hora de evoluir para o próximo nível! Escolha:

a) Hook tipo `prompt` no PreToolUse — Claude revisa o próprio Bash antes de executar
b) Hook tipo `prompt` no PreCompact — Claude salva decisões críticas antes de compactar
c) Auditar hooks existentes — detectar duplicatas, gaps e oportunidades de upgrade para prompt/agent
```

**Se escolher (a) — PreToolUse prompt:**
1. Explique: "Um hook tipo `prompt` injeta instrução no contexto do Claude antes da ação. É diferente de `command` — não roda um processo, faz o Claude raciocinar."
2. Mostre o JSON:
   ```json
   {
     "PreToolUse": [{
       "matcher": "Bash",
       "hooks": [{
         "type": "prompt",
         "prompt": "Antes de executar este comando Bash, verifique: (1) é reversível? (2) pode afetar dados fora do projeto atual? (3) risco de deleção em massa? Se sim para qualquer um, explique o risco e peça confirmação explícita do usuário."
       }]
     }]
   }
   ```
3. Leia `~/.claude/settings.json`, faça merge do hook, escreva o arquivo
4. Explique o resultado: "Agora o Claude raciocina sobre segurança antes de qualquer Bash — sem processo externo, sem latência de shell."

**Se escolher (b) — PreCompact prompt:**
1. Explique: "Quando o contexto está cheio, o Claude compacta a conversa. Um hook `prompt` aqui garante que informações críticas sejam preservadas."
2. Mostre o JSON:
   ```json
   {
     "PreCompact": [{
       "matcher": "",
       "hooks": [{
         "type": "prompt",
         "prompt": "Antes de compactar, salve explicitamente: (1) decisões de arquitetura tomadas nesta sessão, (2) arquivos modificados e por quê, (3) próximos passos pendentes. Inclua isso no resumo de compactação."
       }]
     }]
   }
   ```
3. Leia `~/.claude/settings.json`, faça merge, escreva o arquivo

**Se escolher (c) — Audit completo:**
1. Leia `~/.claude/settings.json`
2. Para cada hook, identifique: tipo atual, evento, se há duplicata
3. Sugira upgrades onde `prompt` faria mais sentido que `command`
4. Mostre diff de mudanças e aplique com aprovação

---

### Frontier — Commits Avançados (Avançado + topic = commits)

```
Você já faz commits. Hora de profissionalizar o fluxo! Escolha:

a) Criar um hook PreToolUse para validar mensagens de commit antes de executar
b) Configurar git aliases + commitlint para padronizar o time
c) Auditar seu histórico de commits — identificar inconsistências e corrigi-las
```

**Se escolher (a) — Hook de validação:**
1. Explique: "Um hook `prompt` no `PreToolUse` para o tool `Bash` pode interceptar comandos `git commit` e validar o formato antes de executar."
2. Mostre o JSON:
   ```json
   {
     "PreToolUse": [{
       "matcher": "Bash",
       "hooks": [{
         "type": "prompt",
         "prompt": "Se o comando contém 'git commit', verifique se a mensagem segue o formato Conventional Commits (type(scope): description). Se não seguir, avise o usuário e sugira a mensagem corrigida antes de prosseguir."
       }]
     }]
   }
   ```
3. Aplique com aprovação e mostre como testar

**Se escolher (b) — Aliases + commitlint:**
1. Mostre aliases úteis para `.gitconfig`
2. Guie instalação do commitlint para o projeto atual
3. Crie um `.commitlintrc.json` com as regras do projeto

**Se escolher (c) — Audit de histórico:**
1. Rode `git log --oneline -20` para ver os últimos commits
2. Identifique commits que não seguem Conventional Commits
3. Explique como usar `git rebase -i` para reorganizar se necessário (com aviso de risco)

---

### Frontier — Publicar Skill (Avançado + topic = skills)

```
Você já usa skills. Hora de criar e publicar uma sua! Escolha:

a) Criar uma skill para um processo que você repete — e publicar no GitHub
b) Evoluir uma skill existente — adicionar sub-skills ou lógica de roteamento
c) Criar um skill pack — agrupe skills relacionadas em um repositório
```

**Se escolher (a) — Nova skill pública:**
1. Pergunte: "Qual processo você repete que poderia virar uma skill para a comunidade?"
2. Crie a skill seguindo o padrão: frontmatter YAML + instruções diretas
3. Salve em `~/.claude/skills/` e teste com `/nome-da-skill`
4. Guie para publicar: crie repo GitHub, estruture como `01-categoria/nome-skill/SKILL.md`

---

### Frontier — Gestão de Contexto (Avançado + topic = context)

> **Como funciona:** O Claude Code tem um limite de contexto por sessão. Quando esse limite se aproxima, o Claude compacta automaticamente a conversa — e pode perder decisões importantes. Dominar a gestão de contexto significa manter a qualidade do trabalho mesmo em sessões longas.

```
Você já opera em sessões longas. Hora de dominar o contexto! Escolha:

a) Hook PreCompact — salva decisões críticas antes da compactação automática
b) Estratégia de contexto mínimo — estruturar prompts para desperdiçar menos tokens
c) Auditoria de uso de contexto — identificar o que está consumindo mais espaço
```

**Se escolher (a) — PreCompact hook:**
1. Explique: "O Claude Code compacta o contexto automaticamente quando está cheio. Um hook `prompt` no evento `PreCompact` garante que informações críticas sejam preservadas no resumo."
2. Mostre o JSON:
   ```json
   {
     "PreCompact": [{
       "matcher": "",
       "hooks": [{
         "type": "prompt",
         "prompt": "Antes de compactar, salve explicitamente: (1) decisões de arquitetura tomadas nesta sessão, (2) arquivos modificados e por quê, (3) próximos passos pendentes. Inclua isso no resumo de compactação."
       }]
     }]
   }
   ```
3. ✓ Micro-check: "Essas 3 categorias cobrem o que você precisa preservar entre sessões? Podemos personalizar."
4. Leia `~/.claude/settings.json`, faça merge, escreva o arquivo
5. Explique: "Agora, antes de qualquer compactação, o Claude vai revisar e incluir explicitamente as decisões críticas no resumo."

**Se escolher (b) — Contexto mínimo:**
1. Explique: "Cada arquivo lido, cada resultado de ferramenta, ocupa espaço no contexto. Operações desnecessárias reduzem o quanto você pode trabalhar em uma sessão."
2. Mostre estratégias práticas:
   - Usar Grep em vez de ler arquivos completos quando só precisa de uma função
   - Passar contexto preciso para subagentes (não o histórico completo)
   - Usar `.clinerules` ou `.claude/settings.json` para limitar quais arquivos o Claude acessa automaticamente
3. Ofereça auditar o CLAUDE.md atual para identificar instruções que forçam carregamento desnecessário de contexto

**Se escolher (c) — Auditoria de contexto:**
1. Peça ao usuário: "Descreva o que você está fazendo quando percebe que o Claude começa a se confundir ou perder instruções."
2. Analise padrões comuns de consumo excessivo:
   - Leitura de arquivos grandes inteiros quando só uma seção era necessária
   - Múltiplas rodadas de feedback sem compactação manual
   - Ausência de hook PreCompact para preservar decisões
3. Sugira melhorias concretas baseadas no padrão identificado

---

## Ao Final de Qualquer Exercício

Sempre pergunte:

```
Exercício concluído! O que quer fazer agora?

1. Ver seu plano de aprendizado → /learn path
2. Testar o que aprendeu → quiz rápido (3 perguntas)
3. Explorar outro tópico → /learn [hooks|agents|claude-md|skills|commits|context]
4. Terminar por aqui
```

Se escolher (2), leia e execute `learn-quiz.md` no modo reinforcement com o tópico praticado.
Se escolher (1), leia e execute `learn-path.md` com o nível detectado.
