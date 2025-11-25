# Backlog Processing Workflow

Turn messy brain dumps into organized, prioritized tasks.

## When to Use

- End of day: Process notes captured throughout the day
- Weekly: Clear out accumulated ideas
- After meetings: Turn action items into tasks

## The Prompt

```
Process my backlog
```

## Example: Before & After

### Your BACKLOG.md (messy input)

```markdown
# Backlog

- need to follow up with james about the api thing
- Q2 planning thoughts - should we focus on mobile or web first? need to think through this
- bug: users can't upload files larger than 10mb, sarah mentioned this
- write blog post about our launch learnings
- competitor launched new feature, should analyze
- 1:1 with mike tomorrow, prep questions
- expense report overdue
- idea: what if we added AI to the search?
```

### The Conversation

**You:** Process my backlog

**Claude:** I found 8 items in your backlog. Let me analyze them:

**Ready to create (5 items):**
| Item | Category | Suggested Priority |
|------|----------|-------------------|
| Follow up with James about API | outreach | P1 |
| Write blog post about launch learnings | writing | P2 |
| Analyze competitor's new feature | research | P2 |
| Prep questions for Mike 1:1 | admin | P1 (tomorrow) |
| Submit expense report | admin | P1 (overdue) |

**Needs clarification (2 items):**

1. "Q2 planning - mobile vs web focus"
   - Is this a decision you need to make, or research to inform the decision?
   - Should this be a task or added to GOALS.md as a strategic question?

2. "Bug: file upload > 10mb"
   - Is this for you to fix, or should it be tracked in your bug tracker?
   - What priority - is it blocking users?

**Potential duplicate (1 item):**
- "AI search idea" - You have an existing task "Explore AI features for Q2" (68% similar). Should I merge this as a sub-item?

How would you like me to proceed?

**You:** The Q2 planning is research I need to do. Bug is P0, users are complaining. Merge the AI idea.

**Claude:** Got it. Creating 6 tasks:

✓ Created: Follow up with James about API.md (P1, outreach)
✓ Created: Write blog post - launch learnings.md (P2, writing)  
✓ Created: Analyze competitor new feature.md (P2, research)
✓ Created: Prep for Mike 1:1.md (P1, admin)
✓ Created: Submit expense report.md (P1, admin)
✓ Created: Research Q2 focus - mobile vs web.md (P2, research)
✓ Created: Fix file upload 10mb limit.md (P0, technical)
✓ Updated: Explore AI features for Q2.md - added search idea

Backlog cleared. You now have 3 P0/P1 tasks due soon:
1. Fix file upload limit (P0)
2. Expense report (P1, overdue)
3. Mike 1:1 prep (P1, tomorrow)

Want to start on any of these?

---

## Tips

- Dump everything into BACKLOG.md throughout the day - don't organize, just capture
- Process at least once per day to keep it manageable
- Be specific when clarifying - Claude will create better tasks
- Review the created tasks briefly to catch any misunderstandings
