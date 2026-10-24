# Delivery plan

## Strategy and dependencies

Deliver a usable classic game first, then bounded capabilities on its integrated baseline. [SPEC](SPEC.md) owns behavior; [DECOMPOSITION](DECOMPOSITION.md) owns components. Each phase preserves the prior playable path. A clean build, focused unit tests, actual application browser checks and user instructions grow with each increment. Mock-only layers cannot satisfy a phase exit.

| Phase | Capability / included contracts | Planned release | Prerequisite |
| --- | --- | --- | --- |
| 1 — Playable classic baseline | B01–B05, Q01 | v0.1.0 | None |

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

Exactly one phase code review/testing/report outcome follows completion and, when enabled, closure of all delivery milestones. Verify phase-specific exits, preserved behavior, reports and deferred TODOs in `docs/dev/reports/phases/1/PHASE-REPORT.md`. When this completes the full intended task list, also aggregate unresolved/deferred TODOs with provenance and options in `docs/dev/reports/IMPLEMENTATION-REPORT.md`. After phase verification, explicitly integrate into the default branch, recheck merged state and publish/read back before tagging v0.1.0 and publishing its GitHub release. Finalize version/release notes against the actual delivered source. No subsequent phase starts before this boundary.

## Scope and count rationale

Phase 1 has three delivery milestones: pure placement, integrated playable loop and verified distribution. The last is narrow (browser acceptance, packaging and instructions) because it provides independent reproducibility evidence for release.

Dedicated phase review milestones and report-only tasks are excluded from delivery counts. A complete task list is derived in [TASKS](TASKS.md) after physical ownership is established in [layout](layout.md).

## Verification, risks and release boundaries

Require isolated Chromium and Playwright-managed Firefox evidence through the central [browser policy](../../BROWSER_DEV_POLICY.md), deterministic engine checks, TypeScript/build gates and static distribution verification. Browser provisioning is an early risk gate; missing required capability blocks dependent acceptance rather than silently shrinking coverage. Check screenshots for Canvas, not just DOM text. No browser execution is claimed during planning.

Every delivery milestone ends with explicit code review/testing/report work. Required defects and contract violations are repaired before closure; only eligible non-critical code TODOs may be deferred with impact, rationale, options and ownership. Final phase review depends on all delivery milestone closures and contains one task; it does not depend on its own milestone closing first.

A phase's release uses finalized root `RELEASE-NOTES.md`, version metadata and a tag on verified default-branch source. Publish after phase integration, not after documentation authoring. Implementation scope and phase activation remain separately authorized operations.
