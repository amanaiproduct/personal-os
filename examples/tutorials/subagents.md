# Subagents in Claude Code

Running multiple Claude instances for parallel work.

## Overview

Subagents let Claude spawn additional Claude instances to handle tasks in parallel. Think of it as delegation - the main Claude coordinates while subagents do focused work.

## When to Use Subagents

**Good use cases:**
- Processing multiple files simultaneously
- Research tasks that can be parallelized
- Batch operations (create 10 tasks, update 5 files)

**Not ideal for:**
- Sequential work where each step depends on the previous
- Simple single-file operations
- Tasks requiring heavy coordination

## How It Works

```
┌─────────────────────────────────────┐
│         Main Claude (Coordinator)    │
│                                     │
│  "Process these 5 backlog items"    │
└──────────┬──────────────────────────┘
           │
           ├──► Subagent 1: "Create task for item 1"
           ├──► Subagent 2: "Create task for item 2"  
           ├──► Subagent 3: "Create task for item 3"
           ├──► Subagent 4: "Research item 4"
           └──► Subagent 5: "Check for duplicates of item 5"
           
           │ (all run in parallel)
           ▼
┌─────────────────────────────────────┐
│  Main Claude collects results       │
│  and presents summary               │
└─────────────────────────────────────┘
```

## Example: Parallel Task Creation

Without subagents (sequential):
```
Creating task 1... done (2s)
Creating task 2... done (2s)
Creating task 3... done (2s)
Total: 6 seconds
```

With subagents (parallel):
```
Creating tasks 1, 2, 3 in parallel... done
Total: 2 seconds
```

## PersonalOS Subagent Patterns

### Pattern 1: Batch Backlog Processing

When you have many backlog items, Claude can delegate:

```
You: Process my backlog (15 items)

Claude (coordinator):
- Subagent 1-5: Check items 1-5 for duplicates
- Subagent 6-10: Categorize items 6-10
- Subagent 11-15: Create task files for clear items

→ All results collected and presented as unified summary
```

### Pattern 2: Research Aggregation

```
You: Research our top 3 competitors

Claude (coordinator):
- Subagent 1: Research Competitor A
- Subagent 2: Research Competitor B
- Subagent 3: Research Competitor C

→ Results synthesized into single analysis
```

### Pattern 3: Multi-File Updates

```
You: Add "due_date: 2024-02-01" to all P0 tasks

Claude (coordinator):
- Identifies 4 P0 task files
- Spawns 4 subagents to update each file
- Confirms all updates completed
```

## Limitations

1. **Context isn't shared** - Each subagent starts fresh, doesn't see what others are doing
2. **Coordination overhead** - Sometimes sequential is simpler
3. **Resource usage** - More subagents = more API calls

## Tips

- Let Claude decide when to use subagents - it knows when parallel helps
- For simple operations, sequential is often faster
- Subagents work best for independent, parallelizable tasks

---

*Next: [Tool Calling & MCP](tool-calling.md)*
