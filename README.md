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
  <a href="#-learn-comandos">/learn</a> •
  <a href="#-roadmap">🗺️ Roadmap</a> •
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

### Recomendado — via Skillshare

[Skillshare](https://github.com/kursku/skills/tree/master/tooling/skillshare) é o gerenciador de skills para Claude Code. Instala, atualiza e sincroniza skills com um comando.

```bash
# Instalar o skillshare (uma vez só)
skillshare install kursku/skills -s skillshare
skillshare sync

# Instalar todas as skills deste pack
skillshare install kursku/learn-claude-code --all --track
skillshare sync
```

> 💡 `--track` permite atualizar com `skillshare install && skillshare sync` quando houver novidades.

### Manual — via git clone

```bash
# 1. Clone o repositório
git clone https://github.com/kursku/learn-claude-code.git

# 2. Copie as skills
cp -r learn-claude-code/01-aprendizado/. ~/.claude/skills/
```

### Passo final — use no terminal

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

## ⭐ /learn — Comandos

A skill principal deste pack. Use `/learn` para descobrir seu nível e receber um plano personalizado:

| Comando | O que faz | Nível sugerido |
|---------|-----------|---------------|
| `/learn` | Diagnóstico completo + exercício personalizado | Todos |
| `/learn quiz` | Teste seus conhecimentos (5 perguntas calibradas) | Todos |
| `/learn path` | Veja seu roadmap com progresso persistente | Todos |
| `/learn claude-md` | Crie ou melhore seu CLAUDE.md | Iniciante+ |
| `/learn commits` | Fluxo de commits com Conventional Commits | Iniciante+ |
| `/learn hooks` | Configure hooks de automação | Intermediário+ |
| `/learn skills` | Crie sua primeira skill personalizada | Intermediário+ |
| `/learn agents` | Aprenda multi-agentes e subagentes | Intermediário+ |
| `/learn context` | Gerencie contexto, tokens e peak hours | Avançado |

### Como funciona o diagnóstico

O `/learn` inspeciona seu ambiente silenciosamente e classifica seu nível:

| Check | Pontos |
|-------|--------|
| `~/.claude/CLAUDE.md` existe | +2 |
| Hooks configurados em `settings.json` | +3 |
| Skills instaladas em `~/.claude/skills/` | +3 |
| `.claude/CLAUDE.md` de projeto existe | +1 |

- **0–3 pts → Iniciante** — exercícios de CLAUDE.md e primeiros commits
- **4–6 pts → Intermediário** — hooks, skills e automações
- **7–9 pts → Avançado** — multi-agent, frontier hooks, gestão de contexto

---

## 🗺️ Roadmap

O que já está pronto e o que vem a seguir. Use como referência para contribuir.

### ✅ v1.0 — Fundação
- [x] Router `/learn` com diagnóstico automático de nível
- [x] Exercícios calibrados por nível (Iniciante / Intermediário / Avançado)
- [x] Seções Frontier para usuários avançados (hooks prompt, commits avançados, publicar skills)
- [x] Quiz com 15 perguntas no nível Apply (cenários reais, não definições)
- [x] Roadmap personalizado por nível
- [x] Roteamento Nível × Tópico (ex: Avançado + hooks → prompt hooks, não notificação básica)

### ✅ v1.1 — Qualidade e Contexto
- [x] Preambles "Como funciona" em cada seção (reduz carga cognitiva)
- [x] Micro-checks após passos críticos
- [x] Novo tópico `/learn context` — janelas de 5h, peak hours (10h–16h BRT), estratégias de economia
- [x] Persistência de progresso via `~/.learn-progress`
- [x] Links externos corrigidos (removidos repos não verificados)
- [x] Seção `Intermediário × agents` adicionada

### 🔜 v1.2 — Robustez
- [ ] Diagnóstico Check B mais robusto no Windows (evitar `node -e` com aspas aninhadas)
- [ ] Suporte a `/learn worktrees` (Git worktrees paralelos)
- [ ] Suporte a `/learn mcp` (Model Context Protocol)
- [ ] Modo `/learn <tópico> --reset` para forçar novo diagnóstico

### 💡 Ideias Futuras
- [ ] `/learn tokens` — monitore consumo em tempo real via console.anthropic.com
- [ ] Integração com `skillshare update` para notificar quando há conteúdo novo
- [ ] Versão EN para comunidade internacional

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

**O que são peak hours e por que importam?**
Nos dias úteis entre 10h–16h BRT (1pm–7pm GMT), o Claude consome sua janela de uso de 5 horas mais rápido. Jobs pesados devem ser agendados fora desse período. Use `/learn context` para saber mais.

---

## 🤝 Contribuindo

Quer adicionar uma skill ou melhorar uma existente?

1. Faça um fork do repositório
2. Crie sua skill seguindo o [guia](./docs/COMO_CRIAR_SKILL.md)
3. Consulte o [TEST-REPORT.md](./docs/TEST-REPORT.md) para entender o padrão de qualidade
4. Abra um Pull Request

Dúvidas? Abra uma [issue](https://github.com/kursku/learn-claude-code/issues).

---

<p align="center">
  Feito com ❤️ por <a href="https://github.com/kursku">kursku</a>
</p>
