# claude-skills

Claude skills for Bilal Ahmed's LinkedIn content system — drafts posts, writes comments/replies/DMs, triages the inbox, plans the week, and audits performance. Brand positioning stays governed separately and is the one part of the system that hasn't changed.

## Brand positioning — unchanged, source of truth for identity

| skill | does |
|---|---|
| `brand-positioning` | Bilal's approved identity, skill tiers, audience, and profile copy (Banner, Headline, About, Featured) — read-only reference for every other skill |
| `linkedin-brand-strategist` | The only skill that evaluates or changes profile copy. Never updates `brand-positioning` without Bilal's explicit approval |

## Content system

| skill | does |
|---|---|
| `linkedin-post-writer` | Turns a raw idea into a full LinkedIn post — 3 hook options from 21 proven formulas (`hooks.json`), one full draft, humanized before delivery. Reads `brand-positioning` for identity/audience and its own `ACCOUNT_HISTORY.md` for voice + validated performance learnings |
| `linkedin-audit` | Post-mortem on published posts — engagement rate, comment ratio, reach multiple, ranked top/bottom 5, honest pattern-finding. Feeds conclusions to `linkedin-weekly-planner` |
| `linkedin-weekly-planner` | The control room — what to post, when, and who to engage with, built from real evidence, not defaults |
| `linkedin-humanizer` | Shared final pass on every draft — strips invisible watermark characters, em dashes, and a 113-term AI-slop lexicon, then scores the result (burstiness, specificity, slop density, fingerprint, voice) |

## Execution skills — day-to-day writing and engagement

None of these post, comment, or send anything automatically — LinkedIn's User Agreement prohibits automating a personal profile. Every skill here ends at a copy-ready block the user sends themselves.

| skill | does |
|---|---|
| `linkedin-comment-writer` | Comments on other people's posts — nine types, picked by what the post actually is |
| `linkedin-reply-writer` | Handles the replies under Bilal's own posts, sorted lead → substance → peer → support → noise |
| `linkedin-dm-writer` | Connection notes and DM follow-ups — the 200-character invite, first message, two follow-ups |
| `linkedin-inbox-triage` | Sorts the inbox into lead / recruiter / peer / ask / spam and drafts only what's worth sending |
| `linkedin-carousel-writer` | Document posts — slide-by-slide copy, the cover that earns the swipe |
| `linkedin-repurposer` | Turns one long asset (video, newsletter, transcript) into a week of standalone posts |
| `linkedin-algorithm-researcher` | Live research on how LinkedIn's feed algorithm currently works — independent of the writing pipeline |

## Design principles

- **Brand positioning changes only with explicit approval.** `linkedin-brand-strategist` proposes, Bilal approves, then `brand-positioning` gets updated — never the other way around.
- **Real account history, not a cold start.** `linkedin-post-writer`'s `ACCOUNT_HISTORY.md` carries forward validated learnings from the account's actual post history — e.g. client-story structure is the strongest proven format, reused proof and "honest failure" postmortems both correlate with the account's worst results, stat-first hooks have underperformed twice against specific-fact hooks.
- **Nothing is fabricated.** No invented clients, metrics, or results ever go out under Bilal's name — a gap gets flagged, never papered over.
- **Nothing posts itself.** Every skill's output is a copy-ready block. A human sends it.

## Credit

Adapted from Jake Schincariol's [linkedin-agent-skill](https://github.com/Jakeschincariol/linkedin-agent-skill) (MIT), rewired to read `brand-positioning` for identity/voice and to preserve this account's own performance history instead of starting from a blank template.

## History

An earlier version of this repo ran a separate evidence pipeline (`CONTENT_DNA`/`VISUAL_DNA`, a Content Strategist/Writer/Analyst/Performance-Analyst/Learning-Engine chain) built up over ~15 published posts. That system was retired in favor of the `linkedin-agent-skill` pack above; its validated findings were migrated into `linkedin-post-writer/ACCOUNT_HISTORY.md` rather than discarded. See git history for the full prior architecture.
