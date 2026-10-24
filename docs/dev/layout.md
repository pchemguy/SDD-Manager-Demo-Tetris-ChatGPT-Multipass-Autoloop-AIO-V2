# Physical layout

The paths below are intended implementation homes; listing them does not claim implementation exists. Existing root policies and `.agents/` packages remain governing inputs. [DECOMPOSITION](DECOMPOSITION.md) owns logical boundaries and [PLAN](PLAN.md) owns delivery order.

| Intended path | Owner and purpose | Verification home |
| --- | --- | --- |
| src/domain/board.ts, src/domain/pieces.ts | C-BOARD: cell geometry, masks, rotation and row compaction | tests/unit/board.test.ts, tests/unit/pieces.test.ts |
| src/domain/game.ts | C-ENGINE: atomic command/time/lifecycle state | tests/unit/game.test.ts |
| src/domain/randomizer.ts | C-PIECE: seeded bag supply; geometry in pieces.ts/board.ts and hold lifecycle in game.ts | tests/unit/randomizer.test.ts and piece/game fixtures |
| src/app/controller.ts | C-INPUT: events, active time, frame/listener lifecycle | tests/unit/controller.test.ts; tests/browser/lifecycle.spec.ts |
| src/settings/model.ts | C-SETTINGS: six-field schema, defaults and validation | tests/unit/settings.test.ts |
| src/settings/browser-config.ts | C-CONFIG: cookie/query resolution and best-effort persistence | tests/unit/browser-config.test.ts; tests/browser/settings.spec.ts |
| src/ui/render.ts, src/ui/panel.ts, src/ui/styles.css | C-VIEW: Canvas drawing, native controls and status | tests/browser/gameplay.spec.ts; screenshot evidence |
| src/main.ts, index.html | Application composition and one controller root | tests/browser/smoke.spec.ts |
| package.json, package-lock.json, tsconfig.json, vite.config.ts | Locked toolchain and static build ownership | Clean install, typecheck and build gates |
| playwright.config.ts, tests/browser, tests/fixtures | Isolated browser runner and test-only deterministic fixtures | Chromium/Firefox application acceptance |
| scripts/package.mjs, tests/package | Static archive creation and package integrity | Archive content and static-preview checks |
| docs/dev, README.md, RELEASE-NOTES.md | Design/contract/plan/task owners, actual user setup and version notes | Document links and release-source checks |
| docs/dev/reports/phases/<phase-id> | Milestone and phase implementation evidence | <milestone-id>.md and PHASE-REPORT.md |
| docs/dev/reports/IMPLEMENTATION-REPORT.md | Final report and aggregated TODO provenance | Final phase review |
| dist/, artifacts/, .browser-state/ | Ignored generated static output, screenshots/archives and isolated browser state | Never commit binaries, profiles, cookies or generated build output |

## Placement and dependency rules

Domain imports only domain types/functions. Controller composes domain and view; rendering consumes snapshots and emits intents. Shared data types remain with the domain or settings owner that defines them; do not create a speculative shared framework. Co-locate focused test fixtures under tests; production bundles contain no test-state injection entry. Static packaging consumes dist rather than source or credential directories.

Browser binaries and state belong in an absolute dedicated installation selected under [BROWSER_DEV_POLICY](../../BROWSER_DEV_POLICY.md); the runner and every child must use that same location. Generated artifacts are excluded from tracked source. Isolation must be verified, not inferred from a folder name. Never use system/personal profiles. The project does not alter global browsers or toolchains.

Root AGENTS links current governing documents. Validated setup commands will be added when implementation establishes them; no proposed command is represented as already run. Manual records under docs/ai-logs are outside routine development-document checks.
