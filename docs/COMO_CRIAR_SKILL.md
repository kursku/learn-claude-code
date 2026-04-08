# ✍️ Como criar sua própria skill

Guia para criar e contribuir com novas skills para este repositório.

---

## Estrutura básica

Toda skill é um arquivo `.md` com frontmatter YAML:

```markdown
---
name: minha-skill
description: O que essa skill faz e quando usar.
---

# Título da Skill

Suas instruções aqui...
```

## Campos obrigatórios

| Campo | Descrição |
|-------|-----------|
| `name` | Identificador da skill (lowercase, hífens) — deve bater com o nome do arquivo |
| `description` | Uma frase explicando o que a skill faz |

---

## Skills simples vs. skills com sub-skills

**Skill simples** — um único arquivo:
```
minha-skill/
└── minha-skill.md
```

**Skill com sub-skills** — roteador + especialistas:
```
minha-skill/
├── minha-skill.md          ← roteador
├── minha-skill-parte1.md   ← sub-skill
└── minha-skill-parte2.md   ← sub-skill
```

---

## Boas práticas

- ✅ Instruções claras e diretas ("Faça X", não "Você pode querer fazer X")
- ✅ Escreva em português (PT-BR)
- ✅ Inclua exemplos de uso
- ✅ Teste antes de abrir PR
- ❌ Não use jargão técnico sem necessidade
- ❌ Não crie skills para tarefas que o Claude já faz bem por padrão

---

## Contribuindo

```bash
# 1. Fork e clone
gh repo fork kursku/learn-claude-code --clone

# 2. Crie uma branch
git checkout -b feat/minha-nova-skill

# 3. Adicione sua skill na categoria certa
# Ex: 01-aprendizado/minha-skill/minha-skill.md

# 4. Abra um Pull Request
gh pr create
```
