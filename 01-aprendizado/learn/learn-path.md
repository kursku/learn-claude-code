---
name: learn-path
description: Mostra um roadmap de aprendizado personalizado baseado no nível do usuário (Iniciante/Intermediário/Avançado). Indica o que aprender em ordem, com comandos concretos para cada passo.
---

# Seu Plano de Aprendizado — Claude Code

Apresente o roadmap baseado no nível recebido. Use checkboxes visuais para mostrar o que já foi feito vs o que falta.

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
[ ] Git worktrees            → /learn worktrees (em breve)
[ ] Multi-agent workflows    → /learn agents

RECURSOS
- Guia completo: github.com/FlorianBruniaux/claude-code-ultimate-guide
- Curso interativo: github.com/delbaoliveira/learn-claude-code
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
[ ] Subagent-driven dev      → skill superpowers:subagent-driven-development
[ ] Git worktrees            → /learn worktrees (em breve)

AVANÇADO
[ ] Multi-agent orchestration
[ ] Hooks com LLM (tipo prompt)
[ ] Contribuir skills para a comunidade

RECURSOS
- Nível Senior: github.com/FlorianBruniaux/claude-code-ultimate-guide
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
[ ] Criar e publicar plugins  → skill skill-creator
[ ] Worktrees paralelos       → superpowers:using-git-worktrees
[ ] Scheduled agents          → skill schedule

COMPARTILHE
[ ] Contribuir uma skill para a comunidade
[ ] Documentar seu workflow em CLAUDE.md público

RECURSOS
- Power User: github.com/FlorianBruniaux/claude-code-ultimate-guide
- Quiz avançado: /learn quiz
```

Após mostrar o roadmap, pergunte: "Quer começar por algum tópico específico? Digite `/learn <tópico>` ou escolha da lista acima."
