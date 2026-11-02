# Onyx WrestleFest — Browser Game

This repository is for the **game client**: `index.html`, `icon.webp`, and all `assets/` files.

## IMPORTANT: Separate AI responsibilities

- **Game client (this repository):** characters, controls, combat, collision, match rules, UI, presentation, and local multiplayer.
- **Network relay (leonzeigler/onyx-wrestlefest-netplay):** Node.js/WebSocket server, rooms, transport, reconnection, and host/guest messaging.

The netplay server is **NOT INCLUDED** in this game-source repository package. Do not overwrite the other AI's server code.

## Install or preview

The site is static: open `index.html` in a browser, or serve from a simple local static server such as `python -m http.server 8000`.
The online mode requires a separately deployed WebSocket relay and integration tests.

## What this gameplay version changes
- Strike contact happens after a windup, not immediately on input.
- CPU attack distance respects the actual fighter collision geometry.
- Endurance costs for offense and guarding.
- Blocking, timed counters, and basic combo feedback.

These changes were checked with JavaScript syntax validation and focused combat-function tests, **not** complete live gameplay testing.

## Safe branching and integration workflow

1. Keep `main` stable.
2. Create a branch like `gameplay/combat-upgrade` before editing gameplay.
3. Let the other AI work on `onyx-wrestlefest-netplay` independently.
4. Coordinate shared changes to the **network protocol** (input keys, state updates, frame format) explicitly.
5. Review changed files before merging; do not blindly replace `index.html` with older snapshots.
6. Test local game modes and six-person netplay before deploying.

## Release checklist
- Verify roster, menus, career, all match types, keyboard, touch and gamepad input.
- Test gamepad assignments for up to 6 local players.
- Test host + five guests on separate browsers, including disconnect/rejoin.
- Verify your configured wss endpoint is reachable and is appropriate for deployment.
- Validate art and audio load in the deployed Netlify site.
