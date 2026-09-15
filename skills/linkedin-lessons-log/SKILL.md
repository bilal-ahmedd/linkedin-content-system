---
name: linkedin-lessons-log
description: "Use after real LinkedIn analytics or a completed li-audit post-mortem are available - distills concrete lessons from what worked and what didn't, and keeps a running lessons.md so future topics and drafts stop repeating the same mistakes."
---

# LinkedIn Lessons Log

The closing loop: `linkedin-agent:li-audit` finds what worked and what didn't in Bilal's actual posts; this skill turns those findings into standing lessons that `linkedin-topic-scout` and `linkedin-brand-gate` read before the next post gets planned or drafted. Without this step, every audit is a one-off insight that gets forgotten by the next post.

## When to run

After `linkedin-agent:li-audit` has actually produced findings from Bilal's real analytics or real published posts. If he hasn't run `li-audit` yet and just wants to know why one post underperformed, point him to `li-audit` first - this skill distills its output, it doesn't replace the analysis itself.

## What counts as a lesson

A lesson is a specific, evidence-backed pattern from Bilal's own data - never a generic LinkedIn-guide platitude restated as if it were something his data proved. "Post consistently" is not a lesson. "The two posts using a listicle-with-emoji format got a third of the engagement of the direct, no-emoji posts in the same month" is.

Pull 2 to 4 lessons per audit, each naming: what the pattern was, which post(s) showed it, and what to do differently next time.

## Maintaining the file

Read `~/.claude/linkedin/lessons.md` first if it exists. Append new lessons with the date and source post(s). If a new lesson sharpens or contradicts an older one (more data changes the picture), update that entry in place rather than leaving both - note in the output that an earlier lesson was superseded, and why. Keep the file scannable - a running list of near-duplicate lessons is as useless as no lessons file at all.

## Output

```
LESSONS UPDATED — [date]

New:
- [lesson] (source: [post/date])
- ...

Superseded/merged: [if any, and why]
```

## What this skill does not do

It doesn't analyze raw analytics itself - `li-audit` does that. It doesn't rewrite brand-positioning - persistent identity/positioning changes still go through `linkedin-brand-strategist` with Bilal's explicit approval. This is tactical, evidence-based memory of what has and hasn't worked, not identity.