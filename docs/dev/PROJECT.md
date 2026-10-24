# Browser Tetris

## Purpose and users

Provide a responsive single-player browser Tetris game for desktop keyboard users. Run as a static website without an account or backend. Clearly explain controls and expose the game's current score and state.

## Intended capabilities

- A 10×20 board, seven tetrominoes, movement, rotation, soft drop, fixed gravity, line clearing, line-based scoring, game over and restart.
- Hold, a ghost landing preview, seven-bag randomization, SRS wall kicks, hard drop and grounded lock delay.

## Goals and constraints

Use TypeScript, a pure game engine, a Canvas board and ordinary HTML controls. Keep rules independent of browser APIs so deterministic tests can exercise gameplay. Fixed gravity and simple scoring keep the game focused on placement.

Verify browser behavior in dedicated, isolated Chromium and Firefox environments under the root [browser development policy](../../BROWSER_DEV_POLICY.md). Use keyboard-operable controls, visible focus and readable instructions.

## Non-goals

Multiplayer, accounts, backend leaderboards, touch controls, progressive speed levels and saved game progress are excluded.

## Decision boundaries

Detailed behavior and acceptance belong to [SPEC](SPEC.md). Structural rationale belongs to [ARCHITECTURE](ARCHITECTURE.md). The first playable release is planned as v0.1.0; releases describe verified integrated implementation.
