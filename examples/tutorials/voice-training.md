# Training Your Agent to Write in Your Voice

How to make your Agent sound like you, not a generic AI.

## The Problem

Out of the box, Claude writes in "AI voice" - polished, formal, and generic. But when it drafts emails, posts, or docs for you, it should sound like *you*.

## The Solution: Voice Training

Give Claude examples of your actual writing, then have it extract patterns and apply them.

## Step-by-Step Setup

### Step 1: Collect Your Writing Samples

Gather 5-10 examples of your real writing. Mix of formats works best:

```
Knowledge/
├── voice-samples/
│   ├── email-to-colleague.md
│   ├── email-to-exec.md
│   ├── slack-messages.md
│   ├── linkedin-post.md
│   ├── blog-post-excerpt.md
│   └── product-spec-intro.md
```

**What makes good samples:**
- Emails you actually sent (not templates)
- Slack messages that got good responses
- Posts that felt authentically "you"
- Writing you're proud of

**What to avoid:**
- Heavily edited/formal documents
- Writing you copied from somewhere
- Samples that don't represent your natural style

### Step 2: Run Voice Analysis

Ask Claude to analyze your samples:

```
Read all files in Knowledge/voice-samples/ and analyze my writing style.
Extract specific patterns for:
1. Sentence structure and length
2. How I open and close messages
3. Words/phrases I use often
4. What I never say
5. Tone and formality level
6. How I structure arguments

Create a voice guide I can add to my agent instructions file (AGENTS.md)
```

### Step 3: Review the Voice Guide

Claude will produce something like:

```markdown
## Your Writing Voice

### Sentence Style
- Short sentences. Punchy. You rarely go over 15 words.
- Questions used to transition: "So what does this mean?"
- Em dashes avoided - you use commas or periods instead

### Openers
- Emails: Jump straight to the point, no "Hope you're well"
- Posts: Lead with a surprising fact or bold claim
- Specs: Start with the user problem, not the solution

### Signature Phrases
- "Here's the thing..."
- "Let's be real"
- "The short version:"
- Ends with clear next step or question

### What You Avoid
- "I hope this email finds you well"
- "Please don't hesitate to reach out"
- Bullet point lists in emails (prefer paragraphs)
- Emojis in professional context
- "Key insights" or "learnings"

### Tone Calibration
- To peers: Casual, direct, occasional humor
- To execs: Concise, data-first, clear ask
- Public posts: Confident but not salesy
```

### Step 4: Add to Your Agent Instructions

Add the voice guide to your agent instructions file (AGENTS.md) so it applies to all sessions:

```markdown
## Writing Style Guidelines

[Paste your generated voice guide here]

When drafting any writing for me:
1. Apply these patterns
2. Read a sample from Knowledge/voice-samples/ if unsure
3. Ask me to review before finalizing
```

### Step 5: Test and Refine

```
Draft an email to my VP about pushing the launch date back one week.
Use my voice - check Knowledge/voice-samples/ for reference.
```

Compare the output to how you'd actually write it. Give feedback:

```
Good start, but I wouldn't say "I wanted to reach out" - I'd just say
"Quick update on launch timing." Also too many bullet points, I usually
write in short paragraphs. Try again.
```

## The Subagent Workflow

For important writing, use this multi-step approach:

```
You: Help me write a blog post about our Q1 learnings

Claude (coordinator):
├── Subagent 1: Read Knowledge/voice-samples/ and extract style patterns
├── Subagent 2: Read Knowledge/q1-retro.md for content
├── Subagent 3: Research similar posts in the space
│
└── Main Claude: Synthesize into draft using your voice
```

**The prompt:**

```
I need to write a blog post about our Q1 learnings.

Before writing:
1. Read my voice samples in Knowledge/voice-samples/
2. Read Knowledge/q1-retro.md for the content
3. Draft an outline, then write

Match my voice exactly. Short sentences. No "key insights" or "learnings."
Lead with the most surprising thing we discovered.
```

## Voice Maintenance

### Monthly Refresh

Your voice evolves. Every month or two:

```
Read my recent writing in [location] and update my voice guide.
What patterns have changed? What's new?
```

### Context-Specific Voices

You might write differently in different contexts:

```markdown
## Voice by Context

### Internal Emails
- Very casual, incomplete sentences OK
- Humor welcome
- Can be blunt

### External/Customer
- Warmer, more complete sentences
- Still direct but softer edges
- Always end with clear next step

### Public Posts
- Confident, opinionated
- Short paragraphs, lots of white space
- Hook in first line
```

## Common Issues

**"It still sounds too formal"**
- Add more casual samples (Slack messages, quick emails)
- Explicitly list phrases to avoid
- Tell Claude: "Write like you're texting a smart colleague"

**"It's too casual for this context"**
- Add context-specific rules
- Specify: "This is for [audience], be more [formal/casual]"

**"It uses phrases I hate"**
- Build an explicit blocklist in your voice guide
- Call them out when you see them: "Never say X again"

**"The structure is wrong"**
- Add examples of how you structure different doc types
- Be explicit: "I always open emails with the ask, not context"

## Quick Start Template

Add this to your agent instructions file (AGENTS.md) and fill in:

```markdown
## My Writing Voice

### I sound like:
[Describe your tone in 2-3 sentences]

### I always:
- [Pattern 1]
- [Pattern 2]
- [Pattern 3]

### I never:
- [Anti-pattern 1]
- [Anti-pattern 2]
- [Anti-pattern 3]

### Sample phrases I use:
- "[Phrase 1]"
- "[Phrase 2]"

### For reference:
See Knowledge/voice-samples/ for examples of my actual writing.
```

---

*Back to: [Tutorials Home](README.md)*
