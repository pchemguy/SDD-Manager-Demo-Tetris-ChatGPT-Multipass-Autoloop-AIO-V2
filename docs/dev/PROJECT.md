# Browser Tetris

## Purpose and users

Provide a small, playable browser Tetris game for a single player using a desktop keyboard. The intended outcome is a responsive, understandable game that can run as a static website without an account or backend.

## Scope

- A 10-column by 20-row board and the seven standard tetrominoes.
- Falling pieces, horizontal movement, rotation and player-controlled downward movement.
- Automatic gravity, collision-safe placement and clearing completed horizontal lines.
- Line-based scoring, visible score, game-over detection and restart.
- A clearly rendered board and concise keyboard instructions.

## Goals and constraints

Use TypeScript, a pure game engine, a Canvas board and ordinary HTML controls. Keep the game rules independent of browser rendering so deterministic tests can exercise gameplay. Use fixed gravity and simple scoring; avoid additional progression systems.

Verify browser behavior in dedicated, isolated Chromium and Firefox environments under the root [browser development policy](../../BROWSER_DEV_POLICY.md). The game must remain usable with keyboard controls, visible focus and readable instructions.

## Non-goals

Hold, ghost, next-piece preview, hard drop, wall kicks, bag randomization, special abilities and configurable settings are outside this scope. Also excluded are multiplayer, accounts, network services, touch controls and saved game progress.

## Decisions

There are no unresolved principal-scope decisions. Detailed controls, scoring values, rotation rules and acceptance scenarios belong to the specification. The first playable version is planned as v0.1.0; a release represents verified, integrated implementation rather than document preparation.
