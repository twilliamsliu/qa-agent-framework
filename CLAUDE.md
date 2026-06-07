# Maintenance rules for AI agents working on this repo

## Iron Law — duplicated content must be edited in lockstep

Some content in this repo is intentionally duplicated. **Before
committing any edit, check every counterpart surface below; if your
change touches duplicated content, update all copies in the same
commit.** Never let two copies drift.

Sync surfaces:

1. **Language pairs** — `README.md` ↔ `README.zh-TW.md`, and
   `templates/orchestrator-bootstrap.md` ↔
   `templates/orchestrator-bootstrap.zh-TW.md`. Any substantive edit
   to one side lands on the other side too.
2. **The 7 interview questions** — README *Questions an agent should
   ask before scaffolding* ↔ bootstrap Phase 1 (inlined by design so
   the bootstrap works offline). Four copies total across both
   languages.
3. **Section-title pointers from bootstrap Phase 3** — bootstrap
   points to two README sections **by section title**: *Push
   confirmation contract (Iron Law 1)* (Layer D) and *A pre-seeded
   rule: task boundaries* (Layer C; zh-TW:
   「一條預埋的自學規則：任務邊界」). Renaming either section breaks
   the pointer.
4. **Adoption path (Week 1–4+)** — README *How to adopt this* ↔
   bootstrap *What's next* roadmap and Phase 4 checklist.
5. **Bootstrap phase structure (Phase 1–4)** — bootstrap files ↔
   `.github/ISSUE_TEMPLATE/bootstrap-feedback.md` progress checklist
   ↔ the Status callout at the top of both READMEs.

If a check reveals the copies were *already* divergent, fix both
sides in the same commit and say so in the commit message.

## Other standing rules

- This repo is documentation only: no orchestrator code, scripts, or
  skill implementations. Concepts stay vendor-neutral.
- Do not add new sections for hypothetical needs; new content requires
  a real signal (an issue, a real adopter complaint).
- Conventional Commits (`feat:` / `fix:` / `docs:` / `chore:` …).
