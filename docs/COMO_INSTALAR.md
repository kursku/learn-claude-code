# 📦 Como instalar skills no Claude Code

Guia passo a passo para instalar qualquer skill deste repositório.

---

## Pré-requisitos

- [Claude Code](https://claude.ai/code) instalado
- Git instalado no terminal

---

## Instalação completa (todas as skills)

```bash
# 1. Clone o repositório
git clone https://github.com/kursku/learn-claude-code.git

# 2. Copie todas as skills
cp -r learn-claude-code/01-aprendizado/. ~/.claude/skills/

# 3. Teste
claude
/learn
```

---

## Instalação individual

Para instalar apenas uma skill específica:

```bash
# Instalar apenas o /learn
cp -r learn-claude-code/01-aprendizado/learn ~/.claude/skills/
```

---

## Onde ficam as skills

As skills do Claude Code ficam em `~/.claude/skills/`. Cada skill é uma pasta com arquivos `.md`:

```
~/.claude/skills/
└── learn/
    ├── learn.md           ← skill principal (invocada com /learn)
    ├── learn-diagnose.md  ← sub-skill de diagnóstico
    ├── learn-exercise.md  ← sub-skill de exercícios
    ├── learn-quiz.md      ← sub-skill de quiz
    └── learn-path.md      ← sub-skill de roadmap
```

---

## Atualizar quando houver novidades

```bash
cd learn-claude-code
git pull
cp -r 01-aprendizado/. ~/.claude/skills/
```

---

## Remover uma skill

```bash
rm -rf ~/.claude/skills/learn
```
