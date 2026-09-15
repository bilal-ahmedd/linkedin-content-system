---
name: linkedin-workflow-router
description: "Use when Bilal asks for LinkedIn help in plain language (find me a topic, write a post, plan my week, score my profile, why isn't this post working, turn this into a carousel, handle this comment/DM) and it isn't obvious which skill to invoke - now covers the full topic-to-lessons loop."
---

# LinkedIn Workflow Router

Bilal shouldn't have to know which of the `linkedin-agent` plugin's eleven skills, or which of his own custom LinkedIn skills, a request needs. This skill reads his plain request, routes it to the right one, and sequences `linkedin-brand-gate` in front of anything that produces new content, claims, or scoring, so every output stays inside his approved positioning.

## The full loop, end to end

```
linkedin-topic-scout       propose topics, wait for Bilal's approval
        |
linkedin-brand-gate        check the approved topic/angle against brand-positioning + history
        |
linkedin-agent:li-post     write the post (needs voice.md - already built)
  or li-carousel
        |
linkedin-visual-brief      build the matching scroll-stopping visual prompt
        |
  ... Bilal posts it on LinkedIn himself ...
        |
linkedin-agent:li-audit    once real analytics/results are pasted back, post-mortem them
        |
linkedin-lessons-log       distill lessons, feed them back into lessons.md
        |
  (linkedin-topic-scout and linkedin-brand-gate read lessons.md on the next cycle)
```

No step in this chain publishes anything - every skill in this system produces text or a prompt for Bilal to use himself.

## Routing table

| Bilal says something like... | Route |
|---|---|
| "find me a topic" / "what should I post about" / "research topics for my brand" | `linkedin-topic-scout` (proposes candidates, waits for his pick, then hands off to the gate) |
| "write a post about X" / "turn this idea into a post" (topic already chosen) | `linkedin-brand-gate` -> `linkedin-agent:li-post` |
| "give it a visual" / "make a visual for this post" / "design something to go with this" | `linkedin-visual-brief` (needs a finished post draft as input) |
| "plan my week" / "what should I post this week" | `linkedin-brand-gate` -> `linkedin-agent:li-plan` |
| "score my profile" / "is my profile good" / attaches a profile export | `linkedin-brand-gate` -> `linkedin-agent:li-profile` |
| "why isn't this post working" / "analyze this post's performance" / pastes real analytics | `linkedin-brand-gate` -> `linkedin-agent:li-audit`, then offer `linkedin-lessons-log` to bank the findings |
| "turn this post into a carousel" | `linkedin-brand-gate` -> `linkedin-agent:li-carousel` |
| "repurpose this" / "reuse this old post" | `linkedin-brand-gate` -> `linkedin-agent:li-repurpose` |
| "reply to this comment" / "what should I say back" | `linkedin-agent:li-comment` or `linkedin-agent:li-reply` (brand-gate optional - low fabrication risk, but still check tone against brand-positioning's voice) |
| "draft a DM to this person" | `linkedin-brand-gate` -> `linkedin-agent:li-dm` |
| "clean up my inbox" / "what messages need a reply" | `linkedin-agent:li-inbox` (no gate needed - it's triage, not content) |
| "does this sound too AI-generated" / "humanize this draft" | `linkedin-agent:li-human` directly (no gate needed - it's a mechanical pass, not a claims check) |
| Request is thin ("post about AI", "write something") with no specific angle already chosen | Route to `linkedin-topic-scout` first rather than straight to `li-post` - a topic is not an angle, and scout is where angles get sourced and approved. |

## Sequencing rule

Any route that creates new written claims, scores something, or diagnoses performance goes through `linkedin-brand-gate` first. Purely mechanical or triage skills (`li-human`, `li-inbox`) skip the gate - there's nothing brand-sensitive to check. `linkedin-visual-brief` also skips the gate itself since it only visualizes a post that already passed the gate - it doesn't introduce new claims of its own, though it must not add any claim the underlying post doesn't already make.

If `linkedin-brand-gate` returns FLAG, stop and resolve that with Bilal before calling the downstream skill - don't run both in the same breath and hope the flag sorts itself out.

## When routing is genuinely ambiguous

If a request could reasonably map to two different skills (for example, "help with this old post" could mean `li-audit` or `li-repurpose`), ask which one in one short question rather than guessing - the two skills produce very different outputs and guessing wrong wastes a full pass.

## Being honest about "the algorithm"

If Bilal asks this system to guarantee reach, engagement, or a specific result because it "follows the LinkedIn algorithm," say plainly that LinkedIn doesn't publish its algorithm and no skill can guarantee an outcome - `linkedin-topic-scout` researches current public reporting on what tends to perform, and `linkedin-lessons-log` tracks what has actually worked for his own account, but neither is a guarantee. His own data in `lessons.md`, once it exists, is the most reliable signal this system has - more reliable than any generic algorithm claim.

## What this skill does not do

It doesn't write, score, plan, research topics, or audit anything itself - it only decides which existing skill should, and in what order. It also doesn't replace `linkedin-brand-gate`'s judgment; if the gate flags something, the router doesn't override that flag to force a route through anyway.