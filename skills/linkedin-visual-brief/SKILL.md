---
name: linkedin-visual-brief
description: "Use after a LinkedIn post draft exists (from li-post or li-carousel) and Bilal wants a matching visual - produces a copy-ready image-generation prompt built around scroll-stopping visual psychology, deep saturated brand colors, and a standing footer credit matching his real published style, optionally built around a photo Bilal attaches, without promising a specific engagement number nothing static can guarantee."
---

# LinkedIn Visual Brief

Takes a finished post draft and produces an image-generation prompt for the visual that runs alongside it. The visual supports the post's actual claim - it never gets built before the post text exists, and it never carries a claim the post itself doesn't make.

## Be upfront about what a visual can and can't do

No static image can be guaranteed to hit a specific engagement number - that depends on distribution, posting time, audience that day, and the algorithm's mood, none of which the image controls. This skill states the design principles it used to make the visual scroll-stopping; it does not promise a result. Say this plainly to Bilal rather than letting a specific percentage go unchallenged if he asks for one.

## Using an image Bilal attaches

Bilal may attach his own image (a headshot, a screenshot, a photo from a real project) to use in the visual. When one is attached for a given post, incorporate it rather than defaulting to a text-only or fully generated graphic - describe explicitly where it goes (e.g. his headshot in a corner or side panel next to the headline, a project screenshot as a supporting proof element) and how it should be treated (cropped, given a border, kept as-is) in both the Visual Brief and the final prompt. When no image is attached for a given post, keep producing the fully generated, text-and-shape visual as before - attaching one is optional per post, not a new standing requirement. Never fabricate or invent a stand-in photo when Bilal hasn't provided one; if a personal photo would clearly strengthen a specific visual, it's fine to ask whether he wants to attach one, rather than generating a generic placeholder person.

## Standing footer credit (every visual, no exceptions)

Confirmed against Bilal's actual published visual (2026-09-13, a real screenshot he shared): the footer reads **"Follow Bilal Ahmed | Systems Architect"** - "Systems Architect" plural, matching his approved brand-positioning and his real posts. This supersedes the earlier "System Architect" (singular) version, which was based on how he'd typed it in chat rather than his actual published copy - always defer to the real published example over a typed-in-chat spelling when the two ever conflict again.

Exact treatment, matched to his real style: centered, directly on the visual's background (not inside a separate filled color bar), positioned in the bottom margin just above the image edge, with a thin horizontal divider line in the accent color directly above it. "Bilal Ahmed" set in bold, "Systems Architect" in the same size but regular weight, both in off-white/light text so they read clearly against the dark teal background. This is a standing requirement on every visual - don't ask whether to include it.

## Scroll-stopping principles actually grounded in how people scroll

- **One focal claim.** The single number or line that matters most on the visual is the post's actual hook or core stat - not a decorative restatement, not a second idea competing for attention.
- **Mobile-first legibility.** Most LinkedIn scrolling happens on a phone, where the visual renders at thumbnail size in the feed before anyone taps in. Large type, high contrast, minimal text - if it's not legible at a glance shrunk to a few inches wide, it fails before anyone reads a word of the post.
- **Pattern interrupt over decoration.** A visual that looks like every other LinkedIn quote-card gets scrolled past exactly like one. Contrast, an unexpected layout, or a real data visual (if the post has real data) works harder than a stock-style graphic. A real attached photo of Bilal also works as a pattern interrupt against generic AI-generated graphics - use it that way when one's provided.
- **No fabricated specifics.** Never invent a chart, screenshot, workflow diagram, or number that isn't actually true of the post's content - same never-fabricate rule as every writing skill in this system.

## Reference layout (matches Bilal's real published style)

His actual visuals use: a numbered step or stat list down the body (numbered circles, an icon, a short bold label + one line of plain description, an optional colored status indicator), a bold headline stat/claim across the top in a bright accent color pill against the dark teal ground, an optional "TOP TAKEAWAY" callout box near the bottom, and the footer credit as its own line beneath a thin divider. Reuse this structural language when the post's content fits it (a numbered breakdown, a ranked list, a checklist) rather than inventing a new layout style each time - consistency across visuals is itself part of his brand.

## Brand colors - deep and saturated, never faded

Confirmed by Bilal: **`#10ADAD`** and **`#0B666A`** are the anchor colors and must stay visually dominant in every visual - the ground, the primary text, or the primary shape fills. Bilal has explicitly said complementary accent colors can be used alongside them for a more attractive, scroll-stopping result (e.g. a bright highlight color on one stat, a warm accent on a callout) - that's fine as long as the two brand colors remain the dominant, recognizable palette rather than being crowded out. Don't invent a palette that replaces the brand colors entirely; a genuine palette change still goes through `linkedin-brand-strategist` and brand-positioning, not a one-off visual brief.

Bilal explicitly corrected this (2026-09-13): every color used, brand colors and any complementary accent alike, must render deep and richly saturated - never pastel, washed-out, faded, or low-saturation. When writing the final image-generation prompt, describe colors with words like "deep", "rich", "saturated", "solid" rather than leaving saturation to the image tool's default, and explicitly call out "no faded or pastel tones" in the prompt itself so this doesn't have to be corrected again per visual.

## Output

```
## Visual Brief

Canvas: [aspect ratio - 1080x1350 vertical is the strongest mobile real estate]
Attached image used: [describe it and its placement/treatment, or "none - fully generated"]
Headline text (verbatim, pulled from the post's actual hook or core number): [...]
Supporting text (minimal, only what's needed): [...]
Footer: "Follow Bilal Ahmed | Systems Architect" - centered, on-background, bold name + regular title, thin divider above
Layout: [...]
Typography: [...]
Spacing: [...]
Brand colors used: #10ADAD and #0B666A as the dominant palette, deep and saturated [+ any complementary accent, named, also deep/saturated]
Design principle applied: [which of the above this visual leans on, and why it fits this specific post]

Note: designed for scroll-stopping using the principles above. No visual can be promised a specific engagement percentage.

[Full copy-ready image-generation prompt, ready to paste into an image tool with no further editing - the footer credit must be explicitly described in this prompt exactly as specified above, every color must be described as deep/saturated/solid with an explicit "no faded or pastel tones" instruction, and if an image was attached, the prompt must describe exactly how to incorporate it]
```