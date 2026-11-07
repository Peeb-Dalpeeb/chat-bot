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
  - For each answer, name the file or function it is based on.
  - If the files don't show it, say "not found in the files." Don't guess.
  - Describe how things work in words. Don't paste code, keys, passwords,
    internal addresses, or settings values that look secret.
- **Grill it.** Don't accept vague answers. Follow up until the detail is
  concrete: which model, which setting, which number, what happens when it
  fails.
- **One category at a time** from the list in
  `docs/01-reference-system/README.md`. The list says what to find out, not
  what to ask. Think through every question needed to understand the category
  fully, and follow new threads as they come up.

### Labelling findings

- **Seen in source code:** the source AI named a specific file or function.
- **Observed in testing:** the owner tried it on the running bot.
- **Said without a file:** the source AI answered but gave no file reference.
- **Our guess:** inferred by us, not stated anywhere.

### When a category is done

A category is done when all three are true:

1. **Teach-back confirmed.** Claude writes a plain-English summary of the
   category. The owner pastes it to the source AI with "Check this against the
   files and correct anything wrong," and the corrections are applied.
2. **No open questions left.** Anything that can't be answered is recorded as
   "unknown" with the reason. Unknowns are allowed; they don't block progress.
3. **Key facts are backed up.** The important details are labelled *seen in
   source code* or *observed in testing*, not just *said without a file*.

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

The reference system isn't ours to publish. Describe *how* it works in our own
words. Never commit its code, and never record secrets, API keys, credentials,
or internal hostnames, even if they appear in a relayed answer. If source files
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
