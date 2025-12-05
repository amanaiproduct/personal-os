# Structuring Context: Markdown & Directories

## Why Markdown?

In the age of AI, **text is the universal interface**. While traditional software relies on databases (SQL) and strict data structures (JSON/XML), AI agents thrive on natural language mixed with light structure.

Markdown is the perfect bridge between human and machine.

### 1. The Native Tongue of LLMs
Large Language Models are trained on the internet—Wikipedia, documentation, GitHub repositories—which means they "think" in headings, lists, and code blocks.
- **JSON** is efficient for data but expensive for tokens and hard for humans to read.
- **PDFs/Word Docs** are heavy, hard to parse, and often lose formatting.
- **Markdown** preserves hierarchy (`#`, `##`), relationships (`-`, `1.`), and emphasis (`**`) using minimal characters.

### 2. "Coding" Your Context
When you use Markdown, you are essentially "coding" your knowledge.
- **Refactoring**: You can move sections, split files, and rename concepts just like refactoring code.
- **Version Control**: Markdown plays perfectly with Git. You can see exactly what changed in your thoughts or tasks over time.
- **Linting**: You can enforce style guides (e.g., "All tasks must have a status").

### 3. Metadata via Frontmatter
By adding YAML frontmatter to the top of a file, you turn a simple text document into a database record.

```markdown
---
type: task
priority: P0
status: pending
tags: [bug, api]
---

# Fix API Latency
```

This allows your AI agent to:
- **Query**: "Find all files where `priority: P0`"
- **Filter**: "Show me only `status: pending`"
- **Read**: "Summarize the content below the header"

## The Power of Directory Structure

If Markdown is the **content**, the directory structure is the **context**.

In PersonalOS, we don't use a database to store relationships. We use the filesystem.

### 1. Semantics by Location
Where a file lives tells the AI what it *is*.

- `Tasks/Fix-Bug.md` → The agent knows this is actionable work.
- `Knowledge/Fix-Bug.md` → The agent knows this is a post-mortem or documentation.
- `Archive/Fix-Bug.md` → The agent knows to ignore this unless asked for history.

You don't need to explain "This is a task" in the file content. The folder path `/Tasks/` *is* the explanation.

### 2. Scoping Context
Directory structures allow you to control the AI's "attention span."

- **Broad Scope**: "Search `Knowledge/` for best practices." (Agent looks at reference material).
- **Narrow Scope**: "Check `Tasks/Active/` for conflicts." (Agent looks only at current work).

This prevents the "needle in a haystack" problem where the AI gets confused by irrelevant documents.

### 3. Scalability
A flat list of 1,000 files is unmanageable for humans and confusing for agents. A nested structure handles complexity gracefully.

```
Project/
├── Core/          # High-level rules
├── Features/      # Specific specs
│   ├── Auth/
│   └── Payment/
└── Legacy/        # Ignored context
```

The AI can traverse this tree logically, just like a developer navigating a codebase.

## Putting It Together

When you combine **Structured Markdown** with **Semantic Directories**, you create a "Database for Agents" without installing any software.

**Example Workflow:**
1.  **User**: "What's high priority?"
2.  **Agent**:
    *   Scans directory: `Tasks/` (ignoring `Knowledge/`)
    *   Parses files: Reads YAML frontmatter for `priority: P0`
    *   Synthesizes: Returns a list of P0 tasks using the Markdown headers as summaries.

This approach is robust, portable, and future-proof. Even if you change AI models, your text files and folders remain the ultimate source of truth.
