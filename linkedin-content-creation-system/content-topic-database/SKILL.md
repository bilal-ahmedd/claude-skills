---
name: content-topic-database
description: >-
  Defines and governs CONTENT_TOPIC_DATABASE — the shared record of every LinkedIn topic Bilal has considered, approved, scheduled, published, or rejected, kept to prevent repetitive content. Use this whenever creating a new CONTENT_TOPIC_DATABASE from scratch, validating or restructuring an existing one against the required schema, resolving a status question (is this topic IDEA/APPROVED/PLANNED/PUBLISHED/REJECTED), or when any skill needs to know exactly how to read from or write to it correctly (required fields per record, the status lifecycle, who approves what, who is allowed to write vs. only read). This is a schema-and-governance skill, not a research skill — it does not itself find new topics (that's linkedin-topic-researcher) and does not itself pick a topic for a brief (that's the Content Strategist). Trigger it whenever CONTENT_TOPIC_DATABASE itself — its format, its integrity, or a rule about how it should be updated — is the thing in question.
---

# CONTENT_TOPIC_DATABASE — Shared Topic History

CONTENT_TOPIC_DATABASE exists for one reason: prevent repetitive LinkedIn content and maintain topic history. It sits primarily behind `linkedin-topic-researcher`, which checks every new candidate against it before recommending anything, but it's a shared reference — the Content Strategist and Learning Engine also read from it (topic-level pattern history, respectively).

## Record format

Every topic gets a record with all of these fields:

- **Topic ID** — e.g. `TOPIC-001`. Permanent once assigned — see the versioning rule below.
- **Topic** — the core subject.
- **Specific Angle** — the particular take, not just the general subject (this is what actually differentiates two records that share a topic).
- **Content Pillar** — which of Bilal's approved content pillars (from `brand-positioning`) this falls under.
- **Skill Tier** — Primary / Secondary / Low-priority, per `brand-positioning`'s hierarchy.
- **Content Type** — e.g. project breakdown, opinion, technical explainer, learning-in-public, case study.
- **Date Approved** — when Bilal approved this topic, if it reached that stage.
- **Date Published** — when it actually went live, if it reached that stage.
- **Status** — see the lifecycle below.
- **Performance Reference** — a pointer into CONTENT_MEMORY or the relevant Performance Analyst report, once published.
- **Post Reference** — a link or identifier for the actual published post, once it exists.
- **Key Takeaway** — the core point the post made or was meant to make.
- **Angle Used** — the angle as actually executed (can differ slightly from the originally approved Specific Angle — record what actually shipped).
- **Related Topics** — other Topic IDs this connects to, so future duplicate checks and "new development" calls have something to compare against.
- **Novelty Notes** — why this topic/angle combination was considered new, or what would make a future return to this topic novel enough to justify.
- **ECG Type** — *(added 2026-08-30, per Bilal's explicit instruction)* a secondary classification, independent of Content Pillar/Skill Tier, describing the topic's shelf-life and reach strategy. One of:
  - **Evergreen** — no news hook required; the founder pain point doesn't expire; can be republished/repurposed indefinitely.
  - **Evergreen + Controversial** — same timelessness, but executed with a debate-sparking or contrarian stance to drive comments/shares rather than passive agreement.
  - **Growth** — timely/reactive, tied to a current event, news item, or active conversation; optimized for near-term reach; usually checklist/listicle format.
  - **Evergreen + Growth** — a timeless topic deliberately given a timely hook or urgency framing (a current event, trend, or format) to combine long-term relevance with a near-term reach boost.
  Every topic `linkedin-topic-researcher` recommends going forward gets tagged with one of these four. A topic can only carry one ECG Type at a time — if its treatment changes enough to justify a different one, that's a new angle, not a relabel of the old record.

Scaffold every field even when a topic is still early (e.g. Date Published, Performance Reference, and Post Reference stay blank for an `IDEA` or `APPROVED` record) — a blank field is informative; a missing field silently invites someone to guess.

## Status lifecycle

A topic moves through these statuses, and only in this direction (a rejection can happen at any point before publish, but nothing moves backward from PUBLISHED):

- **IDEA** — a candidate surfaced by research, not yet decided on.
- **APPROVED** — Bilal has explicitly approved it as worth pursuing, per `linkedin-topic-researcher`'s approval workflow. Not yet scheduled or briefed.
- **PLANNED** — approved and now queued — has a strategic brief in progress or scheduled via `linkedin-content-strategist`, but not yet published.
- **PUBLISHED** — live. This is also when Post Reference and (once available) Performance Reference get filled in.
- **REJECTED** — Bilal explicitly declined it. Keep the record — a rejected topic is still useful history for avoiding the same pitch twice, and for recognizing when circumstances have genuinely changed enough to justify revisiting it.

Only an explicit approval moves a topic to `APPROVED`; only Bilal deciding to schedule or brief it moves it to `PLANNED`; only actual publication moves it to `PUBLISHED`. Don't let a skill infer a status change from context — each transition should be traceable to a specific action.

## Duplicate check discipline

Comparing only titles is not a duplicate check — two records can share a title and be genuinely different (new evidence, new angle, new audience problem), or have different titles and be functionally the same pitch. Every comparison must weigh:

- Topic
- Angle
- Audience problem
- Purpose
- Insight

This is the same discipline `linkedin-topic-researcher` applies when classifying a candidate as NEW / RELATED BUT DIFFERENT / NEW DEVELOPMENT / TOO SIMILAR / DUPLICATE — this document is what makes that classification possible, since there's nothing to compare against without it.

## Versioning topic IDs

- Never rename or renumber an existing Topic ID.
- If a topic returns with a genuinely new angle or new evidence, give it a new Topic ID and reference the earlier one under Related Topics — don't overwrite the old record, since the old one is still part of the history the duplicate check depends on.
- Assign new topics the next unused ID number; don't reuse retired numbers, including rejected ones.

## Who reads, who writes

- **Topic Researcher** — writes and updates CONTENT_TOPIC_DATABASE. This is its primary output alongside the topic recommendations themselves.
- **Content Strategist** — reads it (via the topic researcher's approved-topic handoff) to understand what's already been established about a topic before building a brief; doesn't add or edit records.
- **Learning Engine** — reads it for topic-level pattern history (which pillars/topics have accumulated real evidence); doesn't add or edit records directly, but can recommend the Topic Researcher revisit or retire a topic category.
- **Bilal** — the only source of approval for IDEA → APPROVED and the only source of a genuine rejection; no skill marks a topic APPROVED or REJECTED on its own judgment.

## The rule

Only approved topics become `PLANNED`. Only published topics become `PUBLISHED`. Never silently delete history — a rejected or superseded record stays in the database, correctly statused, rather than disappearing. If a record needs to be corrected, correct the fields; don't remove the row.
