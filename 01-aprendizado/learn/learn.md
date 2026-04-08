---
name: learn
description: Skill de onboarding para Claude Code. Diagnostica o nível do usuário e oferece exercícios personalizados. Uso: /learn (diagnóstico completo), /learn <tópico> (pula direto para módulo), /learn quiz (modo quiz).
---

# /learn — Claude Code Onboarding

Você é o roteador do sistema de aprendizado do Claude Code. Leia o argumento passado e roteie corretamente.

## Como interpretar o comando

O usuário pode ter digitado:
- `/learn` — sem argumento
- `/learn quiz`
- `/learn hooks`
- `/learn agents`
- `/learn claude-md`
- `/learn skills`
- `/learn commits`
- `/learn path`

## Lógica de Roteamento

### Sem argumento → diagnóstico completo
Invoque `learn-diagnose`. Passe o nível detectado para `learn-exercise`.

### `quiz` → modo quiz standalone
Invoque `learn-diagnose` (modo silencioso — apenas inspeciona ambiente, não faz perguntas).
Com o nível detectado, invoque `learn-quiz` no modo standalone (5 perguntas).

### `path` → roadmap
Invoque `learn-diagnose` (modo silencioso).
Com o nível detectado, invoque `learn-path`.

### Qualquer outro tópico (`hooks`, `agents`, `claude-md`, `skills`, `commits`) → exercício direto
Invoque `learn-exercise` diretamente com o tópico passado. Pule o diagnóstico.

## Mensagem de Boas-vindas

Antes de qualquer ação, mostre:

```
/learn — Claude Code Onboarding

[diagnóstico completo]  /learn
[tópico específico]     /learn hooks | agents | claude-md | skills | commits
[modo quiz]             /learn quiz
[ver roadmap]           /learn path
```

Então execute o roteamento adequado.

## Tópicos Disponíveis

| Tópico | O que faz |
|---|---|
| `hooks` | Configura automações com hooks |
| `agents` | Usa agentes paralelos |
| `claude-md` | Cria/melhora CLAUDE.md |
| `skills` | Cria skills personalizadas |
| `commits` | Fluxo de commit com Conventional Commits |
| `quiz` | Testa seu conhecimento |
| `path` | Ver seu roadmap personalizado |

## Tratamento de Tópico Desconhecido

Se o argumento não for nenhum dos tópicos acima, responda:

```
Tópico "[argumento]" não reconhecido.

Tópicos disponíveis: hooks, agents, claude-md, skills, commits, quiz, path

Ou use /learn sem argumento para o diagnóstico completo.
```
