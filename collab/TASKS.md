# Task board

Status key: READY → IN PROGRESS → IN REVIEW → CHANGES REQUESTED → DONE.
One task = one branch = one PR. Reference the task ID in the PR title.

---

## TASK-001 — In-Ring Gameplay Overhaul (fix the 12 playtest issues)

- **Owner:** Codex · **Status:** READY · **Assigned by:** Muse, 2026-11-03
- **Branch:** `gameplay/in-ring-overhaul` (new) — evaluate draft PR #1's branch
  (`gameplay/skull-arcade-stage-2026-11-02`) first; reuse what works, don't
  inherit what doesn't.

**Spec:** Fix the 12 issues in `collab/MEMORY.md` (Leon's 2026-11-02 playtest).
In priority order: real animated moves that match their names (issue 4/5),
movement without sliding/teleporting (10/11/12), working move set beyond
punch/kick/whip (6), rope climbing (7), ropes that match the reference and
mesh visually (8/9), arena look + right-sized crowd (2/3), clean entrances (1).

**Constraints:**
- Do not modify the netplay integration or the pad-input contract (MEMORY.md).
- Prefer combos of the existing 15 whitelisted inputs for new moves. Any NEW
  input key must be flagged at the top of the PR description.
- Keep the skull-arena direction and the directional-grapple set from PR #1
  where they work (grab + direction + Punch/Kick = 8 moves; Run+Punch =
  clothesline; Run+Kick = dropkick).

**Acceptance:**
1. A match can be played start to finish with every listed move visibly
   performing as named.
2. No still-photo move cards, no black-space move cut-ins.
3. Muse's netplay patch applies cleanly and the online smoke test passes.
4. Leon playtests and approves (final gate — not done until he says so).

---

## TASK-002 — Standing review duty

- **Owner:** Muse · **Status:** ONGOING
- Review every Codex PR against MEMORY.md constraints, run the netplay
  compatibility checks and smoke test, publish a test build for Leon's
  playtest, and update MEMORY.md/TASKS.md after each merge.
