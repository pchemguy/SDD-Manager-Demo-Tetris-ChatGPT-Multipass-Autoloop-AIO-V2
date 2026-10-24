# Main documentation preparation record

## Current control

- Mode: autodoc/autoloop, requested by the human on 2026-10-24.
- Current pass: 6 complete; DOCS-009 whole-package QC passed under the human "complete QC" advance on 2026-10-24.
- Authority: the six cumulative passes are complete. The human advanced to whole-package QC, bounded repairs and standard published documentation integration/milestone closure. No implementation is authorized.
- Approval: the human approved the initial interaction and technology recommendations on 2026-10-24. The human subsequently approved the published Pass 1 PROJECT proposal on 2026-10-24; later PROJECT and subsequent document checkpoints are preapproved by the selected mode. New material autoloop decisions are delegated with visible rationale.
- Current stopping boundary: complete package QC and the standard verified documentation integration/milestone closure; stop before implementation. The human advanced beyond the prior autodoc stop on 2026-10-24.
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
| DOCS-002 | Accepted scope 6 retained; current PROJECT.md blob `c61b6c337c589333ba61da8af62a5826d75046b2`. Bounded package-QC clarification under the human advance; affected adjacent reports rechecked. Existing first-approval checkoffs remain complete. |
| DOCS-003 | Pass 6; ARCHITECTURE.md blob `0d2b0d91d0a452732847310adf73041d048d8576`; preapproved by requested autodoc/autoloop and accepted scope sequence. Scope/content and design consistency reviewed; no unresolved material decision. |
| DOCS-004 | Pass 6; DECOMPOSITION.md blob `de9546942983309d3721df642c516e269d5b53a9`; preapproved by requested autodoc/autoloop and accepted scope sequence. Scope/content and design consistency reviewed; no unresolved material decision. |
| DOCS-005 | Accepted scope 6 retained; current SPEC.md blob `8ca988bba193b82e339cac98496d8f43b9495cbe`. Bounded package-QC clarification under the human advance; affected adjacent reports rechecked. Existing first-approval checkoffs remain complete. |
| DOCS-006 | Accepted scope 6 retained; current PLAN.md blob `b224335a45ed88a8e539c25a38297d589805eb2b`. Bounded package-QC clarification under the human advance; affected adjacent reports rechecked. Existing first-approval checkoffs remain complete. |
| DOCS-007 | Accepted scope 6 retained; current layout.md blob `4f1ab04040084dbedcc8407526f7e60887b39c3a`. Bounded package-QC clarification under the human advance; affected adjacent reports rechecked. Existing first-approval checkoffs remain complete. |
| DOCS-008 | Accepted scope 6 retained; current TASKS.md blob `b71d0b2c45f5ee42cc16b6f2b21400f348d8b4de`. Bounded package-QC clarification under the human advance; affected adjacent reports rechecked. Existing first-approval checkoffs remain complete. |
| DOCS-009 | Whole-package QC passed; [DOCS-QC-REPORT](DOCS-QC-REPORT.md) pins repaired root/report identities and resolves QC-001–004. Report, updated evidence, HANDOFF and checked DOCS-009 are co-committed. Publication, issue closure and integration require subsequent readback. |

## Initialization and current reset

- Original retained files: AI_DISCLOSURE.md, SDD-MANAGER.md, AGENTS.md and SKILL_DISCOVERY_PROTOCOL.md. Copied root files: none. All four were present, so no mixed-initialization pause applies.
- Preservation: at DOCS-001 all four root blobs matched initial commit 909a7789bd9292ab53c50d5cb57a47b343577c07. AGENTS project navigation was subsequently maintained at the layout checkpoints.
- Discovery: bundled SDD Manager 0.15.2 and standalone Technical Writing Assistant; root browser policy requires isolated Chromium and Firefox. Linux host; Git, Node and Python available; gh absent.
- Tracking: enabled by root AGENTS.md. Native sdd-docs-main milestone and all nine exact standard issue definitions and associations read back before target writes; DOCS-001–009 map to issues #1–9. Complete enumeration covered open and closed objects.
- Manual provenance: default enabled; two exact packaged scaffold files, no transcript. Base 909a7789bd9292ab53c50d5cb57a47b343577c07; published seed 7a78377e8ae3f522309b3080bd60341450f71b2c; published explicit two-parent main merge 44a20193b5ec94090d041d20649057f2958b4e46. Retain design-docs/ai-logs for manual logs.
- Credential handling: ignored, untracked conventional repository credential established after full projection readback. No credential contents enter project evidence.
- Current reset: from scope 5 at 7f5f8be7fd899e036930aeb078ec948722c14d62 to scope 6; authorized by the accepted predefined sequence. Retained product files are revision inputs; DOCS-002–009 reopened locally.

## Pending transitions

Publish/read back the DOCS-009 completion and close/read back issue #9; then explicitly merge the complete accepted preparation into actual default main, verify/publish/read back, and close/read back sdd-docs-main. These are pending as of this checkpoint. Stop before implementation; no phase projection or release is selected.
