# Shared memory — Onyx WrestleFest

_Last updated by Muse, 2026-11-03. Update this file whenever a fact changes._

## Division of labor (set by Leon)

- **Muse:** online multiplayer networking ONLY (plus goals, this memory,
  task assignments, PR review, deploys).
- **Codex:** gameplay, graphics, wrestling mechanics, AI, local multiplayer —
  per tasks in `collab/TASKS.md`. (ChatGPT did earlier gameplay work; Codex is
  the builder going forward.)
- **Leon:** direction and playtest verdicts.

## Dev rules (agreed 2026-11-02)

1. Gameplay changes must never overwrite Muse's netplay integration.
2. Any new input must also be added to the server's INPUT_KEYS whitelist in the
   same pass — flag it in the PR; Muse makes the server change.
3. Separate branches for gameplay work; test before merging to the live build.
4. Priority = actual gameplay (animations, movement, grappling, impacts,
   opponent behavior), not menus/settings.
5. Features are verified in-game, not by syntax checks.

## Netplay (Muse's block — do not rewrite)

- Server: separate repo `leonzeigler/onyx-wrestlefest-netplay`, hosted on
  Render at `wss://onyx-wrestlefest-netplay.onrender.com` (free tier — first
  connection after idle can take ~50s). Host-authoritative frame relay,
  6-char room codes, host + up to 5 guests, session tokens, 45s rejoin hold.
- Client: `netplay-client.js` (`window.WFNet`) is spliced into the game build
  by Muse's patch step together with the netplay block in `index.html`.
  Gameplay code calls the local pad-input function; the netplay layer reads it.
- The input message requires a `room` field matching the socket's room.
- **INPUT_KEYS whitelist (15):** left, right, up, down, punch, kick, grapple,
  whip, fin, run, tag, apron, start, guard, counter. New moves should be
  combos of existing keys (direction + button) whenever possible — combos
  need no server change.
- Controls note: TAG button and apron-partner controls appear ONLY in tag
  matches — removed in singles and Royal Rumble matches.
- Every fighter needs a visible, in-game move list. A move the announcer calls
  must visibly BE that move (a hip toss must look like a hip toss).

## Live build & deploy

- Live game page: https://onyx-wrestlefest-online.netlify.app
- ⚠️ DEPLOY GOTCHA: the Multiplayer panel's server address prefill
  (`value="wss://onyx-wrestlefest-netplay.onrender.com"` on the `#wfServer`
  input) is NOT in the repo source — Muse re-applies it by hand on every
  deploy, or the panel ships blank.
- Phone builds are LANDSCAPE. On-screen touch buttons stay in every build
  (other players on phones need them) alongside gamepad support.

## Current state (2026-11-03)

- `main` = the pre-overhaul build with Muse's netplay integration (verified:
  local suites 28/28 + 12/12, live Render test 9/9, two-tab browser smoke test).
- Draft PR #1, branch `gameplay/skull-arcade-stage-2026-11-02` (from earlier
  ChatGPT work): skull arcade arena + directional grapples (8 moves from
  grab + direction + Punch/Kick) + running clothesline/dropkick. Netplay
  compatibility verified by Muse. NOT merged — waiting on Leon's playtest at
  https://onyx-wf-branch-test.surge.sh

## Leon's playtest verdict, 2026-11-02 — "still terrible", "still not like WrestleFest"

The 12 issues the overhaul must fix:
1. Entrances are choppy; stray lines appear above/beside characters walking out.
2. Crowd is too large.
3. Doesn't look like an arena.
4. Moves are just photos of moves in black spaces.
5. The pictured move doesn't match the move performed/called.
6. Only punch, kick, and Irish whip really work.
7. Can't climb the ropes.
8. Ropes don't match the game (reference).
9. Ropes don't mesh well visually.
10. Running slides in one stride — worst on the Irish whip.
11. Teleport-slide movement.
12. Both players slide to the ropes.
