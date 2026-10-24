# Browser Tetris

## Purpose and users

Provide a responsive single-player browser Tetris game for desktop keyboard users. Run as a static website without an account or backend. Clearly explain controls and expose the game's current score and state.

## Intended capabilities

- A 10×20 board, seven tetrominoes, movement, rotation, soft drop, fixed gravity, line clearing, line-based scoring, game over and restart.
- Hold, a ghost landing preview, seven-bag randomization, SRS wall kicks, hard drop and grounded lock delay.
- Ghost visibility that hides the whole projection if any projected cell is above the board midline.
- A bonus-funded penetrator ability that passes through settled cells, uses a valid deepest landing preview and renders the active piece white; inventory is capped at three bonuses.

## Goals and constraints

Use TypeScript, a pure game engine, a Canvas board and ordinary HTML controls. Keep rules independent of browser APIs so deterministic tests can exercise gameplay. Fixed gravity and simple scoring keep the game focused on placement.

Verify browser behavior in dedicated, isolated Chromium and Firefox environments under the root [browser development policy](../../BROWSER_DEV_POLICY.md). Use keyboard-operable controls, visible focus and readable instructions.

An activated penetrator cannot be held. Settled cells remain intact while it traverses them; locking must never overlap them. Hard drop and ghost must use the same deepest legal destination.

## Non-goals

Multiplayer, accounts, backend leaderboards, touch controls, progressive speed levels and saved game progress are excluded.

## Decision boundaries

Detailed behavior and acceptance belong to [SPEC](SPEC.md). Structural rationale belongs to [ARCHITECTURE](ARCHITECTURE.md). The first playable release is planned as v0.1.0; releases describe verified integrated implementation.
