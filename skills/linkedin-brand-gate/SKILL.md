---
name: linkedin-brand-gate
description: "Run before any linkedin-agent skill (li-post, li-plan, li-profile, li-audit, li-carousel, li-repurpose, etc.) whenever a request touches Bilal's LinkedIn content, profile, or strategy - checks it against his approved brand-positioning before anything gets written or scored."
---

# LinkedIn Brand Gate

The `linkedin-agent` plugin skills (li-post, li-plan, li-profile, li-audit, li-carousel, li-repurpose, li-comment, li-dm, li-inbox, li-reply, li-human) are generic - they know how to write, plan, score, and audit LinkedIn content in general, but they don't know who Bilal is. This skill is the thin layer that makes them speak his brand instead of a generic one. It does not replace any linkedin-agent skill or duplicate its work - it runs first, then hands off.

## Mandatory first step

Read **[[brand-positioning]]** in full before evaluating anything. That document is the single source of truth for Bilal's identity, audience, skill tiers, approved claims, and content boundaries. Never infer positioning independently or from memory of a prior read - brand-positioning gets updated by `linkedin-brand-strategist` after Bilal's approval, so an old read can be stale.

## Checks to run on every request

**1. Skill-tier compliance.** Cross-check any technology, tool, or skill the content will claim expertise in against brand-positioning's three tiers:
- Primary (WordPress, WordPress Plugin Development, React.js, PHP, UI/UX, Performance Optimization) - safe to claim real, proven expertise.
- Secondary (Node.js, Systems and Workflows, n8n, AI Workflows, System Design) - frame as active growth/learning-in-public, never as established mastery.
- Low Priority (Make.com, Zapier, GoHighLevel, and similar) - never present as expertise, full stop, even in passing.

Flag any draft that claims Secondary-tier work as if it were Primary-tier proven, or that name-drops a Low-Priority tool as something Bilal has hands-on mastery of.

**2. Audience check.** Bilal's audience is high-growth founders and business owners broadly - not narrowed to any single vertical (e.g. "service businesses") unless he explicitly says so for that specific piece of content. Flag any draft that quietly narrows the stated audience.

**3. Never-fabricate check.** The only client/outcome evidence currently approved is: 4+ years (company roles only - LDNinjas, 360DigitalZ, Cybernetic Solutions, NeoDocto; Upwork freelance time is deliberately excluded from this figure, do not round it up), roughly 30+ projects across the US/UK/Europe/Dubai, and the one named WooCommerce case study ("six manual workflows into one connected system"). Flag any draft that invents a new specific number, client name, or result beyond what brand-positioning already lists as approved evidence - a vaguer true claim always beats a specific invented one.

**4. Content-pillar and topic check.** Cross-check the topic against brand-positioning's Topics to Own and Topics to Avoid. Topics to Own: real named project breakdowns in WordPress/React/PHP/UI-UX/Performance; systems-thinking and automation content framed as extending (not replacing) the engineering foundation; learning-in-public AI/n8n experiments explicitly framed as exploration. Topics to Avoid: content built around Zapier/UiPath/Gumloop/Make.com/GoHighLevel as tools of personal expertise; developer-only technical takes that don't translate to founder pain points (plugin-installation habits, generic WordPress speed tips, React performance nitpicks, headless WordPress debates).

**5. Direction check.** Bilal has confirmed the automation/AI-led positioning, anchored in the Primary engineering track record, is fixed and not up for reconsideration. Don't flag or second-guess the direction itself - only flag execution that fails to anchor it in the Primary-tier track record.

## Output

```
BRAND GATE: PASS | FLAG

[if FLAG, one line per issue, referencing the specific brand-positioning rule it violates]

Proceed to: [the linkedin-agent skill that should run next, e.g. li-post, li-plan, li-profile, li-audit]
```

On PASS, hand off directly to the named linkedin-agent skill with the request unchanged. On FLAG, surface the issues to Bilal and ask how he wants to proceed rather than silently rewriting around them - the brand document is his, not this skill's, to override.

## What this skill does not do

It does not write posts, score profiles, plan calendars, or humanize drafts - that's linkedin-agent's job. It does not update brand-positioning itself - that's `linkedin-brand-strategist`'s job, only after Bilal's explicit approval. It is a checkpoint, not a workflow.