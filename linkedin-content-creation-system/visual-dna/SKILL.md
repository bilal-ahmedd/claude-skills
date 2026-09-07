---
name: visual-dna
description: >-
  Defines and governs VISUAL_DNA — the shared LinkedIn visual-pattern knowledge document, and the home of Bilal's approved brand colors. Use this whenever creating a new VISUAL_DNA document from scratch, validating or restructuring an existing one against the required schema, resolving a conflict between new visual evidence and an already-documented pattern, or when any skill needs to know exactly how to read from or write to VISUAL_DNA correctly (which fields are required per pattern, how visual IDs must be versioned, who is allowed to write vs. only read, what the current approved brand colors are). This is a schema-and-governance skill, not an analysis skill — it does not itself analyze visuals (that's linkedin-content-analyst) and does not itself pick a visual for a new post (that's the Content Strategist). Trigger it whenever VISUAL_DNA itself — its format, its integrity, brand colors, or a rule about how it should be updated — is the thing in question.
---

# VISUAL_DNA — Shared Visual Knowledge

VISUAL_DNA is the visual counterpart to CONTENT_DNA, sitting in the same pipeline: `Content Analyst → Content Strategist → Content Writer`, with the Performance Analyst and Learning Engine feeding evidence back in. It stores validated visual patterns from Bilal's actual LinkedIn content — not generic design advice — so those skills don't have to re-derive what visually works from scratch every time.

## Brand colors

**Primary:** `#10ADAD`
**Secondary:** `#0B666A`

These are the default visual identity for every pattern in this document. Every skill that reads VISUAL_DNA should treat them as fixed unless Bilal has explicitly approved a change — a color swap is a strategic change (see `linkedin-brand-strategist` / `linkedin-learning-engine`'s approval-required list), never something a single post or a single visual pattern update can alter on its own. If a pattern entry ever records a deviation from these colors, it should be flagged as a deviation, not treated as a quiet update to the palette.

## The one rule everything else follows from

VISUAL_DNA is built primarily from Bilal's own historical visuals and their performance — it is not a generic design-best-practices library. A layout trend, a design account's advice, or a general aesthetic preference can justify adding an **Experimental Pattern** to test. It does not get to become Proven or Strong just because it looks good or is commonly recommended — only Bilal's own repeated results can promote something that far. If you're ever about to add something to VISUAL_DNA and the only justification is "this is generally good design," it belongs in Experimental Patterns, clearly labeled as untested.

## Document structure

```markdown
# VISUAL_DNA

## LAST UPDATED
[date of the most recent change]

## BRAND COLORS
Primary: #10ADAD
Secondary: #0B666A
[note any explicitly approved deviation here, with date and reason]

## DATA COVERAGE
Number of visuals analyzed: [count]
[date range and any coverage notes — carousels vs. single images, gaps, etc.]

## CONFIDENCE SUMMARY
### PROVEN PATTERNS
### STRONG PATTERNS
### EMERGING PATTERNS
### EXPERIMENTAL PATTERNS
### UNKNOWN

## WEAK PATTERNS

## AVOID LIST

## CHANGELOG
```

## Visual pattern entries

Every pattern the Content Analyst has identified lives under **Confidence Summary**, filed under the subsection matching its current confidence — not in one flat list with confidence as a field. When a pattern's confidence changes, it moves subsection; it isn't duplicated or re-created. Each entry carries all of these fields:

- **Visual ID** — e.g. `VISUAL-01`. Permanent once assigned — see the versioning rule below.
- **Name** — short, descriptive.
- **Confidence** — Proven / Strong / Emerging / Experimental / Unknown (redundant with the subsection it sits in, but keep the field too — it makes the entry self-contained if ever excerpted on its own).
- **Evidence** — the actual count and type of posts behind it, e.g. "4 of 6 high-performing carousel posts, Mar–Jun 2026."
- **Best Used For** — what kind of post or message this pattern fits.
- **Canvas** — dimensions/aspect ratio this pattern is built for (e.g. 1:1, 4:5, carousel 1080×1350).
- **Layout** — the concrete arrangement of elements.
- **Hierarchy** — what the eye hits first, second, third.
- **Typography** — faces, sizes, weight patterns actually observed.
- **Spacing** — margins, padding, whitespace conventions.
- **Color Usage** — how the brand colors (or an approved deviation) actually appear in this pattern.
- **Information Density** — how much text/content per slide or image.
- **Illustration/Icon Guidance** — what kind of supporting visual elements this pattern uses, if any.
- **Avoid** — what weakens this specific pattern if done wrong.
- **Performance Evidence** — the actual metrics tied to posts using this pattern, not just a qualitative impression.

Scaffold the Confidence Summary subsections even when empty — an empty "Proven Patterns" section signals "not enough visual data yet," which is itself useful downstream.

## Weak patterns and the avoid list

**Weak Patterns** — visual approaches associated with weaker-performing posts. Phrase these as observed association ("carousels with more than 8 words per slide are associated with lower completion in this sample"), never as proven cause unless the evidence has genuinely crossed into Proven/Strong territory for that specific claim.

**Avoid List** — a short, standing list of visual mistakes to never repeat, drawn from weak patterns that have shown up repeatedly enough to be worth a blanket rule (e.g. "never use a third accent color outside the two brand colors without explicit approval").

## Versioning visual IDs

Downstream skills depend on visual IDs staying stable — the Content Strategist selects an ID, and the Content Writer builds its image-generation prompt from whatever that ID specifies. Breaking an ID silently breaks that chain invisibly, which is worse than an obvious error.

- Never rename or renumber an existing ID.
- If a pattern changes substantially enough that following the old description would now be wrong, don't overwrite it — version it: the original stays `VISUAL-01 v1`, the revision becomes `VISUAL-01 v2`, and note in the Changelog why and roughly when.
- Assign new patterns the next unused ID number; don't reuse retired numbers.

## Who reads, who writes

- **Content Analyst** — writes and updates VISUAL_DNA. This is one of its primary outputs, and the only skill that touches the document directly.
- **Content Strategist** — reads VISUAL_DNA and selects the most appropriate existing pattern for a given post's visual; does not invent a new one on the spot.
- **Content Writer** — reads VISUAL_DNA and builds its image-generation prompt from whatever pattern the Strategist selected, including the current brand colors from this document.
- **Performance Analyst** — supplies new visual performance evidence from individual posts; doesn't edit the document directly.
- **Learning Engine** — aggregates visual evidence across CONTENT_MEMORY and experiments, and recommends a change when evidence is sufficient; the recommendation still routes through the Content Analyst, which is what actually writes it in and adds the Changelog entry. Any recommendation touching brand colors or "major visual identity" is approval-required, not automatic — flag it rather than acting on it.

## Update rule — never from one post

Never change the visual identity, or promote a pattern's confidence, because of a single post. A brand color swap or a "this layout works" call needs evidence from repeated posts, not one lucky carousel. One unusual result is worth noting in Weak Patterns or Experimental Patterns and watching — not acting on immediately.

## Changelog

For every meaningful update, add an entry — never edit or remove a past one:

```
Date: [when this update happened]
Old Understanding: [what VISUAL_DNA said before]
New Evidence: [what came in — count, source]
New Understanding: [what changed]
Confidence: [Proven / Strong / Emerging / Experimental / Unknown]
Reason: [why this update was made]
```

This is the audit trail for the whole document — anyone reading it later should be able to see why the visual system looks the way it does without reconstructing the reasoning from scratch.
