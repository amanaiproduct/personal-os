# Memory & Context

How your AI agent remembers your preferences, goals, and working style.

## Overview

AI coding agents (Claude Code, Codex, Factory, etc.) don't have persistent memory between sessions by default. PersonalOS solves this with structured files that your agent reads at the start of each conversation.

## The Memory Stack

```
┌─────────────────────────────────────┐
│  AGENTS.md (System Instructions)    │  ← Always loaded first
├─────────────────────────────────────┤
│  GOALS.md (Your Objectives)         │  ← Reference for prioritization
├─────────────────────────────────────┤
│  Tasks/*.md (Active Work)           │  ← Current state
├─────────────────────────────────────┤
│  Knowledge/*.md (Reference Docs)    │  ← Context when needed
└─────────────────────────────────────┘
```

## How It Works

### 1. AGENTS.md - The Instruction Layer

When you start your AI agent in a directory with an instructions file (AGENTS.md, CLAUDE.md, etc.), it automatically reads this file. This is your "system prompt" that shapes the agent's behavior.

**What goes here:**
- How you want your agent to behave
- Your task format and categories
- Priority definitions
- Writing style preferences

**Example:**
```markdown
# AGENTS.md

You are a productivity assistant. When I say "process backlog":
1. Read BACKLOG.md
2. Create tasks in Tasks/ with YAML frontmatter
3. Clear the backlog when done

Always check GOALS.md before assigning priorities.
```

### 2. GOALS.md - The Priority Layer

Your agent reads this to understand what matters to you. When deciding between P1 and P2, it checks if a task aligns with your stated goals.

**Why this works:**
- You define success criteria once
- Every task gets evaluated against your goals
- Priorities stay consistent across sessions

### 3. Tasks & Knowledge - The State Layer

These directories hold your current work state. Your agent reads them to:
- Avoid creating duplicate tasks
- Understand what you're working on
- Find related context for new work

## Memory Patterns

### Pattern 1: Persistent Preferences

Put preferences in AGENTS.md that you want applied to every session:

```markdown
## My Preferences
- Never schedule more than 3 P0 tasks
- Morning is for deep work, afternoon for meetings
- I prefer bullet points over long paragraphs
```

### Pattern 2: Session Context

For temporary context (this week's focus), add it to GOALS.md:

```markdown
## This Week's Focus
- Shipping the Q1 roadmap presentation by Thursday
- Avoiding new commitments until launch
```

### Pattern 3: Task-Specific Memory

For context that belongs to a specific task, put it in the task file:

```markdown
# Write Q1 Blog Post

## Context
- Target audience: Product managers
- Tone: Casual, practical
- Based on learnings from January launch
- Reference: Knowledge/january-launch-retro.md
```

## Tips for Better Memory

1. **Be specific in AGENTS.md** - Vague instructions get vague results
2. **Update GOALS.md regularly** - Stale goals lead to wrong priorities  
3. **Use Knowledge/ for reference** - Don't repeat context in every task
4. **Link related files** - Help your agent find relevant context

## Common Issues

**"My agent forgot my preferences"**
- Check that AGENTS.md is in the root directory
- Make sure preferences are explicit, not implied

**"Priorities seem random"**
- Review GOALS.md - are your goals still accurate?
- Check if AGENTS.md has clear priority definitions

**"My agent doesn't know about my other tasks"**
- It only reads files you reference or that match its search
- Try: "Read my current P0 and P1 tasks before answering"

---

*Next: [Tool Calling & MCP](tool-calling.md)*
