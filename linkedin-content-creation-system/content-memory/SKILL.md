---
name: content-memory
description: >-
  Defines and governs CONTENT_MEMORY — the permanent historical record of every LinkedIn post Bilal has published, what actually happened to it, and what was learned. Use this whenever creating a new CONTENT_MEMORY document from scratch, validating or restructuring an existing one against the required schema, resolving what belongs in a post record versus what belongs in CONTENT_DNA, or when any skill needs to know exactly how to read from or write to CONTENT_MEMORY correctly (required fields per record, who is allowed to write vs. only read, the never-delete rule). This is a schema-and-governance skill, not an analysis skill — it does not itself analyze a post's performance (that's linkedin-performance-analyst) and does not itself decide what graduates into validated knowledge (that's linkedin-learning-engine). Trigger it whenever CONTENT_MEMORY itself — its format, its integrity, or a rule about how it should be updated — is the thing in question.
---

# CONTENT_MEMORY — Shared Historical Record

CONTENT_MEMORY is the historical memory of Bilal's LinkedIn content system: it records what actually happened, post by post. It sits primarily behind `linkedin-performance-analyst`, which writes to it after analyzing each post, and is read by `linkedin-learning-engine` when aggregating evidence across the account's history.

## The one distinction everything else follows from

**CONTENT_MEMORY records history. CONTENT_DNA (and VISUAL_DNA) record validated knowledge.** These are not the same document doing double duty, and conflating them breaks the whole pipeline:

- CONTENT_MEMORY is a factual log — every post that happened, whether it worked or not, whether the result made sense or not. It grows by one entry per post, indefinitely, and nothing in it needs to be "proven" to belong there.
- CONTENT_DNA/VISUAL_DNA are curated, evidence-gated playbooks — only patterns that have earned a confidence level live there, and they change slowly, deliberately, through `linkedin-learning-engine`'s aggregation and `linkedin-content-analyst`'s writes.

A post record belongs in CONTENT_MEMORY the moment it's analyzed, full stop. A *pattern* only belongs in CONTENT_DNA/VISUAL_DNA once enough CONTENT_MEMORY entries support it. If you're ever tempted to add a "confidence" judgment call directly into a CONTENT_MEMORY post record beyond citing what the Performance Analyst concluded for that one post, that's a sign you're drifting into CONTENT_DNA's job.

## Post record format

Every published post gets a record with all of these fields:

- **Post ID** — permanent once assigned, e.g. `POST-014`.
- **Date** — publish date.
- **Topic**
- **Angle**
- **Skill Tier** — Primary / Secondary / Low-priority, per `brand-positioning`.
- **Content Type**
- **Selected DNA** — the CONTENT_DNA structure ID actually used (e.g. `DNA-02 v1`).
- **Selected Visual DNA** — the VISUAL_DNA pattern ID actually used, if any.
- **Hook** — the actual hook mechanism used.
- **Post Reference** — a link or identifier for the published post itself.
- **Performance** — impressions, reach, likes, comments, reposts, saves, profile visits, followers, clicks, leads, calls, clients. Record whatever's actually available; leave the rest blank rather than guessing.
- **Outcome** — a plain-language summary of what happened (e.g. "well above baseline reach, average engagement, one qualified lead").
- **Performance Analyst Notes** — the FACT/OBSERVATION/HYPOTHESIS findings from the linked Performance Analyst report for this post.
- **Learning** — what this post contributed to the account's understanding, if anything — can be "none yet, watching" for a post that hasn't revealed a clear pattern.
- **Confidence** — the confidence level attached to whatever learning is recorded (Proven / Strong / Emerging / Experimental / Unknown), citing the Performance Analyst's or Learning Engine's assessment — not a fresh judgment made while writing the memory entry.
- **Experiments Connected** — any CONTENT_EXPERIMENTS entry (e.g. `EXP-04`) this post is a data point for.

## Who reads, who writes

- **Performance Analyst** — writes and updates CONTENT_MEMORY. This is its primary output, one entry per post analyzed.
- **Learning Engine** — reads across CONTENT_MEMORY to aggregate evidence, detect patterns, and build recommendations for CONTENT_DNA/VISUAL_DNA changes; doesn't edit CONTENT_MEMORY's post records directly, but can mark an entry's Learning/Confidence fields as superseded when new evidence changes the picture (see below).
- **Content Analyst, Content Strategist, Content Writer** — may read CONTENT_MEMORY for context but don't write to it; their relationship is with CONTENT_DNA/VISUAL_DNA, not the raw history.

## Never delete

Never delete a historical record unless Bilal explicitly instructs it. This holds even when:

- A recorded learning turns out to be wrong once more data comes in — mark it **superseded**, with a note pointing to what superseded it and when, rather than removing or rewriting it. The fact that the system's understanding changed is itself useful history.
- A post performed unusually and the anomaly never resolved into a pattern — it stays, unexplained, rather than being cleaned up for tidiness.
- An experiment connected to a post concluded inconclusively — the record stays; log the inconclusive result rather than erasing the attempt.

If Bilal does explicitly ask for a record to be removed, that's the one path deletion can happen through — never proactively, never for cleanup, never because an entry looks redundant.

## Scale

CONTENT_MEMORY will grow indefinitely as a long-running account accumulates posts. When it gets large enough that reading the whole thing isn't practical, the Learning Engine should work from the relevant slice (recent entries, entries matching a topic/structure/tier under review) rather than the full history each time — but the underlying document itself is never trimmed or archived away without Bilal's say-so.
