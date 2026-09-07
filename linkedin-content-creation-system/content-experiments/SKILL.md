---
name: content-experiments
description: >-
  Defines and governs CONTENT_EXPERIMENTS — the shared record of every controlled test Bilal's LinkedIn content system has run or is running, designed to answer a specific question rather than just try something new. Use this whenever creating a new CONTENT_EXPERIMENTS document from scratch, validating or restructuring an existing one against the required schema, resolving what status an experiment is actually in (PROPOSED/ACTIVE/COMPLETED/SUPPORTED/REJECTED/INCONCLUSIVE), or when any skill needs to know exactly how to read from or write to it correctly (required fields per experiment, the status lifecycle, who writes vs. only reads, the never-delete rule). This is a schema-and-governance skill, not the skill that designs or runs experiments — that's linkedin-learning-engine. Trigger it whenever CONTENT_EXPERIMENTS itself — its format, its integrity, or a rule about how it should be updated — is the thing in question.
---

# CONTENT_EXPERIMENTS — Shared Experiment Record

CONTENT_EXPERIMENTS tracks controlled experiments designed to improve Bilal's LinkedIn content system. It's owned and written to by `linkedin-learning-engine`, which designs and evaluates experiments; this skill governs the document's format and rules so that ownership stays disciplined as the log grows.

## Every experiment must answer a specific question

An experiment is not "let's try something different this week" — it's a falsifiable question with a clear variable. Before an entry is created, it should be possible to state the question in one sentence:

- Does a problem-based hook outperform an educational hook?
- Does a technical diagram generate more saves than a text-only post?
- Does a personal experience increase profile visits?

If a proposed experiment can't be stated this specifically, it isn't ready for CONTENT_EXPERIMENTS yet — send it back for tightening rather than logging a vague test that won't produce a clean answer.

## Experiment format

Every experiment gets an entry with all of these fields:

- **Experiment ID** — e.g. `EXP-04`. Permanent once assigned — see versioning below.
- **Hypothesis** — the specific, falsifiable claim being tested.
- **Reason** — what prompted this experiment: an observation, a gap in CONTENT_DNA/VISUAL_DNA, a direct request from Bilal.
- **Variable** — the one thing being changed. Only one major variable per experiment where practical — changing hook, format, and length together tells you nothing about which one mattered.
- **Control** — what stays constant across the test, if applicable.
- **Test** — what the test posts/actions actually consist of (concrete enough that someone could execute it without asking follow-up questions).
- **Audience** — who this experiment is being run against/for.
- **Time Period** — dates or post count the experiment runs across.
- **Sample Size** — how many posts/instances count toward this experiment; also record the number as data comes in, not just the target.
- **Results** — filled in as data comes in, referencing the actual CONTENT_MEMORY entries/posts involved.
- **Comparison** — how the results actually compare to the control or to account baseline.
- **Conclusion** — filled in once the test period/sample is complete.
- **Confidence** — Proven / Strong / Emerging / Experimental / Unknown.
- **Next Action** — what happens because of this result: a CONTENT_DNA/VISUAL_DNA recommendation, a follow-up experiment, or "insufficient evidence, continue observing."

## Status lifecycle

- **PROPOSED** — designed, not yet started.
- **ACTIVE** — currently collecting data.
- **COMPLETED** — data collection finished, conclusion drawn. This is a checkpoint, not a verdict — it says the test is done, not what it found. Every completed experiment resolves into exactly one of the next three:
- **SUPPORTED** — the hypothesis held up; this is what gets cited when recommending a CONTENT_DNA/VISUAL_DNA change.
- **REJECTED** — the hypothesis did not hold up. This is still a valid, useful outcome — record it as clearly as a supported one, since it prevents the same test from being run again under a different name.
- **INCONCLUSIVE** — the data didn't clearly support or reject the hypothesis (sample too small, confounding factors, mixed results). Don't force an inconclusive result into SUPPORTED or REJECTED just to close the entry — an honest INCONCLUSIVE is more useful than a false confident one.

## The important distinction

**An experiment result is not automatically a permanent rule.** Even a SUPPORTED experiment is one piece of evidence, not an instant CONTENT_DNA rewrite — it strengthens the case, and validated results (per the evidence discipline already governing CONTENT_DNA/VISUAL_DNA) may lead the Learning Engine to recommend a change. That recommendation still goes through the same OLD UNDERSTANDING / NEW EVIDENCE / CONFIDENCE / RECOMMENDED CHANGE process as any other CONTENT_DNA update, and still routes through `linkedin-content-analyst` to actually write it in.

## Versioning experiment IDs

- Never rename or renumber an existing Experiment ID.
- If a follow-up experiment tests a refined version of the same hypothesis, give it a new ID and reference the earlier one in Reason — don't overwrite the original, since the original's result is still part of the evidence trail.
- Assign new experiments the next unused ID number; don't reuse retired numbers, including rejected or inconclusive ones.

## Who reads, who writes

- **Learning Engine** — designs, proposes, updates, and evaluates experiments. This is its primary tool for turning a hypothesis into a testable claim.
- **Performance Analyst** — supplies the per-post evidence (via CONTENT_MEMORY, referenced in Experiments Connected) that feeds an active experiment's Results; can propose a new experiment idea, but the Learning Engine formalizes and owns the entry.
- **Content Analyst** — reads a SUPPORTED experiment's conclusion as supporting evidence when the Learning Engine recommends a CONTENT_DNA/VISUAL_DNA change; doesn't edit CONTENT_EXPERIMENTS.
- **Bilal** — can propose an experiment directly; final say on anything that would touch the approval-required list (brand positioning, skill tiers, audience, pillars, voice, visual identity, brand colors) even if an experiment technically supports it.

## Never delete

Never delete or overwrite a past experiment's record, including a failed, rejected, or inconclusive one. A failed experiment is still evidence — deleting it risks the same test being run again later under a different name, wasting a real opportunity to learn something new instead. If Bilal explicitly instructs removal, that's the only path deletion happens through.
