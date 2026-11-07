# Phase 1: Study the reference system

Goal: learn, in full detail, how an existing working chatbot is built, by
interviewing the owner, who answers using the running bot and its source code
(kept in `reference-source/`, which is not committed).

## Categories to cover

These are areas to explore, not a script. Within each one, think of the
questions needed to understand it fully, and keep asking until the details are
concrete. Add new categories if something important turns up. Tick each one off
when its write-up is saved in `findings/`.

- [ ] **Purpose and users:** find out what the bot is for, who uses it, and
      what "working well" means to the organization.
- [ ] **Getting documents in:** find out how the documentation gets into the
      chatbot: sources, formats, tables and charts, cleanup, and updates.
- [ ] **RAG methods:** find out how it splits, stores, and searches documents
      to find the right passages for a question.
- [ ] **AI models and prompts:** find out which models it uses, their
      settings, and what instructions they are given.
- [ ] **Citations:** find out how sources are attached to answers and whether
      they are checked.
- [ ] **Confidence:** find out how it decides how sure it is, and what it does
      when it isn't sure.
- [ ] **Response validation:** find out how it checks that answers are correct
      and supported before and after users see them.
- [ ] **Consistency:** find out how it makes sure the same question gets the
      same answer.
- [ ] **Conversations:** find out how it handles follow-ups, memory, and vague
      questions.
- [ ] **User feedback:** find out how feedback is collected, reviewed, and used
      to improve the bot.
- [ ] **Testing and evaluation:** find out how quality is measured and
      tracked over time.
- [ ] **API calls and architecture:** find out every step and call from
      question to answer, plus speed, cost, and what happens when something
      fails.
- [ ] **Code, tools, and hosting:** find out what it's built with and where it
      runs.
- [ ] **Logging and monitoring:** find out what is recorded and how problems
      are spotted.
- [ ] **Security features:** find out how data, access, and the bot's
      instructions are protected.
- [ ] **Compliance and governance:** find out what reviews, approvals, and
      rules it operates under.
- [ ] **User interface:** find out what users see, including how citations and
      confidence are shown.
- [ ] **Lessons learned:** find out what was hard, what failed, and what they
      would do differently.
- [ ] **Hands-on testing:** have the owner test the bot directly and record
      exactly how it behaves, especially on tricky cases.

## How to record

- `interviews/`: raw notes from each session, named by date and category
  (for example `2026-11-08-rag-methods.md`).
- `findings/`: one clean write-up per category, in our own words.
- Label every finding by its source: **seen in source code**, **observed in
  testing**, **said by the bot**, or **our guess**.
- No secrets, keys, credentials, or copied code.
