# Main documentation preparation record

## Current control

- Mode: autodoc/autoloop, requested by the human on 2026-10-24.
- Current pass: 3; current document DOCS-002; next DOCS-003.
- Authority: prepare six cumulative document passes, publish every owned commit, maintain policy-selected GitHub tracking. No implementation is authorized.
- Approval: the human approved the initial interaction and technology recommendations on 2026-10-24. The human subsequently approved the published Pass 1 PROJECT proposal on 2026-10-24; later PROJECT and subsequent document checkpoints are preapproved by the selected mode. New material autoloop decisions are delegated with visible rationale.
- Final stop: after Pass 6 DOCS-008, before DOCS-009 package QC, documentation integration or implementation.
- Reporting: Standard.

## Scope sequence

1. **Playable classic baseline.** Minimal classic baseline: keyboard-controlled 10×20 board, seven tetrominoes, movement, rotation, soft drop, fixed gravity, line clearing, line-based scoring, game over and restart. Exclude later enhancements from current product documents.
2. **Gameplay enhancements.** Add hold, ghost, 7-bag randomization, wall kicks, hard drop and one full gravity interval of grounded lock delay, including hard drop.
3. **Conditional ghost visibility.** Hide the whole ghost when any projected cell lies above the board midline; show only when all cells are in its lower half.
4. **Penetrator mode.** Add a hotkey-activated penetrator: spend one available bonus, pass through settled cells without destroying them, remain white until locking, and lock only fully inside the board without overlap. Regular pieces are never white. Hard drop and ghost share the lowest valid destination beyond blockers. Award one bonus per four-line clear, cap inventory at three, and show one side-panel symbol per available bonus.
5. **Session-only configuration.** Add session-only controls and next preview: ghost hidden/dynamic/always shown; hard drop on/off; preview on/off; hard-drop lock follow-general/immediate; general lock failed-downward-attempt/full-gravity-interval; hold on/off. Defaults: dynamic ghost, hard drop/preview/hold on, interval lock, hard drop follows general lock. No settings survive reload.
6. **Configuration persistence.** Persist each setting independently: valid explicit URL value, otherwise valid cookie, otherwise default. Save explicit valid URL values to cookies even when equal to defaults. Omitted parameters retain cookies. UI changes save the selected cookie and update its URL parameter, preserving unrelated parameters.

## Accepted exploration decisions

The human's approval covers the proposed rules and TypeScript, pure engine, Canvas board and ordinary HTML controls. Precise contracts are adopted only when their scope enters a product document.

- Grounded movement/rotation does not reset lock time. Becoming airborne cancels it; re-grounding starts a full interval. Repeated hard drop while grounded does not restart time.
- Activated penetrators cannot be held; repeated activation does nothing. Activation spends a bonus immediately. If no fully in-bounds, non-overlapping landing exists, end the game without overwriting settled cells.
- Visibility and feature toggles apply immediately. Switching general locking policy starts a fresh interval for a grounded piece or waits for the next failed downward attempt, respectively.
- Invalid configuration values fall through independently to the next source. Explicit valid URL values, including defaults, are saved; omission never erases saved preference.
- First playable release v0.1.0; choose later semantic versions from actual delivered changes. Once implementation is authorized, publish a tagged GitHub release after each verified and integrated implementation phase. Document passes are not releases.

## Decisions and document evidence

| Task | Current evidence / decision basis |
| --- | --- |
| DOCS-001 | All four original root files preserved byte for byte; default provenance seed and main merge verified. Initialization 8ca36e912d2f58b64a7f0969e71e02e774e6b5e2 published with exact ref readback; issue #1 closed/read back as completed. |
| DOCS-002 | Pass 3; PROJECT.md blob `3aab11a2ae343e512326ce054a8a61c328b03b29`; preapproved by requested autodoc/autoloop and accepted scope sequence. Scope/content and design consistency reviewed; no unresolved material decision. |
| DOCS-003 | Scope 3 pending; prior-scope evidence retained in Git at bd7793aa7a3207c6a47242404f2c43163bb7194f. |
| DOCS-004 | Scope 3 pending; prior-scope evidence retained in Git at bd7793aa7a3207c6a47242404f2c43163bb7194f. |
| DOCS-005 | Scope 3 pending; prior-scope evidence retained in Git at bd7793aa7a3207c6a47242404f2c43163bb7194f. |
| DOCS-006 | Scope 3 pending; prior-scope evidence retained in Git at bd7793aa7a3207c6a47242404f2c43163bb7194f. |
| DOCS-007 | Scope 3 pending; prior-scope evidence retained in Git at bd7793aa7a3207c6a47242404f2c43163bb7194f. |
| DOCS-008 | Scope 3 pending; prior-scope evidence retained in Git at bd7793aa7a3207c6a47242404f2c43163bb7194f. |
| DOCS-009 | Not selected; remains open at the autoloop stop. |

## Initialization and current reset

- Original retained files: AI_DISCLOSURE.md, SDD-MANAGER.md, AGENTS.md and SKILL_DISCOVERY_PROTOCOL.md. Copied root files: none. All four were present, so no mixed-initialization pause applies.
- Preservation: all four worktree blobs match initial commit 909a7789bd9292ab53c50d5cb57a47b343577c07.
- Discovery: bundled SDD Manager 0.15.2 and standalone Technical Writing Assistant; root browser policy requires isolated Chromium and Firefox. Linux host; Git, Node and Python available; gh absent.
- Tracking: enabled by root AGENTS.md. Native sdd-docs-main milestone and all nine exact standard issue definitions and associations read back before target writes; DOCS-001–009 map to issues #1–9. Complete enumeration covered open and closed objects.
- Manual provenance: default enabled; two exact packaged scaffold files, no transcript. Base 909a7789bd9292ab53c50d5cb57a47b343577c07; published seed 7a78377e8ae3f522309b3080bd60341450f71b2c; published explicit two-parent main merge 44a20193b5ec94090d041d20649057f2958b4e46. Retain design-docs/ai-logs for manual logs.
- Credential handling: ignored, untracked conventional repository credential established after full projection readback. No credential contents enter project evidence.
- Current reset: from scope 2 at bd7793aa7a3207c6a47242404f2c43163bb7194f to scope 3; authorized by the accepted predefined sequence. Retained product files are revision inputs; DOCS-002–009 reopened locally.

## Pending transitions

DOCS-002 completion publication and issue #2 closure require confirmation. Recover actual subsequent effects by exact readback before replay. No implementation is authorized.
