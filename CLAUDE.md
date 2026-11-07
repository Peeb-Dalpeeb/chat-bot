# CLAUDE.md

## What this project is

A learning project: build a chatbot that answers questions about banking
regulations **reliably and consistently, always citing the exact section** it
used. Banks and other organizations are building bots like this, and the goal
here is to learn how to build one well, not just to ship one.

The approach is commonly called RAG (retrieval-augmented generation): find the
relevant passages in the documents first, then answer only from those passages.

## How we work: four phases, in order

We don't skip ahead. Each phase builds on what the previous one wrote down.

1. **Study a reference system** (`docs/01-reference-system/`)
   Learn exactly how an existing working chatbot was built: retrieval,
   confidence scoring, answer checks, citations, user feedback, validation, and
   API calls. **Claude interviews the owner**, who answers using that bot and
   its source files. See "How the Phase 1 interview works" below.
2. **Research** (`docs/02-research/`)
   Use research agents to learn how other industries build reliable chatbots
   and what current research says about producing valid, trustworthy answers.
3. **Plan** (`docs/03-plan/`)
   Write our own design, based only on what Phases 1 and 2 found.
4. **Build**
   Implement the plan. Code folders (such as `src/`, `data/`, `tests/`) are
   created in this phase, following the plan. Don't create them earlier.

**Current phase: 1, Study the reference system.**
Update this line when a phase is finished.

## Ground rules

- **Plain English.** The owner is learning. Explain the "why", define jargon
  the first time it appears, and keep write-ups readable.
- **Every bot answer cites its section** (for example, "12 CFR 1005.6(b)").
  This is a hard requirement for the final system.
- **Separate fact from claim.** In Phase 1, label each finding by where it came
  from: *seen in source code*, *observed in testing*, *said by the bot*, or
  *our guess*. A bot describing itself is not proof of how it works.

## How the Phase 1 interview works

- Claude asks; the owner answers. Grill the owner. Don't accept vague answers.
  Ask follow-ups until the detail is concrete (which model, which setting,
  which number, what happens when it fails).
- Work one category at a time from the list in
  `docs/01-reference-system/README.md`. The list says what to find out, not
  what to ask: think through every question needed to understand each category
  fully, and follow new threads as they come up. Ask a few questions per turn,
  not a wall of them.
- For each answer, ask where it came from (the source code, the bot itself, or
  the owner's own understanding), so findings can be labelled.
- When something can't be answered, suggest a question the owner can put to the
  bot, or a place in the source code to look.
- Save notes as you go in `docs/01-reference-system/interviews/`, and write up
  each finished category in `findings/`. Tick it off in the list.
- **Cite research sources.** In Phase 2, every finding links to where it came
  from.
- **Write findings down in `docs/`.** Chat history is lost, but the repo is not.
- **Record decisions** in `docs/decisions.md`, with the date and the reason.

## Reference system source code is confidential

The reference system's source files go in `reference-source/`, and that folder
is git-ignored. Never commit, copy, or quote those files into any other part of
the repo. Never record secrets, API keys, credentials, or internal hostnames
from it. Describe *how* it works in our own words in
`docs/01-reference-system/findings/`.

## Document sources

- **Use:** the official federal text from the eCFR (ecfr.gov), Title 12 (Banks
  and Banking). It has a free API that returns structured XML split into parts,
  sections, and paragraphs. Use the dated URL form
  (`/api/versioner/v1/full/YYYY-MM-DD/title-12.xml?part=1005`), because
  `current` returned an error for full text when tested.
- **Start with:** Reg B (12 CFR 1002), Reg E (1005), Reg Z (1026), Reg DD (1030).
- **Later:** public PDFs with charts and tables (for example, the FFIEC BSA/AML
  Examination Manual and CFPB exam procedures).

## Folder map

```
CLAUDE.md                     this file
README.md                     short project overview
docs/
  decisions.md                dated log of decisions and why
  01-reference-system/
    README.md                 categories to cover in the interview
    interviews/               raw notes from each interview session
    findings/                 one write-up per category, in our own words
  02-research/
    README.md                 research questions
    industries/               how other industries do it
    literature/               what research papers and guides say
  03-plan/
    README.md                 our design, written after Phases 1 and 2
reference-source/             reference system code (git-ignored, local only)
```
