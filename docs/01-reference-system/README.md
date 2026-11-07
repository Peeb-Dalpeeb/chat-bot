# Phase 1: Study the reference system

Goal: learn how an existing working chatbot is designed. Claude writes
questions, and the owner relays them to another AI that can read the system's
files. See "How the Phase 1 interview works" in `CLAUDE.md` for the process,
the labels, and when to stop.

## Core categories

These say what to find out, not what to ask. Tick each one off when it meets
the "done" rule in `CLAUDE.md`.

- [ ] **Getting documents in:** find out how documents get into the chatbot,
      including tables, charts, and updates.
- [ ] **RAG methods:** find out how it splits, stores, and searches documents
      to find the right passages.
- [ ] **Citations:** find out how sources are attached to answers and whether
      they are checked.
- [ ] **Confidence and refusals:** find out how it decides how sure it is, and
      what it does when it can't answer.
- [ ] **Response validation:** find out how it checks that answers are correct
      and supported before users see them.
- [ ] **Testing and evaluation:** find out how quality is measured and tracked
      over time, including user feedback.

## Hands-on testing (do alongside the interview)

- [ ] Run the golden questions (`docs/golden-questions.md`) on the live bot.
      Record its answer and citation, whether the citation is correct, and
      whether asking twice gives the same answer.

## Optional categories (only if the owner asks)

AI models and prompts, consistency, conversation handling, API calls and
architecture, code and hosting, logging and monitoring, security, compliance
and governance, user interface, lessons learned.

## How to record

- `interviews/`: raw questions and answers, named by date and category
  (for example `2026-11-08-rag-methods.md`).
- `findings/`: one short write-up per category, in our own words, with a
  source label on each finding.
- No secrets, keys, credentials, or code.
