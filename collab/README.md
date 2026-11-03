# Collab — how this project is run

Onyx WrestleFest is built by three parties working from this repo:

- **Leon Zeigler** — owner. Sets direction, playtests every build, and is the
  final merge/deploy verdict. Nothing ships on "tests pass" alone; it ships
  when Leon plays it and says it's right.
- **Muse (lead)** — owns goals, this shared memory, task assignments, netplay
  (online multiplayer networking), code review of every PR, and deploys.
- **Codex (builder)** — owns gameplay implementation tasks assigned in
  `collab/TASKS.md`: gameplay, graphics, wrestling mechanics, AI, local play.

## The loop

1. Muse writes/updates tasks in `collab/TASKS.md` (spec + acceptance criteria).
2. Codex works the task on its own branch and opens a PR referencing the task ID.
3. Muse reviews the PR: diff, constraints in `collab/MEMORY.md`, netplay
   compatibility checks, and a live smoke test.
4. Leon playtests the test build. His verdict is the merge gate.
5. Muse merges, deploys, and updates `collab/MEMORY.md` + `collab/TASKS.md`.

## Files

- `GOALS.md` — what we're building and the current milestone.
- `MEMORY.md` — shared facts: architecture, hard rules, current state.
  Read it before starting any task. Update it when a fact changes.
- `TASKS.md` — the task board. One task = one branch = one PR.

## Ground rules

- Never overwrite the netplay integration (see MEMORY.md) in a gameplay change.
- Any NEW input key must be flagged in the PR description — Muse adds it to the
  server whitelist in the same pass, or the input silently dies online.
- Work on a branch; never commit gameplay work directly to `main`.
- A feature is done when it is verified **in the game**, not by syntax checks.
