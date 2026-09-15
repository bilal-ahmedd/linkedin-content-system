---
name: linkedin-topic-scout
description: "Use to source and propose new LinkedIn topic ideas that fit Bilal's approved brand positioning - searches for current angles, assigns each an ECG content type, checks them against his posting history and past lessons, and always gets his explicit approval before any topic moves to writing."
---

# LinkedIn Topic Scout

This skill's only job is to propose topics and get them approved. It never writes the post itself - that's `linkedin-agent:li-post` or `li-carousel`, after the gate.

## Before proposing anything

1. Read **[[brand-positioning]]** in full - Topics to Own, Topics to Avoid, content pillars, audience, current direction.
2. Read `~/.claude/linkedin/lessons.md` if it exists (written by `linkedin-lessons-log`) - don't propose an angle or format a past lesson already flagged as underperforming.
3. Read `~/.claude/linkedin/log.md` if it exists - don't propose something that's a near-repeat of a recent, published, OR already-drafted-but-unpublished post. A topic Bilal has approved and drafted counts as taken even before it goes live - check the log's status markers (published / drafted, not yet published), not just "published".
4. Run a fresh web search for current, publicly reported LinkedIn engagement and algorithm signals (dwell time, saves, first-hour comments, document/carousel performance, native vs. external-link posts, etc.) before proposing formats. Be honest in the output that LinkedIn does not publish its algorithm and public reporting is informed guessing, not confirmed policy - note the search date so staleness is visible later. When this reporting conflicts with Bilal's own actual results in `lessons.md` or a `li-audit` finding, his own data wins, always.

## ECG content type (mandatory field on every candidate)

Assign each candidate one of four ECG types, based on the topic's actual shelf life and stance - not by default, and not left for the writer to decide later:

- **Evergreen** - holds up if someone reads it 6 months from now. No time-bound phrasing ("this week", "just announced"). Best for durable systems-thinking and process lessons.
- **Evergreen + Controversial** - evergreen logic, but commits to a stance clearly enough to invite real disagreement in the comments. Best for a genuine unpopular-opinion angle Bilal actually holds.
- **Growth** - rides a narrow, timely window (a report that just dropped, a trend actively peaking). Needs real urgency and a punchy, save-worthy hook because the window closes. Not for anything that would read stale in a month.
- **Evergreen + Growth** - opens on a timely trigger (a current stat, a live event) but the body carries an evergreen lesson that still holds after the trigger stops being current. This is the most common fit for "here's a current report, and here's the durable lesson in it."

State the ECG type and a one-line reason it fits this specific topic - not just "Growth" with no justification. This carries through to `li-post`, which should honor it in execution (urgency for Growth, no time-bound language for Evergreen, a clear stance for Evergreen + Controversial).

## What to propose

3 to 5 topic candidates, each with:
- A specific angle, not a generic subject. "AI agents" is not an angle; "most things sold as AI agents today are webhooks with better marketing" is.
- Which content pillar it serves (Core: real project breakdowns / Supporting: systems-thinking and automation framed as extending the engineering foundation).
- ECG type (see above), with a one-line reason.
- Why now - tied to something specific: a real recent project, an observed pattern in Bilal's own work, a live audience pain point, or a genuinely current event/report (cited, not invented).
- Recommended format: text post if it's one claim, carousel if it has real sequence (steps, before/after, a countdown) - per `li-carousel`'s own guidance on when a carousel earns its place over a text post.

Never invent a statistic, trend, or "report" to justify a topic. If a number or trend is used as justification, it has to come from an actual search result, cited plainly.

## Mandatory approval gate

Present the candidates and stop. Do not pick "the best one" and proceed - Bilal chooses. Do not move to drafting until he names which topic(s) he wants written.

## Output

```
TOPIC CANDIDATES — sourced [date]

1. [Angle] — Pillar: [Core/Supporting] — ECG: [type + one-line reason] — Format: [text/carousel] — Why now: [...]
2. ...
3. ...

Algorithm context used: [1-2 lines, cited and dated — public reporting, not confirmed LinkedIn policy]
Lessons applied: [any relevant entries from lessons.md that shaped these picks, or "none yet logged"]
Already taken (excluded): [topics skipped because log.md shows them published or drafted]

Which one(s) do you want to move forward with?
```

On approval, hand the chosen topic, angle, and ECG type to `linkedin-brand-gate`, which checks it again at draft time and routes to `li-post` or `li-carousel`.