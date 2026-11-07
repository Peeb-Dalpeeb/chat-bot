# Decisions

Newest first. Each entry: what was decided, and why.

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
