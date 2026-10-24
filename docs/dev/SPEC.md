# System specification

## Context and terms

A static single-player browser Tetris game governed by [PROJECT](PROJECT.md), [ARCHITECTURE](ARCHITECTURE.md) and [DECOMPOSITION](DECOMPOSITION.md). Requirement IDs below are stable. A placement is the four board cells obtained from piece identity, rotation and top-left position; a snapshot includes settled cells, active piece, score and running/game-over state. A command is processed atomically. Rejected commands preserve state unless a contract explicitly defines game over.

## B01 — Board, pieces and start

Owner: C-BOARD/C-ENGINE in [DECOMPOSITION](DECOMPOSITION.md).

Use x=0…9 and y=0…19, with y increasing down. Settled cells contain one piece identity or empty. Start with an empty board and score 0. Use the seven tetrominoes I,O,T,S,Z,J,L; spawn masks in their standard orientation, horizontally centered, top occupied row y=0. Store explicit four-orientation masks (O invariant); I uses its standard 4×4 rotation frame and J/L/S/T/Z use 3×3. A piece whose spawn cells collide ends the game. No hidden occupied rows or partial above-board movement is permitted.

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

ArrowLeft/ArrowRight attempt one column per keydown, including delivered browser repeats. ArrowDown attempts one row without scoring. ArrowUp or X rotates clockwise; Z rotates counterclockwise. O rotation is a no-op. Ordinary translation respects board bounds/collision; rotation follows E02. Failed rotation leaves position and orientation unchanged. Rotation/one-shot actions ignore auto-repeat.

Acceptance: Exercise left/right/bottom/top boundaries and collision rejection in each orientation; rejected actions leave state unchanged.

## B03 — Gravity and baseline locking

Owner: C-ENGINE/C-INPUT in [DECOMPOSITION](DECOMPOSITION.md).

Gravity interval is fixed at 1000 ms of active game time. A successful downward step restarts its gravity-step interval. The general locking default and grounded timing follow E05; failed-attempt locking locks on a failed gravity or soft-drop step. Movement/rotation do not reset the gravity-step clock. No input awards drop points. At equal timestamps, process a due lock deadline, then a due gravity step, then the external command; never apply an old gameplay command to a newly spawned piece in the same timestamp dispatch.

Acceptance: With an injected clock, test 999/1000 ms, soft-drop failure, large elapsed updates and command/deadline ties. Partitioned and combined elapsed updates produce equivalent states for the same events.

## B04 — Atomic settlement, scoring and restart

Owner: C-ENGINE/C-BOARD in [DECOMPOSITION](DECOMPOSITION.md).

Lock only when all four cells are in bounds and non-overlapping. Merge exactly those four cells, remove all full rows simultaneously, shift rows down preserving order, and prepend empty rows. Score 100/300/500/800 for 1/2/3/4 cleared rows and 0 otherwise. Spawn a fresh piece after settlement and game-over on spawn collision. Restart via R or the HTML button clears board, score and active lifecycle and starts a new random sequence.

Acceptance: Test zero through four simultaneous rows, row-order preservation, single scoring transaction, blocked spawn, ignored terminal gameplay, and restart from both running and terminal states.

## B05 — Browser lifecycle and usable presentation

Owner: C-INPUT/C-VIEW in [DECOMPOSITION](DECOMPOSITION.md).

Show board, active piece, score, game-over status, keyboard instructions and a native restart button. Make the game surface keyboard focusable and label its purpose. Use distinct non-white regular-piece colors and consistent settled-cell identities. Canvas scales without changing logical geometry. Suppress gameplay-key browser defaults only when game surface has focus; never hijack form/button shortcuts. On blur/hidden page suspend game time and clear held input; resume with a fresh browser timestamp, preserving remaining game deadlines. Dispose removes listeners and frame ownership.

Acceptance: In Chromium and Firefox, exercise actual keyboard/focus, visible output/screenshots, blur/time suspension, restart and listener teardown. Core game runs without a backend.

## E01 — Seven-bag supply

Owner: C-PIECE in [DECOMPOSITION](DECOMPOSITION.md).

Shuffle one copy of each tetromino with the injected random source, exhaust that bag before drawing the next. Hold and preview consumers observe the same queue. Gameplay has no production seed query parameter.

Acceptance: For seeded fixtures, each consecutive bag of seven has all seven identities, boundaries remain unbiased by hold, and supply is reproducible.

## E02 — SRS wall kicks

Owner: C-BOARD/C-PIECE in [DECOMPOSITION](DECOMPOSITION.md).

Use standard SRS four-state clockwise/counterclockwise transitions for I and J/L/S/T/Z with their separate ordered kick tables; convert SRS y-up offsets to board y-down exactly once. Test the unshifted rotation first, then ordered offsets; choose the first legal result. O does not translate. Reject when all candidates fail.

Acceptance: Use explicit expected fixtures for wall, floor, stack, I-specific offsets, every directed transition and all-candidate rejection; assert ordered selection rather than merely some successful rotation.

### Canonical kick offsets

Offsets below are already in board coordinates (positive y down); do not invert them again. Prefix every row with (0,0), then try the listed four offsets in order.

| Transition | J/L/S/T/Z | I |
| --- | --- | --- |
| 0→R | `(-1,0),(-1,-1),(0,2),(-1,2)` | `(-2,0),(1,0),(-2,1),(1,-2)` |
| R→0 | `(1,0),(1,1),(0,-2),(1,-2)` | `(2,0),(-1,0),(2,-1),(-1,2)` |
| R→2 | `(1,0),(1,1),(0,-2),(1,-2)` | `(-1,0),(2,0),(-1,-2),(2,1)` |
| 2→R | `(-1,0),(-1,-1),(0,2),(-1,2)` | `(1,0),(-2,0),(1,2),(-2,-1)` |
| 2→L | `(1,0),(1,-1),(0,2),(1,2)` | `(2,0),(-1,0),(2,-1),(-1,2)` |
| L→2 | `(-1,0),(-1,1),(0,-2),(-1,-2)` | `(-2,0),(1,0),(-2,1),(1,-2)` |
| L→0 | `(-1,0),(-1,1),(0,-2),(-1,-2)` | `(1,0),(-2,0),(1,2),(-2,-1)` |
| 0→L | `(1,0),(1,-1),(0,2),(1,2)` | `(-1,0),(2,0),(-1,-2),(2,1)` |

## E03 — Hold piece

Owner: C-PIECE/C-ENGINE in [DECOMPOSITION](DECOMPOSITION.md).

C or Shift holds at most once per active-piece lifecycle, subject to the penetrator restriction in P02 and feature availability in C02. Empty hold stores the current identity and consumes the next queue piece; occupied hold swaps without drawing from the queue. A held piece returns in spawn orientation/position with fresh gravity and grounded state. Hold becomes available after lock; a colliding replacement spawn ends the game.

Acceptance: Verify empty/occupied hold, repeated rejected hold, queue consumption, orientation reset and replacement spawn collision.

## E04 — Landing query, ghost and hard drop

Owner: C-BOARD/C-PIECE/C-VIEW in [DECOMPOSITION](DECOMPOSITION.md).

Space performs hard drop to the canonical landing: for an ordinary piece, descend from current position until the next row is blocked. Draw an outline ghost at the exact target with no board mutation, subject to G01 and C01; suppress a coincident ghost under the active piece to avoid obscuring it. Hard drop awards no points. Unless C02 selects immediate hard-drop locking, it uses the general locking rule: under failed-attempt locking, its terminal failed downward attempt locks; under interval locking it starts or preserves the grounded timer. Ignore repeated hard-drop keydown events.

Acceptance: Assert hard-drop and ghost cell equality on empty and irregular stacks, no tunneled ordinary drop, no board mutation by projection, and timing-policy behavior.

## E05 — Full-interval grounded lock delay

Owner: C-ENGINE in [DECOMPOSITION](DECOMPOSITION.md).

Default general locking policy is interval. A grounded piece has no further valid downward progress. Start a 1000 ms deadline on entering grounded state, including spawn, soft/gravity descent and hard drop. Grounded horizontal/rotation actions and repeated hard drops do not restart it. Becoming airborne cancels it; re-grounding starts a fresh full interval. Failed downward attempts do not shorten it. At expiry, recheck landing validity and lock exactly once. Blur freezes both gravity and lock time.

Acceptance: Check contact at t=0, 999 and 1000 ms; grounded motion, airborne cancellation/re-grounding, repeated hard drop, spawn-grounded cases, timer ties and large updates.

## G01 — Dynamic ghost boundary

Owner: C-VIEW in [DECOMPOSITION](DECOMPOSITION.md).

Numbered board rows 0…9 are upper half and 10…19 lower half. In dynamic mode show the whole ghost only when every projected cell has y≥10; a projection containing y=9 is hidden even if other cells are lower. Visibility is recomputed after every relevant state change from the canonical landing.

Acceptance: Test min landing y=9/10, a piece straddling rows 9/10, and movement/rotation causing hide/show in both directions; hiding does not affect hard drop.

## P01 — Activation, traversal and legal landing

Owner: C-ENGINE/C-BOARD/C-PIECE in [DECOMPOSITION](DECOMPOSITION.md).

P activates only for a running ordinary piece when inventory>0; spend one bonus atomically and set active mode penetrator. Repeated activation, repeat keydown and unavailable activation do nothing. Recompute grounded state on activation; a newly deeper destination cancels the old grounded deadline as airborne. Reject hold without resetting that deadline. Traversal ignores settled occupancy but respects board bounds; never destroy settled cells. For its current column/orientation and current-or-lower top-left y, enumerate all fully in-bounds, non-overlapping placements and select the deepest. Gravity and soft drop advance toward that destination, passing through occupied intermediate positions; that destination defines grounded state. Hard drop and ghost use it directly. Lateral/rotation candidates may overlap intermediate settled cells only if they have a legal current-or-lower landing. Reject a candidate without one. If a required landing/lock operation has no valid candidate, end the game without modifying settled cells.

Acceptance: Fixtures include an upper blocker with a deeper cavity, multiple disjoint valid rows, bottom obstruction, overlapping transit, rejected no-destination lateral/rotation, and no-landing terminal failure. Assert deepest legal candidate and no overwritten cells.

## P02 — Penetrator hold, lock and rewards

Owner: C-ENGINE/C-PIECE in [DECOMPOSITION](DECOMPOSITION.md).

Disable hold while penetrator mode is active, without consuming hold eligibility or queue entries. Lock uses the selected ordinary timing policy at the penetrator landing and rechecks full bounds/no overlap. Mode ends at lock; spawn/hold replacements are ordinary. A four-line clear awards one bonus after settlement, saturating at three; other clears award none. Restart clears inventory. Settled penetrator cells retain their tetromino identity and ordinary palette.

Acceptance: Verify disabled hold, one spend per activation, delay/immediate policy interactions, post-lock mode reset, rewards at 0/2/3 bonuses and restart reset.

## P03 — Penetrator presentation

Owner: C-VIEW in [DECOMPOSITION](DECOMPOSITION.md).

Render every cell and border of the active penetrator entirely white; active ordinary and settled pieces never use white. Render a visible penetrator ghost as a white outline. Side panel shows exactly one lightning glyph per available bonus, with an accessible numeric label even at zero. Update on every award/spend and restart.

Acceptance: Inspect screenshots for white active mode and ordinary settled colors; verify accessible count and 0–3 glyph updates after earn/spend.

## C01 — Configuration controls and defaults

Owner: C-SETTINGS/C-INPUT/C-VIEW in [DECOMPOSITION](DECOMPOSITION.md).

Use six native labeled controls: ghost hidden/dynamic/shown (default dynamic), hardDrop true/false (true), next true/false (true), hardDropLock general/immediate (general), lock failed/interval (interval), hold true/false (true). Show one next piece in spawn orientation without consuming supply. Invalid in-memory settings changes are rejected without state mutation. In hidden ghost mode show no ghost; in shown mode apply no midline restriction; coincident ghost suppression still applies.

Acceptance: Check all control options, defaults, keyboard form operation, next queue identity/no consumption, hidden/shown/dynamic differences and invalid change rejection.

## C02 — Live settings transition

Owner: C-SETTINGS/C-INPUT/C-ENGINE in [DECOMPOSITION](DECOMPOSITION.md).

Apply a validated user change before the next input/frame render, without restarting game. Disabling hard drop or hold rejects its action without spending/consuming state; retain held identity for re-enable. Visibility changes redraw immediately. Hard-drop immediate locks a valid hard-drop destination in the same command; follow-general obeys selected lock mode. Changing general lock policy cancels the old grounded deadline; if newly interval and grounded, start a fresh full interval; if failed, wait for the next failed downward attempt. Same-value changes do not reset timers. Changing hard-drop policy alone does not retroactively lock an already dropped piece. Settings and held state survive feature toggles; restart clears held/game state but retains selected settings.

Acceptance: Exercise each toggle mid-fall/grounded/game-over, lock-policy changes at 999 ms, same-value no-reset, disabled keyboard actions and form-focus isolation. Session-only settings reset on reload.

## Q01 — Verification and distribution

The runtime must be deployable as static assets with no backend. A clean locked dependency installation, TypeScript check, production build and deterministic engine tests form the local build gate. Browser acceptance targets isolated Chromium headless shell and Playwright-managed Firefox, using the compatible locked runner and [BROWSER_DEV_POLICY](../../BROWSER_DEV_POLICY.md). Establish actual launch, interaction, rendering/screenshot and teardown capability before dependent tests.

Test actual application/server input and render paths, inspect screenshots and verify score/state text; DOM assertions alone cannot certify Canvas output. A test-only fixture seam may inject deterministic engine states into tests without exposing a production debug endpoint. Do not count skipped browser coverage as passed. User-facing controls require labels, visible focus, readable text and keyboard access; Canvas is accompanied by status text rather than a promise of full screen-reader board navigation.

## Scope exclusions

No accounts, multiplayer, backend services, touch controls, progressive gravity levels or saved board/game progress. Requirement IDs B01–B05 define the core game; other listed requirements define only the capabilities currently specified. No unspecified feature is required.
