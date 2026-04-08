<p align="center">
  <img src="docs/assets/banner.png" alt="Learn Claude Code" width="100%" />
</p>

<h1 align="center">🤖 Learn Claude Code</h1>

<p align="center">
  <strong>Skills prontas para aprender e dominar o Claude Code — em português</strong><br/>
  Do primeiro uso até workflows avançados com agentes, hooks e automações.
</p>

<p align="center">
  <a href="#-como-instalar"><img src="https://img.shields.io/badge/skills-5%2B-brightgreen?style=for-the-badge" alt="5+ Skills" /></a>
  <a href="#-categorias"><img src="https://img.shields.io/badge/categorias-5-blue?style=for-the-badge" alt="5 Categorias" /></a>
  <a href="#"><img src="https://img.shields.io/badge/idioma-PT--BR-yellow?style=for-the-badge" alt="PT-BR" /></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/licen%C3%A7a-MIT-orange?style=for-the-badge" alt="MIT License" /></a>
</p>

<p align="center">
  <a href="#-como-instalar">📦 Como instalar</a> •
  <a href="#-categorias">📂 Categorias</a> •
  <a href="#-faq">❓ FAQ</a> •
  <a href="#-contribuindo">🤝 Contribuindo</a>
</p>

---

## 🎯 O que é isso?

**Skills** são instruções que ensinam o Claude Code a dominar tarefas específicas. É como contratar um especialista sob demanda — mas grátis e disponível 24/7 no seu terminal.

Este pack reúne skills focadas 100% em **aprender e usar o Claude Code** com eficiência:

```
🧠 Descubra seu nível atual...
📝 ...pratique com exercícios reais...
🧪 ...teste seu conhecimento com quiz...
🗺️  ...e siga o roadmap personalizado.
```

> 💡 **Feito para quem quer aprender Claude Code de verdade.** Sem enrolação, em português.

---

## 📦 Como instalar

### Passo 1 — Clone o repositório

```bash
git clone https://github.com/kursku/learn-claude-code.git
```

### Passo 2 — Copie as skills para o Claude Code

```bash
# Copiar a skill /learn
cp -r learn-claude-code/01-aprendizado/learn ~/.claude/skills/

# Ou copiar todas de uma vez
cp -r learn-claude-code/01-aprendizado/. ~/.claude/skills/
```

### Passo 3 — Use no terminal

```bash
claude  # abra o Claude Code
/learn  # ative a skill de aprendizado
```

> 🔥 **Dica:** o Claude Code carrega skills automaticamente de `~/.claude/skills/`. Não precisa reiniciar.

---

## 📂 Categorias

<table>
<tr>
<td width="50%" valign="top">

### 🧠 [01 — Aprendizado](./01-aprendizado/)
**5 skills** — Diagnóstico de nível, exercícios, quiz e roadmap personalizado
> Do zero ao avançado, no seu ritmo

</td>
<td width="50%" valign="top">

### ⚡ 02 — Produtividade *(em breve)*
Daily, context management, memória persistente
> Trabalhe mais rápido com o Claude do seu jeito

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 🌿 03 — Git & GitHub *(em breve)*
Commits, PRs, branches e automações git
> Histórico limpo e fluxo profissional

</td>
<td width="50%" valign="top">

### 🔧 04 — Desenvolvimento *(em breve)*
Debug, TDD, code review e refatoração
> Código melhor com menos esforço

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 🤖 05 — Agentes *(em breve)*
Multi-agent, subagentes paralelos e orquestração
> Delegue tarefas complexas para times de agentes

</td>
</tr>
</table>

---

## ⭐ Destaque: /learn

A skill principal deste pack. Use `/learn` para descobrir seu nível e receber um plano personalizado:

| Comando | O que faz |
|---------|-----------|
| `/learn` | Diagnóstico completo + exercício personalizado |
| `/learn quiz` | Teste seus conhecimentos (5 perguntas) |
| `/learn path` | Veja seu roadmap completo |
| `/learn hooks` | Aprenda hooks na prática |
| `/learn agents` | Aprenda multi-agentes |
| `/learn claude-md` | Crie seu CLAUDE.md |
| `/learn skills` | Crie sua primeira skill |
| `/learn commits` | Fluxo de commits profissional |

---

## ❓ FAQ

**Preciso pagar para usar?**
Não. As skills são gratuitas. Você só precisa ter o [Claude Code](https://claude.ai/code) instalado.

**Funciona no Windows?**
Sim! Claude Code funciona no Windows via terminal (PowerShell, Git Bash ou WSL).

**Posso usar várias skills ao mesmo tempo?**
Sim. Copie quantas quiser para `~/.claude/skills/` — todas ficam disponíveis automaticamente.

**As skills funcionam no claude.ai (não no terminal)?**
Essas skills foram feitas para o **Claude Code** (terminal). Para o claude.ai, veja o [pack-marketing-skills](https://github.com/kursku/pack-marketing-skills).

---

## 🤝 Contribuindo

Quer adicionar uma skill?

1. Faça um fork do repositório
2. Crie sua skill seguindo o [guia](./docs/COMO_CRIAR_SKILL.md)
3. Abra um Pull Request

Dúvidas? Abra uma [issue](https://github.com/kursku/learn-claude-code/issues).

---

<p align="center">
  Feito com ❤️ por <a href="https://github.com/kursku">kursku</a>
</p>
