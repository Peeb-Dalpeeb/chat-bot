# Decisions

Newest first. Each entry: what was decided, and why.

## 2026-11-07: Trim Phase 1 after an independent review

- **Cut Phase 1 to six core categories**, with the rest optional, and about 5
  questions per batch. *Why:* 19 categories would mean weeks of relaying, and
  many teach little about reliable answers with citations.
- **Add a golden question set**, used from Phase 1 onward. *Why:* testing the
  live bot is the only evidence that doesn't rely on an AI's description, and
  the same set later scores our own bot.
- **Check teach-backs in a fresh source-AI session.** *Why:* the same session
  tends to agree with its own earlier answers.
- **Drop the per-category confidence label.** *Why:* the per-finding labels
  already carry that information.
- **Remove the `reference-source/` folder.** *Why:* we study the design, not
  the code, so nothing goes there.
- **Include the Official Interpretations and track regulation dates.** *Why:*
  many answers live in the commentary, and rules change.
- **Not adopted: a hands-on experiment before planning.** *Why:* the owner
  wants research and planning done before any building.

## 2026-11-07: Phase 1 interview process

- **Questions are relayed to a "source AI"** that can read the reference
  system's files, not asked of the owner directly. *Why:* that is where the
  details live.
- **Study the architecture only: no code, file names, or function names.**
  *Why:* the system isn't ours, and the design is what we need to learn.
- **Each answer is marked "confirmed in the files" or "not sure," or says "not
  found."** *Why:* an AI can make things up; this keeps answers checkable
  without exposing the code.
- **Stop each category on a confirmed teach-back, not a confidence number.**
  *Why:* AI self-rated confidence is unreliable. A summary the source AI checks
  against the files is something we can actually verify.

## 2026-11-07: Project setup

- **Work in four phases** (study, research, plan, build), and don't build
  before the plan. *Why:* the goal is to learn how good systems are built, not
  to guess.
- **Every answer must cite its section.** *Why:* reliability and trust; users
  of regulation bots need to check the source.
- **Use eCFR Title 12 as the document source.** *Why:* it is free, official
  federal text with an API and clean structure.
- **Start with Reg B, E, Z, and DD,** then add public PDFs with charts later.
  *Why:* get a small set reliable before scaling up.
- **Keep reference system source code out of git.** *Why:* it isn't ours to
  publish.
