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
            Report: docs/dev/reports/phases/1/PHASE-REPORT.md. After verified phase closure, integrate/recheck/publish the default branch and publish release v0.1.0 under the separately authorized release workflow.

## Phase 2 — Modern piece control

- [ ] Phase 2 — Modern piece control
    - [ ] Milestone 2.1 — Fair supply and wall kicks
        - [ ] T-013 — Implement seven-bag piece supply
            Scope: src/domain/randomizer.ts, src/domain/game.ts, tests/unit. Depends on: T-012.
            Contract: E01 in SPEC. Outcome/evidence: Replace independent sampling with an injected seven-bag queue; verify complete bags, boundaries and deterministic sequence.
        - [ ] T-014 — Implement ordered SRS rotation candidates
            Scope: src/domain/pieces.ts, src/domain/board.ts, tests/unit. Depends on: T-013.
            Contract: E02 in SPEC. Outcome/evidence: Implement explicit I and JLSTZ kick tables, directed transitions and first-legal selection with expected fixtures for each transition.
        - [ ] T-015 — Review, test and report milestone 2.1
            Depends on: T-013, T-014. Review the complete milestone code and integrations separately from test execution; repair required findings and verify exits/regressions. Record actual checks, limits and eligible TODOs with options/ownership.
            Report: docs/dev/reports/phases/2/2.1.md. Publish evidence and close constituent issues before milestone closure.
    - [ ] Milestone 2.2 — Hold and landing tools
        - [ ] T-016 — Implement hold lifecycle and visible held identity
            Scope: src/domain/game.ts, src/ui/panel.ts, tests/unit, tests/browser. Depends on: T-015.
            Contract: E03 in SPEC. Outcome/evidence: Add once-per-piece hold, empty/swap queue semantics, spawn reset and collision game-over behavior; present held identity.
        - [ ] T-017 — Implement canonical landing and ghost projection
            Scope: src/domain/board.ts, src/ui/render.ts, tests/unit, tests/browser. Depends on: T-016.
            Contract: E04,G01 in SPEC. Outcome/evidence: Implement one shared ordinary landing query and ghost view; verify projected cells, including coincidence with the active piece, without an extra visibility suppression or state mutation. Apply the min projected y=10 boundary and straddling hide/show cases.
        - [ ] T-018 — Implement hard-drop command integration
            Scope: src/domain/game.ts, src/app/controller.ts, tests/unit, tests/browser. Depends on: T-017.
            Contract: E04 in SPEC. Outcome/evidence: Wire Space to canonical landing and selected default locking behavior without points; reject key-repeat triggers.
        - [ ] T-019 — Review, test and report milestone 2.2
            Depends on: T-016, T-017, T-018. Review the complete milestone code and integrations separately from test execution; repair required findings and verify exits/regressions. Record actual checks, limits and eligible TODOs with options/ownership.
            Report: docs/dev/reports/phases/2/2.2.md. Publish evidence and close constituent issues before milestone closure.
    - [ ] Milestone 2.3 — Grounded timing and integrated usability
        - [ ] T-020 — Implement grounded interval locking
            Scope: src/domain/game.ts, tests/unit. Depends on: T-019.
            Contract: E05 in SPEC. Outcome/evidence: Implement full-interval contact deadline, motion retention, airborne cancellation and chronological expiry; verify hard-drop and blur interactions.
        - [ ] T-021 — Verify and document integrated modern gameplay
            Scope: tests/browser, src/ui, README.md, RELEASE-NOTES.md. Depends on: T-020.
            Contract: E01–E05,G01 in SPEC. Outcome/evidence: Run modern-control/dynamic-ghost and classic regression scenarios in both browsers; inspect ghost/hold screenshots and document controls, policy and release inputs.
        - [ ] T-022 — Review, test and report milestone 2.3
            Depends on: T-020, T-021. Review the complete milestone code and integrations separately from test execution; repair required findings and verify exits/regressions. Record actual checks, limits and eligible TODOs with options/ownership.
            Report: docs/dev/reports/phases/2/2.3.md. Publish evidence and close constituent issues before milestone closure.
    - [ ] Milestone 2.4 — Phase review
        - [ ] T-023 — Review, test and report phase 2
            Depends on: delivery milestones 2.1, 2.2, 2.3 complete/closed, including their review tasks. Review cross-milestone code/invariants, run included SPEC exits and preserved regressions, repair blockers, and reconcile required reports and TODOs.
            Report: docs/dev/reports/phases/2/PHASE-REPORT.md. After verified phase closure, integrate/recheck/publish the default branch and publish release v0.2.0 under the separately authorized release workflow.

## Phase 3 — Penetrator ability

- [ ] Phase 3 — Penetrator ability
    - [ ] Milestone 3.1 — Safe penetrating placement
        - [ ] T-024 — Implement deepest legal penetrator landing
            Scope: src/domain/board.ts, tests/unit. Depends on: T-023.
            Contract: P01 in SPEC. Outcome/evidence: Enumerate legal current-or-lower placements independently of intervening blockers, including disjoint cavities and no-destination cases.
        - [ ] T-025 — Implement activation, transit and guarded settlement
            Scope: src/domain/game.ts, src/app/controller.ts, tests/unit. Depends on: T-024.
            Contract: P01,P02 in SPEC. Outcome/evidence: Apply activation and bonus spend, transit bounds, candidate rejection, disabled hold and timing/lock guard while preserving settled cells.
        - [ ] T-026 — Review, test and report milestone 3.1
            Depends on: T-024, T-025. Review the complete milestone code and integrations separately from test execution; repair required findings and verify exits/regressions. Record actual checks, limits and eligible TODOs with options/ownership.
            Report: docs/dev/reports/phases/3/3.1.md. Publish evidence and close constituent issues before milestone closure.
    - [ ] Milestone 3.2 — Rewards and visible ability state
        - [ ] T-027 — Implement bonus rewards and inventory lifecycle
            Scope: src/domain/game.ts, tests/unit. Depends on: T-026.
            Contract: P02 in SPEC. Outcome/evidence: Award one per four-line clear capped at three, reset on restart, and preserve ordinary spawn/held behavior.
        - [ ] T-028 — Integrate penetrator visuals and browser acceptance
            Scope: src/ui, tests/browser, README.md, RELEASE-NOTES.md. Depends on: T-027.
            Contract: P03,P01,P02 in SPEC. Outcome/evidence: Render entirely white active mode and projected outline, ordinary settled colors and 0–3 accessible glyph inventory; verify deepest ghost/drop agreement in both browsers.
        - [ ] T-029 — Review, test and report milestone 3.2
            Depends on: T-027, T-028. Review the complete milestone code and integrations separately from test execution; repair required findings and verify exits/regressions. Record actual checks, limits and eligible TODOs with options/ownership.
            Report: docs/dev/reports/phases/3/3.2.md. Publish evidence and close constituent issues before milestone closure.
    - [ ] Milestone 3.3 — Phase review
        - [ ] T-030 — Review, test and report phase 3
            Depends on: delivery milestones 3.1, 3.2 complete/closed, including their review tasks. Review cross-milestone code/invariants, run included SPEC exits and preserved regressions, repair blockers, and reconcile required reports and TODOs.
            Report: docs/dev/reports/phases/3/PHASE-REPORT.md. After verified phase closure, integrate/recheck/publish the default branch and publish release v0.3.0 under the separately authorized release workflow.

## Phase 4 — Session game configuration

- [ ] Phase 4 — Session game configuration
    - [ ] Milestone 4.1 — Validated settings and panel
        - [ ] T-031 — Define normalized settings and defaults
            Scope: src/settings/model.ts, tests/unit. Depends on: T-030.
            Contract: C01 in SPEC. Outcome/evidence: Define six allowlisted values and pure validators, reject invalid in-memory changes and expose defaults without storage effects.
        - [ ] T-032 — Integrate settings controls and next preview
            Scope: src/ui/panel.ts, src/app/controller.ts, tests/browser. Depends on: T-031.
            Contract: C01 in SPEC. Outcome/evidence: Use labeled keyboard-operable HTML controls, show queued piece without drawing supply, and prevent form keys from invoking gameplay.
        - [ ] T-033 — Review, test and report milestone 4.1
            Depends on: T-031, T-032. Review the complete milestone code and integrations separately from test execution; repair required findings and verify exits/regressions. Record actual checks, limits and eligible TODOs with options/ownership.
            Report: docs/dev/reports/phases/4/4.1.md. Publish evidence and close constituent issues before milestone closure.
    - [ ] Milestone 4.2 — Live policy transitions
        - [ ] T-034 — Implement live settings transition semantics
            Scope: src/app/controller.ts, src/domain/game.ts, src/ui/render.ts, tests/unit. Depends on: T-033.
            Contract: C02 in SPEC. Outcome/evidence: Apply toggle rejection, preserved hold, ghost policy and explicit hard-drop/general-lock transitions with same-value no-reset behavior.
        - [ ] T-035 — Verify session configuration and document controls
            Scope: tests/browser, README.md, RELEASE-NOTES.md. Depends on: T-034.
            Contract: C01,C02 in SPEC. Outcome/evidence: Check all options, including coincident ghost visibility, mid-fall/grounded changes, disabled shortcuts, restart retention and unpersisted model defaults before persistence adapters are composed in both browsers. Phase 5 supplies durable restore, and final regressions use its persisted expectations.
        - [ ] T-036 — Review, test and report milestone 4.2
            Depends on: T-034, T-035. Review the complete milestone code and integrations separately from test execution; repair required findings and verify exits/regressions. Record actual checks, limits and eligible TODOs with options/ownership.
            Report: docs/dev/reports/phases/4/4.2.md. Publish evidence and close constituent issues before milestone closure.
    - [ ] Milestone 4.3 — Phase review
        - [ ] T-037 — Review, test and report phase 4
            Depends on: delivery milestones 4.1, 4.2 complete/closed, including their review tasks. Review cross-milestone code/invariants, run included SPEC exits and preserved regressions, repair blockers, and reconcile required reports and TODOs.
            Report: docs/dev/reports/phases/4/PHASE-REPORT.md. After verified phase closure, integrate/recheck/publish the default branch and publish release v0.4.0 under the separately authorized release workflow.

## Phase 5 — Persistent configuration

- [ ] Phase 5 — Persistent configuration
    - [ ] Milestone 5.1 — Independent restore precedence
        - [ ] T-038 — Implement cookie and URL parsing and resolution
            Scope: src/settings/browser-config.ts, src/settings/model.ts, tests/unit. Depends on: T-037.
            Contract: S01 in SPEC. Outcome/evidence: Parse only allowlisted keys, strict values and duplicates; resolve each field independently and test invalid sources without mutating unrelated values.
        - [ ] T-039 — Integrate startup restore and explicit URL cookie writes
            Scope: src/main.ts, src/settings/browser-config.ts, tests/browser. Depends on: T-038.
            Contract: S01 in SPEC. Outcome/evidence: Load before game creation and persist valid explicit URL values, including defaults; omitted/invalid parameters retain existing saved values.
        - [ ] T-040 — Review, test and report milestone 5.1
            Depends on: T-038, T-039. Review the complete milestone code and integrations separately from test execution; repair required findings and verify exits/regressions. Record actual checks, limits and eligible TODOs with options/ownership.
            Report: docs/dev/reports/phases/5/5.1.md. Publish evidence and close constituent issues before milestone closure.
    - [ ] Milestone 5.2 — Synchronized selection and resilience
        - [ ] T-041 — Implement cookie/history writes and storage failure handling
            Scope: src/settings/browser-config.ts, src/app/controller.ts, tests/unit. Depends on: T-040.
            Contract: S02 in SPEC. Outcome/evidence: Write only selected settings with specified cookie attributes, replace URL parameter preserving fragment/other keys, attempt stores independently and expose non-blocking failure status.
        - [ ] T-042 — Verify reload precedence and persistent settings usability
            Scope: tests/browser, tests/unit, README.md, RELEASE-NOTES.md. Depends on: T-041.
            Contract: S01,S02 in SPEC. Outcome/evidence: Run six-field mixed-source, explicit-default, omitted/invalid, duplicate and blocked-storage scenarios in Chromium and Firefox; verify reload/new-page behavior and session-only board state.
        - [ ] T-043 — Review, test and report milestone 5.2
            Depends on: T-041, T-042. Review the complete milestone code and integrations separately from test execution; repair required findings and verify exits/regressions. Record actual checks, limits and eligible TODOs with options/ownership.
            Report: docs/dev/reports/phases/5/5.2.md. Publish evidence and close constituent issues before milestone closure.
    - [ ] Milestone 5.3 — Phase review
        - [ ] T-044 — Review, test and report phase 5
            Depends on: delivery milestones 5.1, 5.2 complete/closed, including their review tasks. Review cross-milestone code/invariants, run included SPEC exits and preserved regressions, repair blockers, and reconcile required reports and TODOs.
            Report: docs/dev/reports/phases/5/PHASE-REPORT.md. Also produce docs/dev/reports/IMPLEMENTATION-REPORT.md with the full-list outcome and aggregated unresolved/deferred TODOs when this completes the intended list. After verified phase closure, integrate/recheck/publish the default branch and publish release v0.5.0 under the separately authorized release workflow.
