# Task Management System with MCP Server

A reusable task management system for AI assistants (Claude, GPT, etc.) with intelligent deduplication and organization.

## Core Features

- **Smart Backlog Processing**: Automatically detects duplicates and ambiguous items
- **Task Organization**: Categories, priorities, and status tracking
- **CRM Integration**: Manage contacts alongside tasks
- **MCP Server**: Reliable tool interface for AI assistants
- **Configurable**: Customize categories, priorities, and workflows

## Quick Start

### 1. Setup

```bash
# Clone the repository
git clone https://github.com/yourusername/task-manager.git
cd task-manager

# Install dependencies
pip install pyyaml mcp

# Create directories
mkdir Tasks CRM
touch BACKLOG.md
```

### 2. Configure

Copy `templates/AGENTS.md` to your root and customize:
- Categories for your workflow
- Priority definitions
- Personal goals (optional)

### 3. Start MCP Server

```bash
python manager_ai_mcp/server_core.py
```

### 4. Use with AI Assistant

Tell your AI assistant:
```
"Read AGENTS.md for instructions on managing my tasks"
```

## System Architecture

```
task-manager/
├── manager_ai_mcp/
│   └── server_core.py      # MCP server with deduplication
├── Tasks/                  # Individual task files
├── CRM/                    # Contact files
├── BACKLOG.md             # Unstructured notes
├── AGENTS.md              # AI instructions (from template)
└── config.yaml            # Optional configuration
```

## Task Format

Tasks are markdown files with YAML frontmatter:

```yaml
---
title: Clear task description
category: technical
priority: P1
status: n
estimated_time: 60
---

# Task Details

## Overview
What needs to be done and why.

## Next Actions
- [ ] Step 1
- [ ] Step 2
```

## MCP Tools Available

| Tool | Description |
|------|-------------|
| `list_tasks` | Filter and view tasks |
| `create_task` | Create new task with metadata |
| `update_task_status` | Change task status |
| `process_backlog_with_dedup` | Smart backlog processing |
| `get_task_summary` | Statistics and overview |
| `prune_completed_tasks` | Clean old completed tasks |

## Configuration

Create `config.yaml` to customize:

```yaml
categories:
  - development
  - marketing
  - operations
  - research

priorities:
  - P0  # Critical
  - P1  # Important
  - P2  # Normal
  - P3  # Low

deduplication:
  similarity_threshold: 0.6
  check_keywords: true

priority_limits:
  P0: 3
  P1: 5
```

## Deduplication Features

The system automatically:
- Detects similar tasks using fuzzy matching
- Identifies ambiguous items that need clarification
- Suggests appropriate categories
- Prevents duplicate task creation

## Best Practices

1. **Process backlog regularly** - Weekly is recommended
2. **Keep tasks specific** - Ambiguous tasks get flagged
3. **Monitor priority balance** - Don't overload P0/P1
4. **Prune completed tasks** - Auto-cleanup after 30 days
5. **Link related items** - Connect tasks to CRM contacts

## Customization

The system is designed to be extended:

- **Categories**: Add your own in config.yaml
- **Priorities**: Define what's urgent for you
- **Workflows**: Modify AGENTS.md instructions
- **Integrations**: Extend MCP server with new tools

## Example Workflow

```bash
# 1. Add items to backlog
echo "- Email John about project\n- Fix login bug\n- Research competitors" >> BACKLOG.md

# 2. Tell AI to process
"Process my backlog"

# 3. AI responds:
"Found 3 items:
- 1 potential duplicate: 'Fix login bug' matches existing 'Fix authentication issue'
- 1 needs clarification: 'Research competitors' - what specific questions?
- 1 ready to create: 'Email John about project'"

# 4. Resolve and create tasks
"Skip the duplicate, create the email task, I'll clarify research later"
```

## Privacy & Sharing

The core system (this repo) contains:
- Generic MCP server code
- Template configurations
- Example structures

Your personal data stays local:
- Tasks/
- CRM/
- BACKLOG.md
- Personal AGENTS.md

## Contributing

Contributions welcome! The goal is a reusable system that works for different workflows:
- Additional category templates
- New MCP tools
- Improved deduplication algorithms
- Integration examples

## License

MIT - Use freely for personal or commercial projects.

## Credits

Built for use with AI assistants like Claude, GPT, and others that support tool calling.