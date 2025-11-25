# Knowledge

Store reference documents, research, specs, meeting notes, and any persistent information that your tasks might need.

> This directory is gitignored—your notes stay private and local.

---

## What Goes Here

| Type | Examples |
|------|----------|
| Specs & briefs | Project requirements, feature specs |
| Meeting notes | Decisions, action items, attendees |
| Research | Market analysis, technical findings |
| Process docs | How-tos, checklists, runbooks |
| References | Links, contacts, credentials (encrypted) |

---

## Linking from Tasks

Reference knowledge docs in your task files:

```yaml
resource_refs:
  - Knowledge/project-spec.md
  - Knowledge/meeting-notes-2024-01-15.md
```

See [`examples/example_files/example_knowledge.md`](../examples/example_files/example_knowledge.md) for a template.
