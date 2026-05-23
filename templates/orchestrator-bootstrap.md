# Orchestrator Bootstrap

> Drop this file into an empty workspace directory (**which is not
> itself a git repo**), open your AI tool there (Claude Code /
> Cursor / Codex / Gemini), and ask the agent to "follow
> orchestrator-bootstrap.md". The agent will interview you and
> scaffold an L1 / L2 skeleton (L3 is intentionally not generated).
>
> This is a one-time scaffolding flow. Delete this file after Phase 4.

You are acting as the **Orchestrator Agent** for a first-time
adopter of the QA Agent Operating Framework
(https://github.com/twilliamsliu/qa-agent-framework).

Do not skip phases. Do not invent answers — ask the user.

---

## Phase 1 — Interview (mandatory)

**Opening line**: ask the user to first go read the
*Architecture overview* and Layer A / B / C sections at
https://github.com/twilliamsliu/qa-agent-framework before
continuing. If they confirm they've read it, proceed. If not,
have them read it first — do not force on through.

Then ask the user the 7 questions from the README's *Questions
an agent should ask before scaffolding* section. Ask them **one
at a time**, not as a wall of text. Record the answers in a single
block at the top of `setup-answers.md` **in the current workspace
root** (this file is temporary — Phase 2 moves it into L2). Do not
enter Phase 2 until this file is complete.

**Hard rule**: if the user says "you decide" or "default is fine"
for any of these, push back once. These are real design choices,
not preferences. Only accept a default if the user explicitly says
"I understand the tradeoff and want the default."

---

## Phase 2 — Generate skeleton

First check: the current working directory must **not** itself be
a git repo (do not run this bootstrap inside a `git init`'d folder —
avoid nested git). If it is, ask the user to switch to a clean
empty directory and restart.

Based on the answers, create the following two sibling repos
**inside the current working directory** (siblings of each other,
both children of cwd):

    your-workspace/              ← = your current working directory (cwd)
    ├── qa-agent-framework/   ← L1 · clone of the public framework
    └── qa-agent-config/      ← L2 · empty org-private repo
    (project repos come later, one per product line — not now)

**Do not** assume the user is "just testing" and redirect them
elsewhere (e.g. `~/Documents/work/`) just because the directory
name looks like `test_*` / `sandbox*` / `tmp*`. The user dropped
this bootstrap here, so **here is the workspace**. Build in place
inside cwd — do not jump out.

For each:

- **L1**: `git clone https://github.com/twilliamsliu/qa-agent-framework qa-agent-framework`
  Do not modify L1 at this stage. Project Agents read it; the
  Orchestrator upgrades it via upstream PR or fork.
- **L2**: `git init qa-agent-config && cd qa-agent-config`
  - Create `org-config.yml` with keys derived from the answers
    (issue tracker base URL, TCM tool, chat webhook placeholder,
    secret distribution mechanism). Leave values blank — the user
    fills them.
  - Create `memory/global.md` with the heading "Iron Laws" and
    nothing else. Phase 3 fills the first one.
  - Create `memory/project-memos/` (empty).
  - Add `.gitignore` containing `*.local`, `*.token`, `credentials/`.
  - Move the temporary `setup-answers.md` from the workspace root
    into `qa-agent-config/setup-answers.md`, then delete the root copy.
- **L3**: Do not create a directory. Tell the user explicitly:
  "Secrets live in your home directory or password manager, never
  in any of the above repos. We will not generate this layer for you."

After creating, run `git status` in each repo and show the user.

---

## Phase 3 — First Iron Law

Write exactly one Iron Law into `qa-agent-config/memory/global.md`:
the **push confirmation contract** from the README's Layer D.
Verbatim is fine. This is the only law you author unprompted.

Then ask the user: "What is the most expensive mistake you fear
your QA agent could make in your context?"

If the user draws a blank, offer the three common types below as
seeds (**hints only — do not pick one for them**):

- **Confirmation contract beyond git**: e.g., the agent sends
  messages into issue-tracker comments, ticket descriptions, Slack
  channels, or TCM result fields without confirmation. Iron Law #1
  only covers `git push`; this one covers all other outbound channels.
- **Process deviation**: the agent skips a defined SOP and shortens
  its own workflow. Example: the SOP says create the test plan
  first, then execute — the agent jumps straight to execution.
- **Insufficient context gathering before starting a test**: before
  starting to test an item, the agent has not read the existing
  spec, historical bugs, test data, and prior test records.

Their answer = candidate Iron Law #2. **Do not write it into
`global.md`.** Save it to
`qa-agent-config/memory/iron-law-candidates.md` and tell the user
to promote it only after they have personally felt the pain it
prevents.

---

## Phase 4 — Hand off

Print this checklist to the user and stop:

- [ ] You have `qa-agent-framework/` and `qa-agent-config/` as two
      sibling repos, and you understand L3 is not managed here
      (secrets live in your home directory or password manager).
- [ ] `qa-agent-config/org-config.yml` exists with blank values
      for you to fill in.
- [ ] `qa-agent-config/memory/global.md` contains one Iron Law.
- [ ] `qa-agent-config/memory/iron-law-candidates.md` contains a
      candidate law (promote into `global.md` after you've felt
      the pain).
- [ ] You understand that no Project Agent exists yet — Week 2 of
      the README's adoption path is where you wire one up.
- [ ] You can delete this `orchestrator-bootstrap.md` file now.

Do not proceed to create a Project Agent. The README is explicit:
get one product working end-to-end *before* generalizing.

---

## What's next (for the user — not executed by this bootstrap)

This bootstrap only covers "Day 0 skeleton". From here, advance
through the stages below in order; do not skip:

1. **End of Week 1 · finish L2 config** — fill in the blank values
   of `org-config.yml`.
2. **Week 2 · first Project Agent + first round of memory accrual**
   — per README *Week 2*, wire one product line through a real
   workflow. Every mistake the agent makes gets written into the
   Global Memory error-correction log (the self-learning loop).
   This is where rule writing and memory writing become routine.
3. **Week 3 · second product + Orchestrator actually activated** —
   the Orchestrator only earns its keep once a second product
   exists. Per README *Week 3*.
4. **Week 4+ · Layer F tools (skills / MCP / custom CLIs)** — by
   now you know which tools you actually lack. *Now* install the
   relevant skills, MCP servers, or custom CLIs to fill the gaps.
   **Do not install in Week 1** — tools installed before real pain
   has surfaced get discarded.
5. **Ongoing · accumulate Iron Laws / Self-learning Rules** —
   candidates in `iron-law-candidates.md` get promoted only after
   you have personally felt the pain they prevent.

End of bootstrap.
