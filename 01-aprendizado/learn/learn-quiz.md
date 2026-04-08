---
name: learn-quiz
description: Quiz mode for /learn — standalone (5 questions) or reinforcement (3 questions post-exercise), calibrated to detected user level
---

# Learn Quiz

You are running the Claude Code quiz. Follow these instructions exactly.

## Mode Detection

You will be invoked in one of two modes:

- **Standalone**: Called from `learn.md` after silent diagnosis → 5 questions calibrated to detected level
- **Reinforcement**: Called from `learn-exercise.md` after an exercise → 3 questions about the concept just practiced

The invoking skill will pass the mode and relevant context (level + topic if reinforcement).

---

## Standalone Mode (5 questions)

### Question Banks by Level

#### Iniciante (0–3 points from diagnosis)

1. **Where does Claude Code look for your personal instructions?**
   - A) `~/.config/claude/rules.md`
   - B) `~/.claude/CLAUDE.md`
   - C) `~/claude-instructions.txt`
   - D) `.env` file in the project root
   - **Answer: B** — `~/.claude/CLAUDE.md` is your global instructions file. Project-level instructions go in `.claude/CLAUDE.md` inside the project.

2. **What happens when you run `/commit`?**
   - A) Automatically commits all staged files with a generic message
   - B) Opens a PR on GitHub
   - C) Guides you through a structured commit with conventional commit format
   - D) Runs `git push` directly
   - **Answer: C** — The `/commit` skill walks you through the commit process, formatting the message according to Conventional Commits.

3. **What is a "skill" in Claude Code?**
   - A) A Python script that extends Claude's abilities
   - B) A markdown file that gives Claude specialized instructions for a task
   - C) A pre-trained model fine-tuned for a specific domain
   - D) A browser extension
   - **Answer: B** — Skills are markdown files (`.md`) with YAML frontmatter. Claude loads them when you invoke `/skill-name`.

4. **You want Claude to always respond in Portuguese. Where do you write this rule?**
   - A) In every prompt you send
   - B) In `~/.claude/CLAUDE.md`
   - C) In `~/.claude/settings.json`
   - D) In a `.env` file
   - **Answer: B** — Personal behavior rules go in your global `CLAUDE.md`. Claude reads this at the start of every session.

5. **What does `~/.claude/` contain?**
   - A) Only Claude Code's binary files
   - B) Your session history and nothing else
   - C) Your personal configuration: CLAUDE.md, settings.json, hooks, skills, and memory
   - D) The Claude API key only
   - **Answer: C** — The `~/.claude/` directory is your personal Claude Code workspace: global instructions, settings, hooks, custom skills, and persistent memory.

---

#### Intermediário (4–6 points from diagnosis)

1. **What is a Claude Code hook?**
   - A) A Git pre-commit check
   - B) A shell command that runs automatically on specific Claude Code events (e.g., Stop, Notification)
   - C) A way to inject code into Claude's responses
   - D) A plugin that modifies Claude's model weights
   - **Answer: B** — Hooks are shell commands configured in `settings.json` that fire on lifecycle events like `Stop`, `PreToolUse`, `PostToolUse`, `Notification`, etc.

2. **Which settings.json key configures hooks?**
   - A) `"plugins"`
   - B) `"extensions"`
   - C) `"hooks"`
   - D) `"events"`
   - **Answer: C** — Hooks live under the `"hooks"` key in `~/.claude/settings.json`, organized by event name.

3. **You want a skill that's only active for one project, not globally. Where do you put it?**
   - A) `~/.claude/skills/`
   - B) `.claude/skills/` inside the project directory
   - C) `~/.config/skills/`
   - D) Skills can't be project-scoped
   - **Answer: B** — Skills in `.claude/skills/` inside a project directory are only available when working in that project.

4. **What's the difference between `~/.claude/CLAUDE.md` and `.claude/CLAUDE.md` (project-level)?**
   - A) There is no difference — Claude only reads one of them
   - B) Global applies everywhere; project-level applies only in that project and can override global
   - C) Project-level applies everywhere; global is ignored
   - D) They are the same file in different formats
   - **Answer: B** — Global CLAUDE.md sets defaults for all projects. Project-level adds context specific to that codebase and can override global settings for that project.

5. **What event hook would you use to send a notification when Claude finishes a task?**
   - A) `PreToolUse`
   - B) `SessionStart`
   - C) `Stop`
   - D) `PostToolUse`
   - **Answer: C** — The `Stop` event fires when Claude finishes its response. It's the right hook for "task complete" notifications.

---

#### Avançado (7–9 points from diagnosis)

1. **What is a subagent in Claude Code?**
   - A) A background process that monitors your CPU usage
   - B) A separate Claude instance with isolated context, dispatched to handle a specific task
   - C) A cheaper version of Claude for simple tasks
   - D) A human reviewer who checks Claude's output
   - **Answer: B** — Subagents are fresh Claude instances dispatched via the `Agent` tool. They have no memory of the parent session — you provide exactly the context they need.

2. **Why dispatch subagents with isolated context instead of doing everything in one session?**
   - A) Subagents are faster because they use a different server
   - B) Each subagent stays focused on its task without confusion from earlier conversation history
   - C) Subagents have access to more tools
   - D) It's required by the Claude Code license
   - **Answer: B** — Context isolation prevents subagents from being confused by irrelevant prior conversation. You craft exactly what they need, nothing more.

3. **You have a CLAUDE.md that's grown to 400 lines. What's the likely impact?**
   - A) No impact — Claude reads all of it equally
   - B) Claude may miss instructions buried in the middle; shorter, structured files are more reliable
   - C) Claude will automatically summarize it
   - D) Claude will refuse to read files over 300 lines
   - **Answer: B** — Very long CLAUDE.md files can dilute instruction following. Keep them focused: global for universal rules, project-level for codebase-specific context.

4. **What is the `PostToolUse` hook useful for?**
   - A) Running code before Claude reads a file
   - B) Injecting additional context after each tool call (e.g., context usage warnings, linting results)
   - C) Blocking tool calls that match a pattern
   - D) Modifying Claude's response before it's shown to the user
   - **Answer: B** — `PostToolUse` fires after each tool call. It can inject `additionalContext` into Claude's conversation, making it aware of conditions like context limits or test failures.

5. **When designing a multi-agent workflow, what should each subagent receive?**
   - A) The full parent session transcript
   - B) Access to all files in the repository
   - C) Only the information it needs to complete its specific task — no more
   - D) A copy of the parent's memory
   - **Answer: C** — Subagents should receive minimal, precise context. Over-providing context wastes tokens and can confuse the agent. Under-providing leads to NEEDS_CONTEXT escalations.

---

## Reinforcement Mode (3 questions post-exercise)

Based on the topic practiced, select 3 relevant questions:

### After CLAUDE.md exercise
- Use Iniciante Q1, Q4, and Intermediário Q4

### After hooks exercise
- Use Intermediário Q1, Q2, Q5

### After skills exercise
- Use Iniciante Q3, Intermediário Q3, and ask: **"What frontmatter field is required in every skill file?"** (Answer: `name` and `description`)

### After commit exercise
- Use Iniciante Q2, then ask: **"What type prefix would you use for a bug fix in Conventional Commits?"** (Answer: `fix`), then: **"What's the imperative mood rule?"** (Answer: "add", not "added" or "adds")

### After agent/multi-agent exercise
- Use Avançado Q1, Q2, Q5

---

## Quiz Delivery Format

Present each question as:

```
**Question N of N**

[Question text]

A) [Option]
B) [Option]
C) [Option]
D) [Option]
```

After the user answers:
- If correct: `✓ Correct! [Explanation from answer key]`
- If incorrect: `✗ Not quite. The answer is [X]. [Explanation from answer key]`

After all questions, show:
```
Quiz complete: N/N correct

[If score < 60%]: These topics are worth revisiting. Try `/learn <topic>` to practice hands-on.
[If score 60-80%]: Good foundation! A few gaps to fill — check the weak areas above.
[If score > 80%]: Strong knowledge. You're ready for the next level.
```

If this was reinforcement mode, add:
```
Want to continue learning? Try `/learn path` to see your full roadmap.
```
