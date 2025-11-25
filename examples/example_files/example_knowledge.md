# Knowledge Base Example - Project Architecture

## Overview
This is an example of a knowledge document that tasks can reference. Store any persistent information here that multiple tasks might need.

## Common Use Cases

### Technical Documentation
- API endpoints and authentication
- Database schemas
- Deployment procedures
- Architecture decisions

### Process Documentation  
- How to submit expenses
- Code review process
- Meeting templates
- Onboarding checklist

### Reference Information
- Important links and bookmarks
- Team contact info
- Vendor details
- License keys (encrypted)

### Research & Analysis
- Market research findings
- Competitor analysis
- User interview notes
- Feature specifications

## Linking from Tasks

In your task files, reference knowledge docs like this:
- `See [[Knowledge/api-docs.md]] for endpoint details`
- `Process defined in [[Knowledge/code-review.md]]`
- `Research findings: [[Knowledge/user-interviews-q1.md]]`

## Organization Tips

1. **Use clear filenames**: `project-name-spec.md` not `spec.md`
2. **Date versioned docs**: `meeting-notes-2024-01-15.md`
3. **Create index files**: `engineering-index.md` linking to all eng docs
4. **Archive old docs**: Move to `Knowledge/archive/` subfolder

## Template Sections

When creating new knowledge docs, consider including:
- **Overview**: One paragraph summary
- **Context**: Why this exists, who needs it
- **Details**: The actual information
- **Related**: Links to related docs
- **Last Updated**: Date and author