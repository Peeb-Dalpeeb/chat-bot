# Decisions

Newest first. Each entry: what was decided, and why.

## 2026-11-07: Project setup

- **Work in four phases** (study, research, plan, build), and don't build
  before the plan. *Why:* the goal is to learn how good systems are built, not
  to guess.
- **Every answer must cite its section.** *Why:* reliability and trust; users
  of regulation bots need to check the source.
- **Use eCFR Title 12 as the document source; don't use BankersOnline.**
  *Why:* eCFR is free, official federal text with an API and clean structure.
  BankersOnline returned "Payment Required", its robots.txt blocks AI tools, and
  its content is copyrighted.
- **Start with Reg B, E, Z, and DD,** then add public PDFs with charts later.
  *Why:* get a small set reliable before scaling up.
- **Keep reference system source code out of git.** *Why:* it isn't ours to
  publish.
