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

As sub-skills estão na mesma pasta. Use a ferramenta **Read** para carregar cada arquivo e siga suas instruções diretamente.

### Sem argumento → diagnóstico completo
Leia e execute `learn-diagnose.md` (modo completo — faz perguntas ao usuário).
Com o nível detectado, leia e execute `learn-exercise.md`.

### `quiz` → modo quiz standalone
Leia `learn-diagnose.md` (modo silencioso — apenas inspeciona ambiente, não faz perguntas).
Com o nível detectado, leia e execute `learn-quiz.md` no modo standalone (5 perguntas).

### `path` → roadmap
Leia `learn-diagnose.md` (modo silencioso).
Com o nível detectado, leia e execute `learn-path.md`.

### Qualquer outro tópico (`hooks`, `agents`, `claude-md`, `skills`, `commits`) → exercício com nível
Leia `learn-diagnose.md` (modo silencioso — apenas inspeciona ambiente, não faz perguntas).
Com o nível detectado, leia e execute `learn-exercise.md` passando o tópico e o nível.
Isso garante que o exercício seja calibrado ao nível do usuário (ex: Avançado + hooks → prompt hooks, não notificação básica).

> **Nota:** os caminhos dos arquivos ficam em `<base_dir>/learn-diagnose.md`, `<base_dir>/learn-exercise.md` etc., onde `<base_dir>` é o diretório base desta skill (informado no contexto de execução).

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
