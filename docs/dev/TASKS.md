# Implementation tasks

All implementation work is pending. [SPEC](SPEC.md) owns behavior, [PLAN](PLAN.md) owns phase/milestone scope and exits, and [layout](layout.md) owns physical paths. IDs are stable and project-wide; review tasks are executable work within a selected range. Every delivery task includes relevant tests and documentation, and implementation uses the task commit/publication contract in root instructions.

## Phase 1 — Playable classic baseline

- [ ] Phase 1 — Playable classic baseline
    - [ ] Milestone 1.1 — Deterministic placement foundation
        - [ ] T-001 — Establish the isolated build and test environment
            Scope: package.json, package-lock.json, tsconfig.json, vite.config.ts, playwright.config.ts. Depends on: none.
            Contract: B01,Q01 in SPEC. Outcome/evidence: Create locked TypeScript/Vite/Vitest/Playwright tooling and build commands; provision and exercise both required isolated browsers following the central policy. Retain actual runner/binary versions, installation/interaction/teardown evidence and limitations. Do not close if required provisioning remains blocked.
        - [ ] T-002 — Define board geometry and tetromino masks
            Scope: src/domain/board.ts, src/domain/pieces.ts, tests/unit. Depends on: T-001.
            Contract: B01,B02 in SPEC. Outcome/evidence: Implement explicit masks, coordinate conversion, legal placement, rotation and row compaction primitives with boundary fixtures.
        - [ ] T-003 — Implement spawn and directional command transitions
            Scope: src/domain/game.ts, tests/unit. Depends on: T-002.
            Contract: B01,B02 in SPEC. Outcome/evidence: Implement seeded independent piece supply, running/game-over lifecycle and atomic translation/rotation rejection; test spawn collisions and unchanged rejected state.
        - [ ] T-004 — Review, test and report milestone 1.1
            Depends on: T-001, T-002, T-003. Review the complete milestone code and integrations separately from test execution; repair required findings and verify exits/regressions. Record actual checks, limits and eligible TODOs with options/ownership.
            Report: docs/dev/reports/phases/1/1.1.md. Publish evidence and close constituent issues before milestone closure.
    - [ ] Milestone 1.2 — Playable browser loop
        - [ ] T-005 — Implement chronological gravity and baseline locking
            Scope: src/domain/game.ts, src/app/controller.ts, tests/unit. Depends on: T-004.
            Contract: B03 in SPEC. Outcome/evidence: Advance explicit active game time with chronological ordering, downward steps and failed-attempt lock; test elapsed partition equivalence, deadline ties and blur-time adapter behavior.
        - [ ] T-006 — Implement settlement, score and restart
            Scope: src/domain/game.ts, src/domain/board.ts, tests/unit. Depends on: T-005.
            Contract: B04 in SPEC. Outcome/evidence: Integrate simultaneous row clear, exact score increments, fresh spawn, terminal rejection and clean restart in one lock transaction.
        - [ ] T-007 — Integrate Canvas, keyboard controls and status
            Scope: index.html, src/main.ts, src/app/controller.ts, src/ui, tests/browser. Depends on: T-006.
            Contract: B05 in SPEC. Outcome/evidence: Render playable state, accessible score/status and restart; scope keyboard handlers to game focus and verify frame/listener disposal and blur suspension.
        - [ ] T-008 — Review, test and report milestone 1.2
            Depends on: T-005, T-006, T-007. Review the complete milestone code and integrations separately from test execution; repair required findings and verify exits/regressions. Record actual checks, limits and eligible TODOs with options/ownership.
            Report: docs/dev/reports/phases/1/1.2.md. Publish evidence and close constituent issues before milestone closure.
    - [ ] Milestone 1.3 — Verified static distribution
        - [ ] T-009 — Verify baseline gameplay in both target browsers
            Scope: tests/browser, tests/fixtures, playwright.config.ts. Depends on: T-008.
            Contract: B01–B05,Q01 in SPEC. Outcome/evidence: Exercise actual keyboard play, scoring/restart fixtures, game over and focus lifecycle on Chromium and Firefox; inspect saved Canvas screenshots and repair required failures.
        - [ ] T-010 — Prepare static build, instructions and baseline release inputs
            Scope: README.md, package.json, RELEASE-NOTES.md, scripts/package.mjs, tests/package. Depends on: T-009.
            Contract: Q01 in SPEC. Outcome/evidence: Verify a clean production build and static preview without backend; document actual setup/controls and package generated static assets with version v0.1.0. Prepare exact release notes; publication occurs only after completed phase integration.
        - [ ] T-011 — Review, test and report milestone 1.3
            Depends on: T-009, T-010. Review the complete milestone code and integrations separately from test execution; repair required findings and verify exits/regressions. Record actual checks, limits and eligible TODOs with options/ownership.
            Report: docs/dev/reports/phases/1/1.3.md. Publish evidence and close constituent issues before milestone closure.
    - [ ] Milestone 1.4 — Phase review
        - [ ] T-012 — Review, test and report phase 1
            Depends on: delivery milestones 1.1, 1.2, 1.3 complete/closed, including their review tasks. Review cross-milestone code/invariants, run included SPEC exits and preserved regressions, repair blockers, and reconcile required reports and TODOs.
            Report: docs/dev/reports/phases/1/PHASE-REPORT.md. Also produce docs/dev/reports/IMPLEMENTATION-REPORT.md with the full-list outcome and aggregated unresolved/deferred TODOs when this completes the intended list. After verified phase closure, integrate/recheck/publish the default branch and publish release v0.1.0 under the separately authorized release workflow.
