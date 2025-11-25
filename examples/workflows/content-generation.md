---
name: content-generation
description: Generate content (blog posts, emails, social media) in the user's authentic voice. Invoke when any writing, marketing, or content task is requested.
---

# Content Generation Workflow

Generate written content that sounds like the user, not generic AI.

## When to Use

- Writing blog posts, articles, or documentation
- Drafting emails or outreach messages
- Creating social media posts (LinkedIn, Twitter/X)
- Any task with category: `content`, `writing`, `outreach`, or `marketing`

## Inputs Required

- **What to write**: The content type and topic
- **Audience**: Who is this for?
- **Goal**: What action or response do we want?

## Workflow Steps

### Step 1: Check for Voice Samples

Look for the user's writing samples:

```
Knowledge/voice-samples/
```

If the directory exists, read 2-3 samples to understand the user's voice patterns.

If no samples exist, ask:
> "I don't have examples of your writing style yet. Would you like to:
> 1. Share a few examples of emails/posts you've written that you liked
> 2. Proceed with a neutral professional tone
> 3. Describe your preferred style (casual, formal, etc.)"

### Step 2: Check for Voice Guide

Look for an existing voice guide:

```
Knowledge/voice-guide.md
```

If it exists, read and apply those patterns. If not, extract patterns from samples (if available) or use defaults.

### Step 3: Gather Context

Read relevant context based on content type:

| Content Type | Context to Read |
|--------------|-----------------|
| Blog post | `Knowledge/` docs related to topic, `GOALS.md` for positioning |
| Email/outreach | Task file for recipient context, any related `Knowledge/` files |
| Social media | Recent posts in `Knowledge/voice-samples/`, `GOALS.md` for themes |

### Step 4: Draft Content

Apply these voice principles (override with user's voice guide if available):

**Structure:**
- Lead with the most interesting point, not throat-clearing
- Short paragraphs (2-3 sentences max)
- Clear, direct sentences

**Tone:**
- Conversational but professional
- Confident without being salesy
- Specific over vague

**Avoid:**
- "Key insight" / "Here's the thing" / "Let's be real"
- "I hope this email finds you well"
- Em dashes (use commas or periods)
- Excessive emojis or bullet points
- Rhetorical questions followed by answers

### Step 5: Present Draft with Options

Show the draft and ask:
> "Here's a draft. Let me know if you want me to:
> - Adjust the tone (more casual / more formal)
> - Shorten or expand any section
> - Change the structure or emphasis"

## Success Criteria

- [ ] Content matches user's voice (if samples available)
- [ ] Appropriate length for the format
- [ ] Clear call-to-action or next step
- [ ] No cliched AI phrases
- [ ] User approves or requests specific edits

## Creating a Voice Guide

If the user wants to establish their voice for future content, run this sub-workflow:

1. Ask for 5-10 writing samples (emails, posts, docs they liked)
2. Save samples to `Knowledge/voice-samples/`
3. Analyze patterns and create `Knowledge/voice-guide.md`:

```markdown
# Voice Guide

## Sentence Style
- [Length patterns]
- [Structure patterns]

## Openers
- [How they start emails]
- [How they start posts]

## Signature Phrases
- [Phrases they use often]

## Never Say
- [Phrases to avoid]

## Tone by Context
- Internal: [description]
- External: [description]
- Public: [description]
```

## Example Usage

**User:** "Write a LinkedIn post about our Q1 product launch"

**Agent workflow:**
1. Check `Knowledge/voice-samples/` - found 3 samples
2. Check `Knowledge/voice-guide.md` - exists, apply patterns
3. Read `Knowledge/q1-launch-notes.md` for context
4. Draft post using voice patterns
5. Present draft with adjustment options

---

*Related: See `examples/tutorials/voice-training.md` for detailed voice training instructions.*
