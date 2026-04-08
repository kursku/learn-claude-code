---
name: learn-exercise
description: Delivers a personalized Claude Code exercise based on user level (Iniciante/Intermediário/Avançado) or a specific topic. Runs the exercise live in the session, then offers learn-path and learn-quiz.
---

# Claude Code Exercise Delivery

You receive a level (Iniciante, Intermediário, or Avançado) and optionally a topic. Deliver the right exercise.

## Quick Win Menu

Present exactly 3 options for the detected level. Let the user pick one.

### Se level = Iniciante (ou topic = claude-md)

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

### Se level = Intermediário (ou topic = hooks)

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
3. Leia `~/.claude/settings.json`, faça merge do hook, escreva o arquivo
4. Confirme: "Hook adicionado. Na próxima vez que o Claude terminar uma resposta, você receberá uma notificação."

**Se escolher (b) — Skill:**
Invoque a skill `write-a-skill` se disponível, ou guie:
1. Pergunte: "Qual processo você repete muito que o Claude poderia automatizar?"
2. Crie um arquivo `.md` simples em `~/.claude/skills/` com frontmatter + instruções

**Se escolher (c) — Project CLAUDE.md:**
1. Crie `.claude/CLAUDE.md` no diretório atual
2. Adicione regras específicas do projeto (linguagem, padrões de commit, arquivos a ignorar)

---

### Se level = Avançado (ou topic = agents)

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
2. Liste hooks existentes
3. Sugira hooks ausentes comuns: PreCompact (salvar estado), PostToolUse (auto-format), Notification (alertas)

---

## Ao Final de Qualquer Exercício

Sempre pergunte:

```
Exercício concluído! O que quer fazer agora?

1. Ver seu plano de aprendizado → /learn path
2. Testar o que aprendeu → quiz rápido (3 perguntas)
3. Explorar outro tópico → /learn [hooks|agents|claude-md|skills|commits]
4. Terminar por aqui
```

Se escolher (2), invoque `learn-quiz` no modo reinforcement com o tópico praticado.
Se escolher (1), invoque `learn-path` com o nível detectado.

Report: DONE or BLOCKED with brief summary.
