# Delivery plan

## Strategy and dependencies

Deliver a usable classic game first, then bounded capabilities on its integrated baseline. [SPEC](SPEC.md) owns behavior; [DECOMPOSITION](DECOMPOSITION.md) owns components. Each phase preserves the prior playable path. A clean build, focused unit tests, actual application browser checks and user instructions grow with each increment. Mock-only layers cannot satisfy a phase exit.

| Phase | Capability / included contracts | Planned release | Prerequisite |
| --- | --- | --- | --- |
| 1 — Playable classic baseline | B01–B05, Q01 | v0.1.0 | None |
| 2 — Modern piece control | E01–E05, G01 | v0.2.0 | Phase 1 verified, integrated and published |

## Phase 1 — Playable classic baseline

Outcome: A complete keyboard-playable classic game; modern piece tools, penetration and settings are excluded.

### Milestone 1.1 — Deterministic placement foundation

Valid shapes, supply, spawn and command movement can be exercised without a browser.

Exit: verify included contracts, relevant prior regressions and integrated component behavior; complete milestone code review, repair blockers, run focused checks and retain `docs/dev/reports/phases/1/1.1.md`.

### Milestone 1.2 — Playable browser loop

B03,B04,B05 integrated as gravity, settlement and actual controls.

Exit: verify included contracts, relevant prior regressions and integrated component behavior; complete milestone code review, repair blockers, run focused checks and retain `docs/dev/reports/phases/1/1.2.md`. Demonstrate keyboard play, line clear and restart to inform whether the controls and rendering need amendment before distribution.

### Milestone 1.3 — Verified static distribution

A buildable static game with real-browser evidence and usable instructions.

Exit: verify included contracts, relevant prior regressions and integrated component behavior; complete milestone code review, repair blockers, run focused checks and retain `docs/dev/reports/phases/1/1.3.md`.

### Milestone 1.4 — Phase review

Exactly one phase code review/testing/report outcome follows completion and, when enabled, closure of all delivery milestones. Verify phase-specific exits, preserved behavior, reports and deferred TODOs in `docs/dev/reports/phases/1/PHASE-REPORT.md`. After phase verification, explicitly integrate into the default branch, recheck merged state and publish/read back before tagging v0.1.0 and publishing its GitHub release. Finalize version/release notes against the actual delivered source. No subsequent phase starts before this boundary.

## Phase 2 — Modern piece control

Outcome: Preserve the classic game while adding fair supply, forgiving rotation, piece tools and full-interval locking; penetration/settings are excluded.

### Milestone 2.1 — Fair supply and wall kicks

Seeded bags and SRS preserve valid board placement.

Exit: verify included contracts, relevant prior regressions and integrated component behavior; complete milestone code review, repair blockers, run focused checks and retain `docs/dev/reports/phases/2/2.1.md`.

### Milestone 2.2 — Hold and landing tools

Hold, ghost and hard drop share the active lifecycle and canonical landing. Dynamic ghost visibility is included in the existing projection seam.

Exit: verify included contracts, relevant prior regressions and integrated component behavior; complete milestone code review, repair blockers, run focused checks and retain `docs/dev/reports/phases/2/2.2.md`.

### Milestone 2.3 — Grounded timing and integrated usability

All modern controls operate consistently under full-interval locking.

Exit: verify included contracts, relevant prior regressions and integrated component behavior; complete milestone code review, repair blockers, run focused checks and retain `docs/dev/reports/phases/2/2.3.md`. Demonstrate the changed controls and state transitions; use failures or unclear feedback to inform continue/amend/simplify/stop decisions within the authorized range.

### Milestone 2.4 — Phase review

Exactly one phase code review/testing/report outcome follows completion and, when enabled, closure of all delivery milestones. Verify phase-specific exits, preserved behavior, reports and deferred TODOs in `docs/dev/reports/phases/2/PHASE-REPORT.md`. When this completes the full intended task list, also aggregate unresolved/deferred TODOs with provenance and options in `docs/dev/reports/IMPLEMENTATION-REPORT.md`. After phase verification, explicitly integrate into the default branch, recheck merged state and publish/read back before tagging v0.2.0 and publishing its GitHub release. Finalize version/release notes against the actual delivered source. No subsequent phase starts before this boundary.

## Scope and count rationale

Phase 1 has three delivery milestones: pure placement, integrated playable loop and verified distribution. The last is narrow (browser acceptance, packaging and instructions) because it provides independent reproducibility evidence for release.

Modern gameplay has three delivery milestones: fair supply/rotation, piece tools and grounded timing. Conditional visibility belongs to the existing ghost outcome, avoiding a tiny independent phase.

Dedicated phase review milestones and report-only tasks are excluded from delivery counts. A complete task list is derived in [TASKS](TASKS.md) after physical ownership is established in [layout](layout.md).

## Verification, risks and release boundaries

Require isolated Chromium and Playwright-managed Firefox evidence through the central [browser policy](../../BROWSER_DEV_POLICY.md), deterministic engine checks, TypeScript/build gates and static distribution verification. Browser provisioning is an early risk gate; missing required capability blocks dependent acceptance rather than silently shrinking coverage. Check screenshots for Canvas, not just DOM text. No browser execution is claimed during planning.

Every delivery milestone ends with explicit code review/testing/report work. Required defects and contract violations are repaired before closure; only eligible non-critical code TODOs may be deferred with impact, rationale, options and ownership. Final phase review depends on all delivery milestone closures and contains one task; it does not depend on its own milestone closing first.

A phase's release uses finalized root `RELEASE-NOTES.md`, version metadata and a tag on verified default-branch source. Publish after phase integration, not after documentation authoring. Implementation scope and phase activation remain separately authorized operations.
