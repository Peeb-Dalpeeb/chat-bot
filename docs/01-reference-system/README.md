# Phase 1: Study the reference system

Goal: learn, in full detail, how an existing working chatbot is built. We do it
interviewing the owner, who answers using the running bot and its source code
(kept in `reference-source/`, which is not committed).

## Topics to cover

Each topic gets its own write-up in `findings/` when done.

- [ ] **Retrieval (RAG):** how documents are loaded, split into chunks, stored,
      and searched. Which embedding model and search method are used.
- [ ] **Confidence ratings:** how the bot decides how sure it is, and what it
      does when it isn't sure.
- [ ] **Answer quality checks:** what makes an answer "good" and how that is
      checked before the user sees it.
- [ ] **Citations:** how sources are attached to answers and checked for
      accuracy.
- [ ] **User feedback:** how users rate answers, and what happens to that
      feedback.
- [ ] **Validation and testing:** how answers are tested over time (test sets,
      scoring, reviews).
- [ ] **API calls:** which AI models and services are called, in what order,
      and with what settings and prompts.
- [ ] Anything else that turns up.

## How to record

- `interviews/`: raw notes from each session, named by date
  (for example `2026-11-08-retrieval.md`).
- `findings/`: one clean write-up per topic, in our own words.
- Label every finding by its source: **seen in source code**, **said by the
  bot**, or **our guess**.
- No secrets, keys, credentials, or copied code.
