---
name: learn-path
description: Mostra um roadmap de aprendizado personalizado baseado no nível do usuário (Iniciante/Intermediário/Avançado). Indica o que aprender em ordem, com comandos concretos para cada passo.
---

# Seu Plano de Aprendizado — Claude Code

Apresente o roadmap baseado no nível recebido. Use checkboxes visuais para mostrar o que já foi feito vs o que falta.

## Progresso Persistente

Antes de mostrar o roadmap, leia `~/.learn-progress` (se existir) para verificar quais tópicos o usuário já completou. O arquivo tem o formato:

```
hooks=done
claude-md=done
commits=done
```

Marque com `[x]` os tópicos que aparecem como `done` no arquivo. Os demais ficam `[ ]`.

Ao final do roadmap, pergunte:
```
Quer marcar algum tópico como concluído? Digite o nome (ex: hooks, commits, claude-md) ou "nenhum" para continuar.
```

Se o usuário nomear um tópico, adicione-o ao arquivo `~/.learn-progress` com `=done`.
Se o arquivo não existir, crie-o com a entrada nova.

## Se nível = Iniciante

```
Seu plano de aprendizado — Claude Code

FUNDAMENTOS (comece aqui)
[ ] CLAUDE.md global         → /learn claude-md
[ ] Primeiro commit guiado   → /learn commits
[ ] Entender ferramentas     → Read, Edit, Bash, Glob, Grep

PRÓXIMO NÍVEL
[ ] Hooks básicos            → /learn hooks
[ ] Skills personalizadas    → /learn skills
[ ] CLAUDE.md de projeto     → crie .claude/CLAUDE.md no seu repo

AVANÇADO (quando estiver confortável)
[ ] Agentes paralelos        → /learn agents
[ ] Gestão de contexto       → /learn context
[ ] Multi-agent workflows    → /learn agents

RECURSOS
- Documentação oficial: docs.anthropic.com/claude-code
- Quiz a qualquer momento: /learn quiz
```

## Se nível = Intermediário

```
Seu plano de aprendizado — Claude Code

JÁ DOMINADO ✓
[x] CLAUDE.md básico
[x] Fluxo de trabalho diário

DESBLOQUEIE AGORA
[ ] Hooks de automação       → /learn hooks
[ ] Skills personalizadas    → /learn skills
[ ] settings.json avançado   → explore permissions, env vars

PRÓXIMO NÍVEL
[ ] Agentes paralelos        → /learn agents
[ ] Gestão de contexto       → /learn context
[ ] Commits avançados        → /learn commits

AVANÇADO
[ ] Multi-agent orchestration
[ ] Hooks com LLM (tipo prompt)
[ ] Contribuir skills para a comunidade

RECURSOS
- Documentação oficial: docs.anthropic.com/claude-code
- Quiz: /learn quiz
```

## Se nível = Avançado

```
Seu plano de aprendizado — Claude Code

JÁ DOMINADO ✓
[x] CLAUDE.md personalizado
[x] Hooks configurados
[x] Skills instaladas

OTIMIZE
[ ] Audit CLAUDE.md          → /learn (opção de revisão)
[ ] Hooks com tipo prompt     → decisões com LLM
[ ] Hooks tipo agent          → verificações complexas

FRONTIER
[ ] Gestão avançada de contexto → /learn context
[ ] Publicar skill pública       → /learn skills
[ ] Hooks tipo prompt/agent      → /learn hooks

COMPARTILHE
[ ] Contribuir uma skill para a comunidade
[ ] Documentar seu workflow em CLAUDE.md público

RECURSOS
- Documentação oficial: docs.anthropic.com/claude-code
- Quiz avançado: /learn quiz
```

Após mostrar o roadmap, pergunte: "Quer começar por algum tópico específico? Digite `/learn <tópico>` ou escolha da lista acima."
