# Build Your Personal OS

A hands-on guide to building your own AI-powered productivity system using coding agents like Cursor, Claude Code, or Factory.

## Why Build a Personal OS?

Most people use ChatGPT as a chat interface. But AI coding agents give you something more powerful: the ability to build systems that work *for* you, not just *with* you.

Building a Personal OS teaches you AI fundamentals through daily use:
- **Context management** - How do you give an AI the right information?
- **Agent memory** - How does an AI remember across sessions?
- **Tool use** - How do agents take actions in the real world?
- **Workflow automation** - How do you encode repeatable processes?

When you use your Personal OS daily, the bottlenecks become visceral. You'll intuit solutions before they're announced because you've faced the exact problems yourself.

## What You'll Build

By the end of this guide, you'll have:

```
personal-os/
├── AGENTS.md           # Your AI's instructions and personality
├── GOALS.md            # Your objectives and priorities
├── BACKLOG.md          # Quick capture inbox
├── Tasks/              # Individual task files with metadata
├── Knowledge/          # Reference docs, notes, research
│   └── voice-samples/  # Your writing examples for voice matching
└── examples/
    └── workflows/      # Reusable agent workflows
```

This isn't just a folder structure - it's a system where your AI agent:
- Processes messy notes into organized tasks
- Prioritizes based on your goals
- Writes in your voice
- Suggests what to work on each day

## Prerequisites

- An AI coding agent: [Cursor](https://cursor.sh), [Claude Code](https://claude.ai), or [Factory](https://factory.ai)
- Basic comfort with files and folders
- 30 minutes for initial setup

No coding experience required. The AI does the coding.

---

## Part 1: The Foundation

### Step 1: Clone or Create Your Workspace

**Option A: Use this template**
```bash
git clone https://github.com/amanaiproduct/personal-os.git
cd personal-os
./setup.sh
```

**Option B: Start from scratch**
Create a new folder and open it in your AI coding agent.

### Step 2: Create AGENTS.md

This is your AI's instruction manual. It tells the agent who it is and how to behave.

```markdown
# AGENTS.md

You are a personal productivity assistant. You help me:
- Process messy notes into organized tasks
- Prioritize based on my goals
- Suggest what to work on each day

## Workspace Structure
- Tasks/ - Individual task files
- Knowledge/ - Reference documents
- BACKLOG.md - Quick capture inbox
- GOALS.md - My objectives

## When I say "process my backlog":
1. Read BACKLOG.md
2. Create task files in Tasks/
3. Clear the backlog

## Task Format
Tasks are markdown files with YAML frontmatter:
---
title: Task name
priority: P0/P1/P2/P3
status: n (not started), s (started), d (done)
---
```

**Key insight**: AGENTS.md is just a markdown file, but it shapes every interaction. This is "prompt engineering" in practice - you're encoding your preferences into a reusable system prompt.

### Step 3: Create GOALS.md

Your AI needs to know what matters to you to prioritize correctly.

```markdown
# GOALS.md

## This Quarter
- Ship the Q1 product roadmap
- Build thought leadership through writing
- Improve team velocity by 20%

## Priority Framework
- P0: Must do THIS WEEK
- P1: Important, has deadlines
- P2: Normal priority
- P3: Nice to have
```

### Step 4: Create BACKLOG.md

This is your inbox - dump anything here without organizing it.

```markdown
# Backlog

- follow up with james about api
- write blog post about launch learnings
- expense report overdue
- idea: what if we added AI to search?
```

### Step 5: Test It

Open your AI coding agent in the personal-os folder and say:

> "Read AGENTS.md and process my backlog"

Watch what happens. The agent should:
1. Read your instructions
2. Read your backlog
3. Create task files in Tasks/
4. Ask clarifying questions if needed

**This is the core loop**: Dump notes → Process with AI → Get organized tasks.

---

## Part 2: Core Concepts

### Concept 1: Context Engineering

The #1 skill in working with AI agents is **giving them the right context**.

Your Personal OS solves this through file structure:
- AGENTS.md = persistent instructions (always loaded)
- GOALS.md = your priorities (referenced when prioritizing)
- Knowledge/ = deep context (loaded when relevant)

**Try this**: Add something to your backlog that relates to a goal. Process it and see how the AI connects them.

### Concept 2: Agent Memory

AI agents don't remember between sessions. Your Personal OS creates "memory" through files:

| Type | File | Purpose |
|------|------|---------|
| Instructions | AGENTS.md | How to behave |
| Priorities | GOALS.md | What matters |
| State | Tasks/*.md | Current work |
| Context | Knowledge/*.md | Reference material |

**The insight**: Memory isn't magic - it's just structured information the agent reads each time.

### Concept 3: Tool Use

When you say "create a task," your AI agent:
1. Interprets your intent
2. Decides to use the "create file" tool
3. Generates the file content
4. Writes it to disk

This is the same pattern as any AI product:
- Intent → Tool selection → Execution → Result

Your Personal OS uses simple tools (read/write files), but the pattern scales to APIs, databases, and complex integrations.

### Concept 4: Workflows as Skills

Instead of putting everything in AGENTS.md, you can create **workflow files** that the agent reads on-demand.

```
examples/workflows/
├── content-generation.md  # How to write in your voice
├── morning-standup.md     # Daily planning routine
└── weekly-review.md       # Reflection process
```

In AGENTS.md, you just reference them:

```markdown
## Specialized Workflows

| Trigger | Workflow File |
|---------|---------------|
| Writing tasks | examples/workflows/content-generation.md |
| "What should I work on?" | examples/workflows/morning-standup.md |
```

**Why this matters**: It keeps your main instructions lightweight and makes workflows reusable and shareable.

---

## Part 3: Daily Use

### Morning Routine (2 minutes)

Open your agent and ask:

> "What should I work on today?"

The agent reads your tasks, checks priorities, and suggests focus areas.

### During the Day

Whenever you have a thought, note, or task - dump it in BACKLOG.md. Don't organize, just capture.

```markdown
# Backlog

- sarah mentioned bug with file uploads
- prep for thursday meeting
- look into competitor's new feature
```

### End of Day (5 minutes)

> "Process my backlog"

The agent turns your messy notes into organized tasks.

### Weekly Review (15 minutes)

> "What did I accomplish this week? How am I tracking against my goals?"

The agent reviews completed tasks and compares against GOALS.md.

---

## Part 4: Advanced - Voice Training

One of the most powerful features: teaching your AI to write like you.

### Step 1: Collect Writing Samples

Create `Knowledge/voice-samples/` and add 5-10 examples of your actual writing:
- Emails you sent
- Posts you published
- Messages you liked

### Step 2: Create a Voice Guide

Ask your agent:

> "Read my voice samples in Knowledge/voice-samples/ and create a voice guide that captures my writing style. Save it to Knowledge/voice-guide.md"

### Step 3: Use It

Now when you ask for any writing task, the agent will:
1. Read your voice guide
2. Apply your patterns
3. Draft content that sounds like you

**The pattern**: Few-shot prompting through examples, stored as files.

---

## Part 5: Team Use

Your Personal OS can become a team system.

### Shared Repository

Put your personal-os in a Git repo. Team members can:
- Share the same AGENTS.md conventions
- Contribute to Knowledge/
- Use the same workflow files

### Team-Specific Workflows

Create workflows for team processes:
- `workflows/sprint-planning.md`
- `workflows/incident-response.md`
- `workflows/onboarding.md`

### Knowledge Base

Build a shared Knowledge/ folder with:
- Product specs
- Architecture docs
- Decision records
- Research findings

The AI becomes a team member that knows your institutional knowledge.

---

## Part 6: X-Ray Vision

After using your Personal OS daily, you'll develop intuition for how AI products work.

### Every AI Product Has:

1. **Context** - What information does it have access to?
2. **Instructions** - What is it told to do? (system prompt)
3. **Tools** - What actions can it take?
4. **Memory** - How does it persist information?
5. **Orchestration** - How does it decide what to do?

### When You See a New AI Product, Ask:

- "Where's the context coming from?"
- "What's in the system prompt?"
- "What tools does it have access to?"
- "How is it storing state?"
- "Is it one agent or multiple?"

### You've Already Built These:

| Concept | In Your Personal OS |
|---------|---------------------|
| System prompt | AGENTS.md |
| RAG (retrieval) | Knowledge/ folder |
| Agent memory | Task files with status |
| Tool use | File read/write |
| Multi-agent | Workflow delegation |
| Few-shot prompting | voice-samples/ |

---

## Troubleshooting

### "The AI doesn't follow my instructions"

- Make AGENTS.md more specific
- Add examples of what you want
- Check that it's being loaded (ask "what does AGENTS.md say?")

### "Tasks aren't prioritized correctly"

- Update GOALS.md with current priorities
- Be explicit about what P0 vs P1 means to you
- Add examples in AGENTS.md

### "The AI forgets things between sessions"

- This is normal - agents don't persist memory
- Everything important goes in files
- Reference files explicitly: "Read GOALS.md before answering"

### "The output doesn't sound like me"

- Add more voice samples
- Be specific in your voice guide about what to avoid
- Give feedback and iterate

---

## Next Steps

1. **Use it daily** - The value compounds with use
2. **Iterate on AGENTS.md** - Refine based on what works
3. **Build your Knowledge base** - Add docs you reference often
4. **Create custom workflows** - Encode your processes
5. **Share with your team** - Scale what works

---

## Resources

- [Memory & Context Tutorial](memory.md) - Deep dive on how context works
- [Voice Training Tutorial](voice-training.md) - Detailed voice training guide
- [Tool Calling Tutorial](tool-calling.md) - How agents use tools
- [Workflows README](../workflows/README.md) - Available workflows

---

*This guide is part of [PersonalOS](https://github.com/amanaiproduct/personal-os) - an open-source template for building your AI-powered productivity system.*
