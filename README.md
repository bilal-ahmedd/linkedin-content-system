# linkedin-content-system

A Claude skills system for managing LinkedIn strategy, content, and engagement end-to-end — from topic discovery to publishing to post-mortem analysis.

## Structure

```
skills/
├── brand-positioning/          # Source of truth: approved identity, audience, skill hierarchy, current profile copy
├── linkedin-brand-gate/        # Runs before any content/profile/strategy skill fires; checks requests against brand-positioning
├── linkedin-workflow-router/   # Entry point for plain-language requests; routes to the right skill below
├── linkedin-topic-scout/       # Sources new topic ideas, tags them by content type, requires explicit approval before writing
├── linkedin-lessons-log/       # Turns published-post analytics into a running lessons.md that future drafts must respect
├── linkedin-visual-brief/      # Generates image-gen prompts to accompany a finished post draft
└── linkedin-agent/             # Content + engagement pipeline (installed marketplace plugin)
    ├── li-post/                 # Idea → LinkedIn post (21 hook formulas, 3 hook options + 1 draft)
    ├── li-carousel/             # Idea → slide-by-slide carousel + PDF
    ├── li-repurpose/            # Long-form asset (video/newsletter/transcript) → a week of posts
    ├── li-plan/                 # Weekly content calendar + engagement list
    ├── li-human/                # Strips AI writing fingerprints, runs a 5-check detection pass before publishing
    ├── li-profile/              # Scores a LinkedIn profile out of 100 against a 12-part rubric, rewrites weak sections
    ├── li-audit/                # Post-mortem on published posts/analytics — what worked, what to stop doing
    ├── li-inbox/                # Triages DMs and connection requests into leads/recruiters/peers/spam
    ├── li-comment/              # Drafts comments on other people's posts
    ├── li-reply/                # Drafts replies to comments on your own posts
    └── li-dm/                   # Connection notes and DM follow-ups
```

## How it flows

1. A request comes in through **linkedin-workflow-router**, which decides which skill should handle it.
2. **linkedin-brand-gate** checks the request against **brand-positioning** before any writing happens.
3. New ideas start in **linkedin-topic-scout** and need explicit approval before moving to drafting.
4. Drafting happens in the relevant `linkedin-agent` skill (`li-post`, `li-carousel`, or `li-repurpose`).
5. Every draft passes through **li-human** before it's considered publish-ready.
6. After publishing, **li-audit** reviews performance, and **linkedin-lessons-log** feeds the takeaways back so future topics and drafts don't repeat the same mistakes.
7. **linkedin-visual-brief**, **li-inbox**, **li-comment**, **li-reply**, **li-dm**, and **li-profile** support the pipeline as needed (visuals, inbox triage, engagement, profile upkeep).

## Notes

- `brand-positioning` is read-only from every other skill's perspective — it's written and updated only after explicit approval.
- The `linkedin-agent/*` skills mirror an installed marketplace plugin (`linkedin-agent`); they're included here for version control and reference.
