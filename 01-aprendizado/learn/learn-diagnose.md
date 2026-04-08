---
name: learn-diagnose
description: Diagnoses a Claude Code user's experience level by inspecting their environment, then asks 1-2 targeted questions. Outputs one of: Iniciante, Intermediário, Avançado.
---

# Claude Code Level Diagnosis

Your job is to determine the user's Claude Code experience level so the right exercise can be offered. Do this in two steps: inspect, then confirm.

## Step 1 — Silent Environment Inspection

Run these checks silently (no output to user yet). Use Glob and Bash tools.

**Check A — Global CLAUDE.md**
```bash
ls ~/.claude/CLAUDE.md 2>/dev/null && echo "EXISTS" || echo "MISSING"
```

**Check B — Hooks configured**
```bash
node -e "
const s=require(require('os').homedir()+'/.claude/settings.json');
const hooks=s.hooks||{};
const custom=Object.keys(hooks).filter(k=>!['PreToolUse'].includes(k)||hooks[k].some(h=>h.matcher!=='Skill'));
console.log(custom.length>0?'HAS_HOOKS':'NO_HOOKS');
" 2>/dev/null || echo "NO_HOOKS"
```

**Check C — Custom skills**
```bash
ls ~/.claude/skills/ 2>/dev/null | grep -v "^$" | wc -l | xargs -I{} sh -c 'if [ {} -gt 0 ]; then echo "HAS_SKILLS"; else echo "NO_SKILLS"; fi'
```

**Check D — Project CLAUDE.md**
```bash
ls .claude/CLAUDE.md 2>/dev/null && echo "EXISTS" || echo "MISSING"
```

## Step 2 — Score and Classify

Score the user based on findings:

| Finding | Points |
|---|---|
| Global CLAUDE.md exists | +2 |
| Hooks configured | +3 |
| Custom skills installed | +3 |
| Project CLAUDE.md exists | +1 |

**Classification:**
- 0–2 points → **Iniciante**
- 3–5 points → **Intermediário**
- 6–9 points → **Avançado**

## Step 3 — Ask 1 Targeted Question

Ask exactly ONE question based on the biggest gap found:

- If NO global CLAUDE.md: "Você já configurou um CLAUDE.md para personalizar como o Claude trabalha com você?"
- If CLAUDE.md exists but NO hooks: "Você já configurou hooks — comandos que rodam automaticamente quando o Claude termina uma tarefa?"
- If hooks exist but NO custom skills: "Você já criou skills personalizadas para ensinar o Claude a seguir seus próprios processos?"
- If everything found: "Você já usou agentes paralelos para dividir tarefas complexas em paralelo?"

Wait for the answer. Use it to adjust the classification by +1 or -1 if the answer contradicts the signals (e.g., has CLAUDE.md but says they've never used it).

## Step 4 — Announce Level

Present the result clearly:

```
Nível detectado: [Iniciante / Intermediário / Avançado]

Por quê: [1-2 sentences explaining the signals found]
```

Then immediately invoke `learn-exercise` with the detected level and any topic argument passed to this skill.
