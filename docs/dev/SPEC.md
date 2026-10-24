# System specification

## Context and terms

A static single-player browser Tetris game governed by [PROJECT](PROJECT.md), [ARCHITECTURE](ARCHITECTURE.md) and [DECOMPOSITION](DECOMPOSITION.md). Requirement IDs below are stable. A placement is the four board cells obtained from piece identity, rotation and top-left position; a snapshot includes settled cells, active piece, score and running/game-over state. A command is processed atomically. Rejected commands preserve state unless a contract explicitly defines game over.

## B01 — Board, pieces and start

Owner: C-BOARD/C-ENGINE in [DECOMPOSITION](DECOMPOSITION.md).

Use x=0…9 and y=0…19, with y increasing down. Settled cells contain one piece identity or empty. Start with an empty board and score 0. Use the seven tetrominoes I,O,T,S,Z,J,L; spawn masks in their standard orientation, horizontally centered, top occupied row y=0. Store explicit four-orientation masks (O invariant); I uses its standard 4×4 rotation frame and J/L/S/T/Z use 3×3. Choose each piece independently with equal probability through the injected random source. A piece whose spawn cells collide ends the game. No hidden occupied rows or partial above-board movement is permitted.

Acceptance: Assert each spawn has four distinct in-bounds cells; a blocked spawn enters game over without changing settled cells.

### Piece geometry

The spawn masks below use `.` for empty and `#` for occupied, with rows separated by `/`. For each spawn set top-left x=floor((10−frame width)/2) and top-left y=−(first occupied row index), placing the first occupied row at y=0. Rotate the complete square frame clockwise by (x,y)→(N−1−y,x), counterclockwise by (x,y)→(y,N−1−x); O remains fixed. Rotation states are 0,R,2,L. Reject out-of-bounds occupied cells even if frame padding itself lies outside the board.

| Identity | Spawn mask |
| --- | --- |
| I | `..../####/..../....` |
| O | `##/##` |
| T | `.#./###/...` |
| S | `.##/##./...` |
| Z | `##./.##/...` |
| J | `#../###/...` |
| L | `..#/###/...` |

## B02 — Movement and rotation

Owner: C-BOARD/C-ENGINE in [DECOMPOSITION](DECOMPOSITION.md).

ArrowLeft/ArrowRight attempt one column per keydown, including delivered browser repeats. ArrowDown attempts one row without scoring. ArrowUp or X rotates clockwise; Z rotates counterclockwise. O rotation is a no-op. Reject any ordinary move or rotation that leaves the board or overlaps settled cells; failed rotation leaves position and orientation unchanged. Rotation/one-shot actions ignore auto-repeat.

Acceptance: Exercise left/right/bottom/top boundaries and collision rejection in each orientation; rejected actions leave state unchanged.

## B03 — Gravity and baseline locking

Owner: C-ENGINE/C-INPUT in [DECOMPOSITION](DECOMPOSITION.md).

Gravity interval is fixed at 1000 ms of active game time. A successful downward step restarts its gravity-step interval. Under failed-attempt locking, a failed gravity or soft-drop step locks the current piece. Movement/rotation do not reset the gravity-step clock. No input awards drop points. At equal timestamps, process a due gravity step, then the external command; never apply an old gameplay command to a newly spawned piece in the same timestamp dispatch.

Acceptance: With an injected clock, test 999/1000 ms, soft-drop failure, large elapsed updates and command/deadline ties. Partitioned and combined elapsed updates produce equivalent states for the same events.

## B04 — Atomic settlement, scoring and restart

Owner: C-ENGINE/C-BOARD in [DECOMPOSITION](DECOMPOSITION.md).

Lock only when all four cells are in bounds and non-overlapping. Merge exactly those four cells, remove all full rows simultaneously, shift rows down preserving order, and prepend empty rows. Score 100/300/500/800 for 1/2/3/4 cleared rows and 0 otherwise. Spawn a fresh piece after settlement and game-over on spawn collision. Restart via R or the HTML button clears board, score and active lifecycle and starts a new random sequence.

Acceptance: Test zero through four simultaneous rows, row-order preservation, single scoring transaction, blocked spawn, ignored terminal gameplay, and restart from both running and terminal states.

## B05 — Browser lifecycle and usable presentation

Owner: C-INPUT/C-VIEW in [DECOMPOSITION](DECOMPOSITION.md).

Show board, active piece, score, game-over status, keyboard instructions and a native restart button. Use distinct non-white regular-piece colors and consistent settled-cell identities. Canvas scales without changing logical geometry. Suppress gameplay-key browser defaults only when game surface has focus; never hijack form/button shortcuts. On blur/hidden page suspend game time and clear held input; resume with a fresh browser timestamp, preserving remaining game deadlines. Dispose removes listeners and frame ownership.

Acceptance: In Chromium and Firefox, exercise actual keyboard/focus, visible output/screenshots, blur/time suspension, restart and listener teardown. Core game runs without a backend.

## Q01 — Verification and distribution

The runtime must be deployable as static assets with no backend. A clean locked dependency installation, TypeScript check, production build and deterministic engine tests form the local build gate. Browser acceptance targets isolated Chromium headless shell and Playwright-managed Firefox, using the compatible locked runner and [BROWSER_DEV_POLICY](../../BROWSER_DEV_POLICY.md). Establish actual launch, interaction, rendering/screenshot and teardown capability before dependent tests. No browser installation or execution is claimed by this specification.

Test actual application/server input and render paths, inspect screenshots and verify score/state text; DOM assertions alone cannot certify Canvas output. A test-only fixture seam may inject deterministic engine states into tests without exposing a production debug endpoint. Do not count skipped browser coverage as passed. User-facing controls require labels, visible focus, readable text and keyboard access; Canvas is accompanied by status text rather than a promise of full screen-reader board navigation.

## Scope exclusions

No accounts, multiplayer, backend services, touch controls, progressive gravity levels or saved board/game progress. Requirement IDs B01–B05 define the core game; other listed requirements define only the capabilities currently specified. No unspecified feature is required.
