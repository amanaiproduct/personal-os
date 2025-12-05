# Understanding MCP: The "API for AI"

## What is MCP?

The Model Context Protocol (MCP) is an open standard that enables AI agents to interact with external systems securely. In PersonalOS, the MCP server acts as the "Product Logic Layer" between the AI and your file system.

Think of it like an API for your AI. Instead of giving the agent raw, unstructured access to read and write files, you give it a set of defined tools with strict rules.

## Why Use It?

**1. Prevent Data Corruption**
Without MCP, an agent might write a file with the wrong format or missing metadata. With MCP, you enforce a schema (e.g., "Task priority must be P0, P1, or P2").

**2. Intelligent Deduplication**
Raw agents can't easily check 50 files for duplicates without reading all of them (costing tokens and time). An MCP server can run efficient logic to check for similarity before creating a new item.

**3. Context Aggregation**
Instead of the agent reading multiple files to understand the state of the project, the server can aggregate data from tasks, backlogs, and calendars into a single "System Status" object.

## The Problem: Raw File Access

Without MCP, an AI agent interacting with a codebase works like a developer with direct database access.

**The "Raw" Approach:**
> **User:** "Check my backlog."
> **AI:** *Reads `BACKLOG.md` directly.* "I see 'fix bug'."
> **User:** "Add 'fix bug' to tasks."
> **AI:** *Creates a new markdown file.*

**Risks:**
- **Inconsistency:** The AI creates files with varying formats.
- **Duplication:** It doesn't know a task called "Bug Fix: API" already exists.
- **Hallucination:** It might invent categories or tags that don't exist in your system.

## The Solution: The MCP Layer

MCP introduces a middleware layer that encapsulates your business logic.

**The "MCP" Approach:**
> **User:** "Check my backlog."
> **AI:** *Calls `process_backlog` tool.*
> **Server:** *Runs logic to parse and dedup items.* "Here is the list."
> **User:** "Add 'fix bug'."
> **AI:** *Calls `create_task` tool.*
> **Server:** *Checks for duplicates.* "Rejected: 90% similar to existing task T-123."

## Core Features in PersonalOS

Here is how PersonalOS uses MCP to turn a simple markdown system into a smart application.

### 1. Business Logic Injection
We force the agent to use `create_task` instead of writing files directly.

**The Schema:**
```json
{
  "name": "create_task",
  "arguments": {
    "title": "string (required)",
    "priority": "string (enum: P0, P1, P2)",
    "category": "string (inferred from content)"
  }
}
```
*Benefit:* The agent *cannot* create a P5 task because the schema restricts it to P0-P2.

### 2. Intelligent Deduplication
The `process_backlog_with_dedup` tool moves complexity from the prompt to the server.

- **Input:** A list of raw text strings.
- **Server Logic:** Uses Python's `difflib` to compare new items against existing task titles.
- **Output:** Categorizes items as "New", "Duplicate", or "Ambiguous".

This allows the agent to handle hundreds of backlog items without filling its context window.

### 3. Context Aggregation
The `get_system_status` tool solves the "fragmented context" problem.

Instead of the AI reading 10 different files to answer "How am I doing?", it calls one tool. The server compiles:
- Active task count by priority
- Backlog size
- Current time of day insights

## Anatomy of an MCP Tool

An effective MCP tool consists of three parts:

1.  **Intent (Name & Description)**
    *   *Ex:* `prune_completed_tasks`
    *   *Desc:* "Deletes tasks marked 'done' that are older than X days."
    *   *Role:* Tells the AI *when* to use this tool.

2.  **Constraints (Input Schema)**
    *   *Ex:* `days` must be an integer > 0.
    *   *Role:* Prevents the AI from passing invalid arguments.

3.  **Execution (Server Logic)**
    *   *Ex:* Python code that safely iterates and deletes files.
    *   *Role:* Ensures reliability independent of the AI's ability to write shell commands.

## Summary

MCP acts as the backend for your AI frontend.

- **Without MCP:** The AI creates and edits files directly, relying on prompt instructions for consistency.
- **With MCP:** The AI interacts through a safe API, ensuring data consistency and enforcing business rules.

This structure allows you to build robust AI-powered applications that go beyond simple text generation.
