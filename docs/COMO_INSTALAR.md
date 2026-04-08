# 📦 Como instalar skills no Claude Code

Guia passo a passo para instalar qualquer skill deste repositório.

---

## Pré-requisitos

- [Claude Code](https://claude.ai/code) instalado
- Git instalado no terminal

---

## ✅ Recomendado — via Skillshare

[Skillshare](https://github.com/kursku/skills/tree/master/tooling/skillshare) é o gerenciador oficial de skills para Claude Code. Instala, atualiza e sincroniza com um comando.

### 1. Instalar o Skillshare (uma vez só)

```bash
skillshare install kursku/skills -s skillshare
skillshare sync
```

### 2. Instalar todas as skills deste pack

```bash
skillshare install kursku/learn-claude-code --all --track
skillshare sync
```

### 3. Testar

```bash
claude
/learn
```

### Atualizar quando houver novidades

```bash
skillshare install && skillshare sync
```

### Remover

```bash
skillshare uninstall learn
skillshare sync
```

---

## Manual — via git clone

Se preferir instalar manualmente:

### Instalação completa

```bash
# 1. Clone o repositório
git clone https://github.com/kursku/learn-claude-code.git

# 2. Copie todas as skills
cp -r learn-claude-code/01-aprendizado/. ~/.claude/skills/

# 3. Teste
claude
/learn
```

### Instalação individual

```bash
cp -r learn-claude-code/01-aprendizado/learn ~/.claude/skills/
```

### Atualizar manualmente

```bash
cd learn-claude-code
git pull
cp -r 01-aprendizado/. ~/.claude/skills/
```

### Remover manualmente

```bash
rm -rf ~/.claude/skills/learn
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
