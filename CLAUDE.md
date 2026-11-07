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
   Learn how an existing working chatbot is designed. Claude writes questions,
   and the owner relays them to another AI that can read that system's files.
   The owner also tests the live bot with the golden questions. See "How the
   Phase 1 interview works" below.
2. **Research** (`docs/02-research/`)
   Claude runs web research (using subagents to cover several topics at once)
   on how other industries build reliable chatbots and what current research
   says. One file per source or topic, and every claim links to its source.
3. **Plan** (`docs/03-plan/`)
   Write our own design, based only on what Phases 1 and 2 found.
4. **Build**
   Implement the plan. Code folders (such as `src/`, `data/`, `tests/`) are
   created in this phase, following the plan. Don't create them earlier.

**Current phase: 1, Study the reference system.**
Update this line when a phase is finished.

## Golden questions

`docs/golden-questions.md` is the project's test set: real questions, each
with the correct answer and section citation. It is used in every phase: to
test the reference bot (Phase 1), to judge what research suggests (Phases 2-3),
and to score our own bot (Phase 4). Build it up early and keep it current.

## Ground rules

- **Plain English.** The owner is learning. Explain the "why", define jargon
  the first time it appears, and keep write-ups readable.
- **Every bot answer cites its section** (for example, "12 CFR 1005.6(b)").
  This is a hard requirement for the final system.
- **Separate fact from claim.** Label every Phase 1 finding by where it came
  from (labels are listed below). An AI describing a system is not proof of how
  it works.
- **Write findings down in `docs/`.** Chat history is lost, but the repo is not.
- **Record decisions** in `docs/decisions.md`, with the date and the reason.

## How the Phase 1 interview works

### The setup

Claude is not talking to the reference system directly. The loop is:

1. Claude writes a batch of questions.
2. The owner pastes them into another AI that has access to the reference
   system's files (the "source AI").
3. The owner pastes the source AI's answers back here.

### Keep it light

- **Six core categories only** (listed in `docs/01-reference-system/README.md`).
  The optional ones are covered only if the owner asks.
- **About 5 questions per batch, and aim for 2-3 batches per category.** Ask
  what matters most first. Don't chase small details that won't affect our own
  design.

### Writing each batch

- **One copy-paste block per batch.** The source AI hasn't seen this
  conversation, so each batch must make sense on its own.
- **Start every batch with these instructions to the source AI:**
  - Describe the architecture and approach in plain words. Don't include code,
    file names, function names, keys, passwords, or internal addresses.
  - Mark each answer **confirmed in the files** or **not sure**.
  - If the files don't show it, say "not found in the files." Don't guess.
- **Stay at the architecture level:** what the parts are, what approach each
  one uses, what kind of tool or model, in what order, and what happens when
  something fails. Never ask for code or where in the code something lives.
- **Push past vague answers.** If the answer is "it checks the answer," ask:
  checks it how, against what, and what happens if the check fails?

### Labelling findings

- **Observed in testing:** the owner saw it happen on the live bot. This is the
  strongest evidence, because it doesn't rely on an AI's description.
- **Confirmed in the files:** the source AI marked it confirmed.
- **Not sure:** the source AI marked it not sure.
- **Not found:** the source AI said the files don't show it.
- **Our guess:** inferred by us, not stated anywhere.

### When a category is done

1. **Teach-back confirmed.** Claude writes a short plain-English summary. The
   owner pastes it into a **fresh** source-AI session (so it isn't just
   agreeing with its own earlier answers) with "Check this against the files
   and correct anything wrong," and the corrections are applied.
2. **Gaps recorded.** Anything that can't be answered is written down as
   "unknown" with the reason. Unknowns don't block progress.

Tick it off in the list.

### When the interview is done

- The six core categories are done, the golden questions have been run on the
  live bot, **and**
- Claude writes a short walkthrough of one question's full journey, from "user
  hits send" to "answer with citations appears," and a fresh source-AI session
  confirms it.

The owner can stop, skip, or reorder at any time.

### Saving work

Save raw questions and answers in `docs/01-reference-system/interviews/`, and
write up each finished category in `docs/01-reference-system/findings/`.

## Reference system details are confidential

The reference system isn't ours to publish. We study its design, not its code.
Describe how it works in our own words. Never ask for or record its code, file
names, secrets, API keys, credentials, or internal hostnames, even if they
appear in a relayed answer.

## Document sources

- **Use:** the official federal text from the eCFR (ecfr.gov), Title 12 (Banks
  and Banking). It has a free API that returns structured XML split into parts,
  sections, and paragraphs. Use the dated URL form
  (`/api/versioner/v1/full/YYYY-MM-DD/title-12.xml?part=1005`), because
  `current` returned an error for full text when tested.
- **Start with:** Reg B (12 CFR 1002), Reg E (1005), Reg Z (1026), Reg DD (1030).
- **Include the Official Interpretations** (Supplement I at the end of each
  part). Many real answers live there, not in the rule text.
- **Track dates.** Regulations change. Every document and answer should say
  which version (date) it is based on.
- **Later:** public PDFs with charts and tables (for example, the FFIEC BSA/AML
  Examination Manual and CFPB exam procedures).

## Folder map

```
CLAUDE.md                     this file
README.md                     short project overview
docs/
  decisions.md                dated log of decisions and why
  golden-questions.md         test questions with correct answers and citations
  01-reference-system/
    README.md                 categories to cover in the interview
    interviews/               raw questions and answers from each session
    findings/                 one write-up per category, in our own words
  02-research/
    README.md                 research questions
    industries/               how other industries do it
    literature/               what research papers and guides say
  03-plan/
    README.md                 what the plan must cover
```
