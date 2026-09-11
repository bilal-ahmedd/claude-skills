# claude-skills

Claude skills for Bilal Ahmed's LinkedIn content system — a governed pipeline that researches topics, drafts posts, writes comments/replies/DMs, triages the inbox, plans the week, scores the profile, and measures what actually worked, all grounded in one evolving, evidence-based source of truth instead of generic LinkedIn advice.

## How it fits together

```
Topic Researcher ──▶ Content Strategist ──▶ Content Writer ──▶ (posted by Bilal)
      │                                                              │
      ▼                                                              ▼
Content Topic DB                                           Performance Analyst
                                                                      │
                                                                      ▼
                                                            Learning Engine
                                                                      │
                                                                      ▼
                                                          Content Analyst ──▶ CONTENT_DNA / VISUAL_DNA
```

Everything upstream of a post (topic, structure, voice) comes from evidence already logged in this repo's data documents — not from a generic hook-formula list. Everything downstream of a post (performance, learning) feeds back into those same documents, so the system gets better at *this specific account* over time instead of staying static.

## Governance skills — schema + data, not workflow

Each pair below is a schema-and-rules skill plus the actual data document it governs. Only the named owner writes to the data file; everything else reads it.

| schema skill | data file | owner | purpose |
|---|---|---|---|
| `brand-positioning` | (itself) | `linkedin-brand-strategist` | Approved identity, skill tiers, audience, profile copy |
| `content-dna` | `content-dna-record` | `linkedin-content-analyst` | Evidence-gated content structures + Voice DNA |
| `visual-dna` | `visual-dna-record` | `linkedin-content-analyst` | Evidence-gated visual patterns + brand colors |
| `content-memory` | `content-memory-record` | `linkedin-performance-analyst` | Permanent per-post performance log |
| `content-experiments` | `content-experiments-record` | `linkedin-learning-engine` | Controlled tests run on the account |
| `content-topic-database` | `content-topic-database-record` | `linkedin-topic-researcher` | Every topic considered, approved, or rejected |

## Pipeline skills

| skill | does | reads | never does |
|---|---|---|---|
| `linkedin-topic-researcher` | Finds non-repetitive content opportunities grounded in real positioning and history | brand-positioning, CONTENT_TOPIC_DATABASE, CONTENT_DNA | Write posts, pick structure |
| `linkedin-content-strategist` | Turns an approved topic into a strategic brief (structure + visual + hook direction) | CONTENT_DNA, VISUAL_DNA, brand-positioning | Write final copy |
| `linkedin-content-writer` | Executes a brief into a finished post + image prompt, in Voice DNA, following the selected structure | Strategist's brief, CONTENT_DNA, VISUAL_DNA | Choose structure, research topics |
| `linkedin-performance-analyst` | Analyzes single posts or batches against baseline; separates FACT/OBSERVATION/HYPOTHESIS | Post + metrics, CONTENT_MEMORY | Edit CONTENT_DNA directly, write posts |
| `linkedin-learning-engine` | Decides when evidence is strong enough to actually change CONTENT_DNA/VISUAL_DNA; owns experiments | Accumulated performance data | Write posts, change brand positioning |
| `linkedin-content-analyst` | Converts real post history (copy + visuals + metrics) into structured CONTENT_DNA/VISUAL_DNA updates | Published posts, performance data | Write new posts, decide strategy |
| `linkedin-brand-strategist` | The only skill that evaluates or changes profile copy (headline/About/Featured/banner); scores it against a 12-point rubric | brand-positioning | Write posts, research topics |
| `linkedin-algorithm-researcher` | Live research on how LinkedIn's feed algorithm currently works | Fresh web research (never memory alone) | Give branding or content advice |

## Execution skills — day-to-day writing and engagement

These produce copy-ready text the user reviews and posts themselves. **None of them post, comment, or send anything automatically** — LinkedIn's User Agreement prohibits automating a personal profile, and every skill here ends at a copy-ready block, by design, not as a limitation bolted on afterward.

| skill | does |
|---|---|
| `linkedin-comment-writer` | Comments on other people's posts — nine types, picked by what the post actually is |
| `linkedin-reply-writer` | Handles the replies under Bilal's own posts, sorted lead → substance → peer → support → noise |
| `linkedin-dm-writer` | Connection notes and DM follow-ups — the 200-character invite, first message, two follow-ups |
| `linkedin-inbox-triage` | Sorts the inbox into lead / recruiter / peer / ask / spam and drafts only what's worth sending |
| `linkedin-carousel-writer` | Document posts — slide-by-slide copy, the cover that earns the swipe |
| `linkedin-repurposer` | Turns one long asset (video, newsletter, transcript) into a week of standalone posts |
| `linkedin-weekly-planner` | The control room — what to post, when, and who to engage with, built from real evidence not defaults |
| `linkedin-humanizer` | Shared final pass on every draft above — strips invisible watermark characters, em dashes, and a 113-term AI-slop lexicon, then scores the result (burstiness, specificity, slop density, fingerprint, voice) |

`linkedin-humanizer` ships two dependency-free Python scripts (`humanize.py`, `detect.py`) plus `slop.json` (the lexicon). It runs as a mechanical, quantitative pass *after* the qualitative `stop-slop` pass every writer skill already applies — the two aren't redundant: one catches structural AI tells, the other catches invisible characters and typography a prose review misses.

## Design principles

- **Evidence over formula.** CONTENT_DNA and VISUAL_DNA are built from this account's own published results, not generic "21 hooks that work on LinkedIn" advice. Where a generic reference (like `hooks.json`) is kept, it's explicitly secondary to whatever the evidence-based structure already specifies.
- **Nothing is approved silently.** Brand positioning and profile copy only change after Bilal explicitly approves — a proposal is never treated as decided just because it sounds right.
- **Nothing is fabricated.** No invented clients, metrics, or results ever go out under Bilal's name, even as a placeholder — a gap gets flagged (`[NEED USER INPUT]`), never papered over.
- **Nothing posts itself.** Every skill's output is a copy-ready block. A human sends it.
- **One writer per document.** Each data file (CONTENT_DNA, CONTENT_MEMORY, etc.) has exactly one skill authorized to write to it; every other skill reads it.

## Credit

The hook-formula library, the humanizer's mechanical checks, and several of the engagement-focused skills (comment, reply, DM, inbox, carousel, repurpose, weekly planning) were adapted from Jake Schincariol's [linkedin-agent-skill](https://github.com/Jakeschincariol/linkedin-agent-skill) (MIT), then rewired to read from and write to this repo's own CONTENT_DNA/brand-positioning system instead of a standalone voice file.
