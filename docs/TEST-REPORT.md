# /learn Skill — Test Report

**Data:** 2026-04-09
**Ambiente de teste:** Windows 10, Claude Code (Sonnet 4.6)
**Nível detectado:** Avançado (8/9 pontos)

---

## Ambiente de Diagnóstico

| Check | Resultado | Pontos |
|-------|-----------|--------|
| Global CLAUDE.md (`~/.claude/CLAUDE.md`) | EXISTS | +2 |
| Hooks configurados | HAS_HOOKS | +3 |
| Custom skills instaladas | HAS_SKILLS (1.577) | +3 |
| Project CLAUDE.md (`.claude/CLAUDE.md`) | MISSING | +0 |
| **Total** | | **8/9 → Avançado** |

---

## Resultados por Comando

### `/learn` — Diagnóstico completo

| Etapa | Status | Observação |
|-------|--------|------------|
| Leitura de `learn-diagnose.md` | ✅ OK | Arquivo encontrado |
| Modo completo (Steps 1-4) | ✅ OK | Inspeção + pergunta + anúncio de nível |
| Continuidade para `learn-exercise.md` | ⚠️ Ambíguo | SKILL.md diz "passe o nível" mas não diz explicitamente "leia e execute learn-exercise.md" após diagnose terminar |

**Problema:** A instrução no SKILL.md é:
> "Leia e execute `learn-diagnose.md`. Passe o nível detectado para `learn-exercise.md`."

Isso é ambíguo — "passe o nível" não deixa claro que o router deve ler exercise.md **depois** que diagnose finaliza. Um modelo menos instruído pode não carregar o exercise automaticamente.

---

### `/learn quiz` — Modo quiz

| Etapa | Status | Observação |
|-------|--------|------------|
| Diagnóstico silencioso | ✅ OK | Detecta Avançado sem perguntar |
| Ranges de score | ✅ OK | 0-3/4-6/7-9 consistente entre diagnose e quiz |
| Banco Avançado (7-9) | ✅ OK | 5 perguntas corretas |
| Referência ao arquivo | ✅ OK | `SKILL.md` (corrigido de `learn.md`) |
| Reforço frontier | ✅ OK | Perguntas para prompt hooks e commits |

---

### `/learn path` — Roadmap

| Etapa | Status | Observação |
|-------|--------|------------|
| Diagnóstico silencioso | ✅ OK | Detecta Avançado |
| Seção Avançado exibida | ✅ OK | Checkboxes corretos para nível |
| Links externos | ⚠️ Não verificado | `github.com/FlorianBruniaux/claude-code-ultimate-guide` e `github.com/delbaoliveira/learn-claude-code` — podem não existir |
| Persistência de progresso | ❌ Ausente | Checkboxes sempre voltam desmarcados em nova sessão |

---

### `/learn hooks` — Hooks (Avançado)

| Etapa | Status | Observação |
|-------|--------|------------|
| Diagnóstico silencioso | ✅ OK | 8/9 = Avançado |
| Tabela de roteamento | ✅ OK | `hooks + Avançado` → Frontier: Hooks Avançados |
| Seção entregue | ✅ OK | Conteúdo de prompt/agent hooks, não notificação básica |
| Exercícios frontier | ✅ OK | PreToolUse prompt, PreCompact prompt, Audit |

> **Teste mais crítico:** antes da correção, este fluxo entregava o exercício de notificação básica para qualquer nível. Agora entrega conteúdo correto para Avançado. ✅

---

### `/learn commits` — Commits (Avançado)

| Etapa | Status | Observação |
|-------|--------|------------|
| Diagnóstico silencioso | ✅ OK | Avançado detectado |
| Tabela de roteamento | ✅ OK | `commits + Avançado` → Frontier: Commits Avançados |
| Seção entregue | ✅ OK | Hook de validação, aliases, audit de histórico |
| Exercícios frontier | ✅ OK | Conteúdo relevante e acionável |

---

### `/learn agents` — Agentes (Avançado)

| Etapa | Status | Observação |
|-------|--------|------------|
| Diagnóstico silencioso | ✅ OK | Avançado detectado |
| Tabela de roteamento | ✅ OK | `agents + Avançado` → Seção Avançado (multi-agent) |
| Seção entregue | ✅ OK | Workflow multi-agente com Task tool |
| agents + Intermediário | ⚠️ Gap | Tabela mapeia para "Seção Intermediário (opção skill)" — mas a seção Intermediário não tem conteúdo dedicado para agentes. O usuário Intermediário que pede `/learn agents` recebe opções genéricas de hooks/skills, não sobre agentes. |

---

### `/learn claude-md` — CLAUDE.md (Avançado)

| Etapa | Status | Observação |
|-------|--------|------------|
| Diagnóstico silencioso | ✅ OK | Avançado detectado |
| Tabela de roteamento | ✅ OK | `claude-md + Avançado` → Seção Avançado (audit) |
| Seção entregue | ✅ OK | Auditoria com boas práticas |

---

### `/learn skills` — Skills (Avançado)

| Etapa | Status | Observação |
|-------|--------|------------|
| Diagnóstico silencioso | ✅ OK | Avançado detectado |
| Tabela de roteamento | ✅ OK | `skills + Avançado` → Frontier: Publicar Skill |
| Seção entregue | ✅ OK | Criar, publicar e criar skill pack |

---

## Resumo Geral

| Comando | Roteamento | Conteúdo | UX |
|---------|-----------|----------|-----|
| `/learn` | ⚠️ | ✅ | ✅ |
| `/learn quiz` | ✅ | ✅ | ✅ |
| `/learn path` | ✅ | ⚠️ | ⚠️ |
| `/learn hooks` | ✅ | ✅ | ✅ |
| `/learn commits` | ✅ | ✅ | ✅ |
| `/learn agents` | ⚠️ | ⚠️ | ⚠️ |
| `/learn claude-md` | ✅ | ✅ | ✅ |
| `/learn skills` | ✅ | ✅ | ✅ |

**Aprovação geral: 6/8 fluxos sem ressalvas**

---

## Bugs e Melhorias Identificados

### 🔴 Bug — SKILL.md: instrução ambígua para `/learn` sem argumento

**Arquivo:** `SKILL.md`
**Problema:** "Passe o nível detectado para `learn-exercise.md`" não instrui explicitamente o modelo a ler e executar `learn-exercise.md` após o diagnose terminar.
**Fix:** Substituir por "Com o nível detectado, leia e execute `learn-exercise.md`."

---

### 🟠 Gap de conteúdo — `/learn agents` para Intermediário

**Arquivo:** `learn-exercise.md`
**Problema:** Usuário Intermediário que digita `/learn agents` cai na seção genérica de Intermediário (hooks/skills/claude-md), sem mencionar agentes.
**Fix:** Adicionar seção "Intermediário × agents" com introdução a subagentes simples (ex: usar um agente para pesquisa paralela).

---

### 🟠 Label enganosa — Seção Intermediário

**Arquivo:** `learn-exercise.md`
**Problema:** O header da seção diz `Se level = Intermediário (ou topic = hooks)` — mas hooks+Avançado agora vai para Frontier. Um mantenedor futuro pode se confundir.
**Fix:** Atualizar para `Se level = Intermediário (ou topic = hooks para Iniciante/Intermediário)`.

---

### 🟡 Links externos não verificados — `/learn path`

**Arquivo:** `learn-path.md`
**Problema:** Recursos apontam para repositórios GitHub externos que podem não existir.
**Fix:** Substituir por links verificados ou remover referências específicas, usando descrições genéricas.

---

### 🟡 Persistência de progresso — `/learn path`

**Arquivo:** `learn-path.md`
**Problema:** Checkboxes do roadmap sempre aparecem desmarcados. Não há memória de tópicos já concluídos entre sessões.
**Possíveis soluções:**
- Usar o sistema de memória do Claude Code (`~/.claude/projects/.../memory/`) para salvar progresso
- Criar um arquivo `.learn-progress` no diretório do usuário
- Aceitar como limitação conhecida e documentar

---

### 🟡 Check B frágil no diagnóstico (Windows)

**Arquivo:** `learn-diagnose.md`
**Problema:** O check de hooks usa `node -e` com aspas aninhadas que podem falhar em shells Windows.
**Fix:** Usar Glob diretamente em `~/.claude/settings.json` para verificar se a chave `hooks` tem entradas, sem depender de node.

---

## Melhorias Sugeridas (Próximas Iterações)

### v1.1 — Fixes críticos (imediatos)
- [ ] Corrigir instrução de continuidade no SKILL.md para `/learn` sem argumento
- [ ] Adicionar seção `agents` para Intermediário em learn-exercise.md
- [ ] Corrigir label da seção Intermediário

### v1.2 — Qualidade
- [ ] Verificar e atualizar links externos em learn-path.md
- [ ] Robustecer Check B do diagnóstico para Windows

### v1.3 — Features
- [ ] Persistência de progresso via arquivo `.learn-progress`
- [ ] Suporte a `/learn worktrees` (frontier já no roadmap)
- [ ] Suporte a `/learn mcp` (Model Context Protocol — tópico emergente)
- [ ] Modo `/learn <tópico> --reset` para reiniciar diagnóstico

---

*Relatório gerado automaticamente durante sessão de melhoria contínua da skill /learn.*
