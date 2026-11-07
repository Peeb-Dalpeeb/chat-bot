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
   API calls. Claude writes the questions, and the owner relays them to another
   AI that can read that system's files. See "How the Phase 1 interview works"
   below.
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
  from (labels are listed below). An AI describing a system is not proof of how
  it works.
- **Cite research sources.** In Phase 2, every finding links to where it came
  from.
- **Write findings down in `docs/`.** Chat history is lost, but the repo is not.
- **Record decisions** in `docs/decisions.md`, with the date and the reason.

## How the Phase 1 interview works

### The setup

Claude is not talking to the reference system directly. The loop is:

1. Claude writes a batch of questions.
2. The owner pastes them into another AI that has access to the reference
   system's files (the "source AI").
3. The owner pastes the source AI's answers back here.

### Writing each batch

- **One copy-paste block per batch.** The source AI hasn't seen this
  conversation, so each batch must make sense on its own.
- **Start every batch with these instructions to the source AI:**
  - Describe the architecture and approach in plain words. Don't include code,
    file names, function names, keys, passwords, or internal addresses.
  - Mark each answer **confirmed in the files** or **general understanding /
    not sure**.
  - If the files don't show it, say "not found in the files." Don't guess.
- **Stay at the architecture level.** The goal is to understand the design:
  what the parts are, what approach each one uses, what kind of tool or model,
  in what order, and what happens when something fails. Never ask for code or
  for where in the code something lives.
- **Grill it within that level.** Don't accept vague answers like "it checks
  the answer." Follow up until the approach is clear: checks it how, against
  what, and what happens if the check fails.
- **One category at a time** from the list in
  `docs/01-reference-system/README.md`. The list says what to find out, not
  what to ask. Think through every question needed to understand the category
  fully, and follow new threads as they come up.

### Labelling findings

- **Confirmed in the files:** the source AI marked it confirmed.
- **Observed in testing:** the owner tried it on the running bot.
- **Not confirmed:** the source AI marked it general understanding or not sure.
- **Our guess:** inferred by us, not stated anywhere.

### When a category is done

A category is done when all three are true:

1. **Teach-back confirmed.** Claude writes a plain-English summary of the
   category. The owner pastes it to the source AI with "Check this against the
   files and correct anything wrong," and the corrections are applied.
2. **No open questions left.** Anything that can't be answered is recorded as
   "unknown" with the reason. Unknowns are allowed; they don't block progress.
3. **Key facts are backed up.** The important details are labelled *confirmed
   in the files* or *observed in testing*, not just *not confirmed*.

Give each finished category a confidence label (high, medium, or low) in its
write-up, and tick it off in the list.

### When the whole interview is done

- Every category is done or marked "can't find out," **and**
- Claude writes a step-by-step walkthrough of one question's full journey, from
  "user hits send" to "answer with citations appears," and the source AI
  confirms it is accurate.

The owner can stop, skip, or reorder categories at any time.

### Saving work

Save raw questions and answers as you go in
`docs/01-reference-system/interviews/`, and write up each finished category in
`docs/01-reference-system/findings/`.

## Reference system details are confidential

The reference system isn't ours to publish. We study its architecture, not its
code. Describe *how* it works in our own words. Never ask for or record its
code, file names, secrets, API keys, credentials, or internal hostnames, even
if they appear in a relayed answer. If source files
are ever copied into this repo, they go in `reference-source/`, which is
git-ignored.

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
    interviews/               raw questions and answers from each session
    findings/                 one write-up per category, in our own words
  02-research/
    README.md                 research questions
    industries/               how other industries do it
    literature/               what research papers and guides say
  03-plan/
    README.md                 our design, written after Phases 1 and 2
reference-source/             for copied source files, if ever (git-ignored)
```
