---
name: content-dna
description: >-
  Defines and governs CONTENT_DNA — the shared LinkedIn content knowledge document that sits between the Content Analyst, Content Strategist, Content Writer, and Performance Analyst skills. Use this whenever creating a new CONTENT_DNA document from scratch, validating or restructuring an existing one against the required schema, resolving a conflict between pieces of evidence (e.g. new performance data vs. an older established pattern), or when any skill needs to know exactly how to read from or write to CONTENT_DNA correctly (which sections exist, which fields are required, how structure IDs must be versioned, who is allowed to write vs. only read). This is a schema-and-governance skill, not an analysis skill — it does not itself analyze posts (that's linkedin-content-analyst) and does not itself pick a structure for a new post (that's the Content Strategist). Trigger it whenever CONTENT_DNA itself — its format, its integrity, or a rule about how it should be updated — is the thing in question.
---

# CONTENT_DNA — Shared Content Knowledge

CONTENT_DNA is the knowledge layer connecting the user's LinkedIn content pipeline: `Content Analyst → Content Strategist → Content Writer`, with the Performance Analyst feeding new evidence back in. It exists so those skills don't have to re-derive what works from scratch every time — but that only holds if the document stays disciplined about what counts as evidence.

## The one rule everything else follows from

CONTENT_DNA is built primarily from the user's own historical LinkedIn content and performance data — it is not a generic best-practices template library. A tactic a LinkedIn influencer recommends, or something a general algorithm-research skill turns up, can justify adding an **Experimental Pattern** to test. It does not get to become a proven or strong pattern just because it's popular advice — only the user's own repeated results can promote something that far. If you're ever about to add something to CONTENT_DNA and the only justification is "this is commonly recommended," it belongs in section 7 (Experimental), clearly labeled as untested, not anywhere else.

## Document structure

A CONTENT_DNA document follows this exact header layout. When creating one from scratch, scaffold every section even if some start nearly empty — an empty "Topic DNA" section signals "not enough data yet," which is itself useful information for downstream skills.

```markdown
# CONTENT_DNA

## LAST UPDATED
[date of the most recent change]

## DATA COVERAGE
Number of posts analyzed: [count]
[date range and any other coverage notes — e.g. gaps, platforms, formats included]

## CONFIDENCE SUMMARY
### PROVEN STRUCTURES
### STRONG STRUCTURES
### EMERGING STRUCTURES
### EXPERIMENTAL STRUCTURES

## HOOK DNA

## TOPIC DNA

## VOICE DNA

## FORMATTING DNA

## WEAK PATTERNS

## EXPERIMENTAL PATTERNS

## CONTENT PRINCIPLES

## CHANGELOG
```

### Confidence Summary and Content Structures

Every structure the Content Analyst has identified lives under **Confidence Summary**, filed under the subsection matching its current confidence — not in one flat list with confidence as a field. When a structure's confidence changes, it moves to a different subsection; it does not get duplicated or re-created under a new one. Each structure entry carries:

- **ID** — e.g. `DNA-01`. See the versioning rule below; IDs are permanent once assigned, regardless of which confidence subsection they currently sit under.
- **Name** — short, descriptive.
- **Evidence** — the actual count and type of posts behind it, e.g. "6 of 10 high-performing posts, Jan–Jun 2026."
- **Best For** — topics/content purposes this structure suits.
- **Sequence** — the exact logical flow, step by step.
- **Hook Pattern** — the opening mechanism this structure pairs with.
- **Body Pattern** — how information progresses through the middle.
- **Ending Pattern** — how it typically concludes.
- **Formatting** — relevant formatting traits.
- **Avoid** — what weakens this structure specifically.

### Hook DNA

Successful hook mechanisms actually observed in the user's data — problem-first, surprising realization, personal mistake, result-first, contrarian observation, curiosity, specific situation, or whatever else the data shows. These are patterns *from this account's data*, not a universal claim that a mechanism works for everyone — say so if it's ever at risk of being read that way.

### Topic DNA

- Topics that repeatedly perform well.
- Topics with weak performance.
- Topics not tested enough to have a signal either way.
- Audience-relevant topics (even if not yet proven, if there's a clear reason to believe the user's audience cares).
- Topic/structure combinations that look promising together.

### Voice DNA

Tone, sentence style, vocabulary, technical depth, personality, storytelling style, confidence level, conversational style — described specifically enough that someone could imitate the user's actual voice from this section alone, not generic "professional but approachable" filler.

### Formatting DNA

Paragraph length, line breaks, whitespace, lists, bullets, numbers, emoji usage, technical formatting conventions. Only record what's actually observed in the user's posts — don't fill this section with formatting "best practices" that weren't actually seen in the data.

### Weak Patterns

Patterns associated with weaker-performing posts. Always phrase these as **observed association**, e.g. "Posts opening with a generic industry statistic are associated with lower engagement in this sample" — never as a proven cause, unless the evidence has genuinely crossed into Proven/Strong territory for that specific claim.

### Experimental Patterns

New approaches not yet validated — including anything sourced from outside research or general advice (per the one rule above). Every entry here must stay visibly labeled as experimental; nothing quietly graduates out of this section without new evidence from the user's own posts.

### Content Principles

Durable, cross-cutting takeaways that aren't tied to one specific structure, hook, or topic — things that seem true across most or all of what's working, stated plainly enough to guide a judgment call the other sections don't directly cover. Keep this section short; it's for genuinely cross-cutting principles, not a catch-all for anything that didn't fit elsewhere.

### Changelog

For every meaningful update, add an entry — never edit or remove a past entry:

```
Date: [when this update happened]
Old Understanding: [what CONTENT_DNA said before]
New Evidence: [what came in — count, source, e.g. "linkedin-learning-engine recommendation, EXP-04 concluded"]
New Understanding: [what changed]
Confidence: [Proven / Strong / Emerging / Experimental]
Reason: [why this update was made]
```

The changelog is the audit trail for the whole document — if a future session or a skeptical read ever asks "why does CONTENT_DNA believe this," the changelog should have the answer without anyone needing to reconstruct it from memory.

## Versioning structure IDs

Downstream skills depend on structure IDs staying stable — the Content Strategist selects an ID, and the Content Writer executes whatever that ID specifies. Breaking an ID silently breaks that chain invisibly, which is worse than an obvious error.

- Never rename or renumber an existing ID.
- If a structure changes substantially enough that following the old description would now be wrong, don't overwrite it — version it: the original stays `DNA-01 v1`, the revision becomes `DNA-01 v2`, and note in the document why the change happened and roughly when.
- Assign new structures the next unused ID number; don't reuse retired numbers.

## Who reads, who writes

- **Content Analyst** — writes and updates CONTENT_DNA. This is its primary output, and the only skill that touches the document directly.
- **Content Strategist** — reads CONTENT_DNA and selects the most appropriate existing structure/pattern for a given piece of content; does not invent new structures on the spot.
- **Content Writer** — reads CONTENT_DNA and executes whatever structure the Strategist selected; does not deviate from it based on its own judgment about what "should" work.
- **Performance Analyst** — supplies new performance evidence from individual posts; doesn't edit the document directly.
- **Learning Engine** — aggregates evidence across CONTENT_MEMORY, experiments, and Performance Analyst reports, and *recommends* a change (per the OLD/NEW/CONFIDENCE format it uses) when evidence is genuinely sufficient. It doesn't write to CONTENT_DNA either — the recommendation still routes through the Content Analyst, which is what actually adds the Changelog entry and moves a structure between confidence subsections.

If asked to act as one of the downstream skills while this skill is active, keep those boundaries — e.g. don't let a Strategist-role request quietly invent a brand-new content structure instead of selecting from what's already documented; flag that a new structure would need to go through the Analyst/evidence path first.

## Evidence hierarchy for conflicts

When new evidence conflicts with what's already documented, resolve it in this order, highest priority first:

1. Recent, repeated performance data (the freshest signal, seen more than once).
2. A larger historical sample (more posts, even if slightly older).
3. Consistency of the pattern across different conditions/topics.
4. A single successful post (weak on its own — a data point, not a pattern).
5. Generic LinkedIn advice (lowest priority — informative for generating experiments, never enough on its own to override the user's actual results).

Generic advice does not get to override strong evidence from the user's own content without a documented, specific reason — if you're ever tempted to let it, that's a sign the change belongs in Experimental Patterns instead of overriding an established entry.

## Updating instead of overwriting

Never regenerate CONTENT_DNA from scratch when new evidence comes in — that erases the confidence history and risks breaking ID stability for anything already depending on it. Instead: read what exists, compare the new evidence against it, adjust confidence levels up or down as warranted, add genuinely new patterns, and leave everything else untouched. A single unusual post is never grounds for rewriting an established pattern — note it, don't act on it yet.
