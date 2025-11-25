# Tool Calling & MCP

How Claude takes actions and interacts with external systems.

## Overview

Claude Code can do more than chat - it can take actions through "tools." These let Claude read files, create tasks, run commands, and interact with external services.

## Built-in Tools

Claude Code comes with tools for:

| Tool | What it does |
|------|--------------|
| Read files | View contents of any file |
| Write files | Create or edit files |
| Run commands | Execute shell commands |
| Search | Find files and content |

**Example:**
```
You: Create a new P0 task for the API bug

Claude: [Uses write tool to create Tasks/Fix API bug.md]
✓ Created: Fix API bug.md
```

## MCP (Model Context Protocol)

MCP lets you give Claude custom tools. PersonalOS includes an optional MCP server that adds specialized task management tools.

### Why Use MCP?

**Without MCP:**
- Your agent reads/writes raw markdown files
- You define the format in AGENTS.md
- Works great for most users

**With MCP:**
- Claude gets purpose-built tools like `list_tasks`, `create_task`
- Automatic duplicate detection
- Structured data responses
- Better for power users and automation

### PersonalOS MCP Tools

```
┌─────────────────────────────────────────────────┐
│  Task Management                                │
├─────────────────────────────────────────────────┤
│  list_tasks        - Filter by category/status  │
│  create_task       - Create with auto-category  │
│  update_task_status - Change task state         │
│  get_task_summary  - Statistics and insights    │
├─────────────────────────────────────────────────┤
│  Backlog Processing                             │
├─────────────────────────────────────────────────┤
│  process_backlog   - Read backlog content       │
│  process_backlog_with_dedup - Smart processing  │
│  clear_backlog     - Mark as processed          │
│  prune_completed   - Clean old done tasks       │
├─────────────────────────────────────────────────┤
│  System Status                                  │
├─────────────────────────────────────────────────┤
│  get_system_status - Full dashboard             │
│  check_priority_limits - Workload warnings      │
└─────────────────────────────────────────────────┘
```

## Setting Up MCP (Optional)

### 1. Install Dependencies

```bash
cd core/mcp
pip install -r requirements.txt
```

### 2. Configure Claude Code

Add to your Claude Code MCP config:

```json
{
  "mcpServers": {
    "manager-ai": {
      "command": "python",
      "args": ["core/mcp/server.py"],
      "env": {
        "MANAGER_AI_BASE_DIR": "/path/to/your/personal-os"
      }
    }
  }
}
```

### 3. Verify It Works

```
You: Get my system status

Claude: [Calls get_system_status tool]

System Status:
- Active tasks: 12
- P0: 2, P1: 4, P2: 6
- Backlog items: 3
- Recommendation: Process backlog before EOD
```

## How Tool Calling Works

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│    You       │────►│   Claude     │────►│    Tool      │
│  "list P0s"  │     │ (interprets) │     │ (executes)   │
└──────────────┘     └──────────────┘     └──────────────┘
                            │                    │
                            │◄───────────────────┘
                            │    (returns data)
                            ▼
                     ┌──────────────┐
                     │  Claude      │
                     │ (formats     │
                     │  response)   │
                     └──────────────┘
```

1. You make a request in natural language
2. Claude decides which tool(s) to use
3. Tool executes and returns data
4. Claude formats the response for you

## With vs Without MCP

| Scenario | Without MCP | With MCP |
|----------|-------------|----------|
| List tasks | Claude reads all .md files | `list_tasks` returns structured data |
| Create task | Claude writes markdown | `create_task` with validation |
| Find duplicates | Claude compares titles manually | `process_backlog_with_dedup` |
| System overview | Claude reads multiple files | `get_system_status` |

## Tips

- **Start without MCP** - The basic system works great
- **Add MCP when** - You want automation, integrations, or power features
- **Tools are optional** - Claude can always fall back to basic file operations

---

*Back to: [Tutorials Home](README.md)*
