# Doc-design modes and pass control

Use for main document preparation mode selection, the DOCS-008 boundary, cursor reset and multipass recovery. [Main preparation](main-preparation.md) retains task/QC/publication ownership; [human review](human-document-review.md) retains presentation and decision evidence. A cursor reset changes workflow progress, not Git history or file contents.

## Select and retain the mode

The ordinary default is **interactive/onepass**. Document approval and pass control are separate choices:

| Selection | Human approval | End of DOCS-008 |
| --- | --- | --- |
| interactive/onepass | Each necessary document checkpoint unless explicitly preapproved | Follow the selected main-preparation range and existing final-QC gates |
| autodoc/onepass | PROJECT remains active; ARCHITECTURE through TASKS are preapproved | Stop before DOCS-009 |
| autodoc with human-controlled multipass | PROJECT remains active each pass; subsequent document checkpoints are preapproved | Stop for reset or advance direction |
| autodoc with autoloop | First PROJECT approval remains active; later PROJECT approvals are waived | Reset for the next predefined scope; stop after the last pass, before DOCS-009 |

When autodoc includes an explicitly predefined sequence of later scope revisions, use autoloop unless the human requests human-controlled multipass. Do not infer future scopes or select multipass for an ordinary onepass request. At entry, state the actual selection, pass scope and stop. In autoloop, **explicitly announce that later PROJECT approvals are waived** before the first brief approval. Retain explicit human overrides and later steering.

Record mode, current pass/cursor, scope sequence and actual approval/delegation basis in DOCS_PREPARATION under [record ownership](main-preparation.md#preparation-record-and-adoption); DOCS_TASKS holds only tasks/checkoffs. Carry them into each document-owner handoff so delegated decisions and preapproval are not replaced by generic interactive defaults. HANDOFF snapshots link that owner; no second registry is needed. Selection supplies only its scoped checkpoint preapproval. Initialization continuation, technical QC, Git publication, tracking and implementation authority keep their existing gates.

## Prepare scope and decisions

Use sdd-design's [exploration](../../sdd-design/references/exploration.md) during brief preparation and revision. Proactively identify and resolve important interactions and boundary cases, surfacing decisions that materially affect current application scope before PROJECT approval. Keep the brief at principal-scope depth rather than drafting a detailed SPEC early.

For human-controlled passes, obtain the current scope/revision and resolve its important choices with the human before brief approval. For predefined autoloop, clarify the initial scope and important interactions across all supplied later-pass scopes upfront; do not draft all later document sets. Each PROJECT describes the complete current-pass scope; retain future changes in the DOCS_PREPARATION scope sequence until their turn rather than folding them into the first brief. Apply the [development-document content boundary](human-document-review.md#development-document-content-boundary) to every authored root/child: express the intended project state without narrating the pass sequence. The first PROJECT approval authorizes the agreed sequence and resets, with later document checkpoints preapproved as stated above.

In autoloop, newly discovered material decisions outside the initial agreement are delegated to the agent. Use best judgment from available project/conversation context and general domain knowledge, distinguish assumptions from verified facts, and record consequential decisions in the owning documents. Give timely, concise commentary identifying the issue, relevant assumptions, key tradeoffs, chosen action and scope consequences so the human can steer. Proceed without an acknowledgment or extra approval pause. Actual execution failures and missing required facilities retain their gates; do not turn an eligible delegated decision into a blocker.

## Complete a pass

One full pass spans **DOCS-002 through DOCS-008** in dependency order. Revise retained documents against the current pass scope and recheck affected dependents. Reuse unchanged acceptable content without artificial edits, but record fresh pass acceptance/preapproval and relevant QC; prior-pass approval alone does not complete a reset task.

Complete each document with its approved state, current-pass decision/QC references in DOCS_PREPARATION and checked DOCS task together, then publish/read back and close/read back its existing issue when tracking is enabled. A preapproved document needs no extra proposal/approval round trip. Earlier user-requested stops and resets remain controlling.

After DOCS-008 and its required publication/issue closure, autodoc stops or performs the next authorized autoloop reset. At an autodoc stop, include DOCS_PREPARATION pass evidence and refresh HANDOFF in the DOCS-008 completion commit with the pass result and pending reset/advance boundary; confirm subsequent hosted effects by readback. Keep DOCS-009 unchecked and its issue and documentation milestone open. Do not call the package complete, run whole-package QC, merge documentation or activate implementation. Per-document QC remains required. Human-controlled multipass waits for reset/scope or advance direction; autoloop proceeds through only the predefined remaining scopes, then stops. Incorporating those revisions means updating the document set, not Git integration.

An explicit advance selects the existing [package-QC stage](main-preparation.md#final-package-qc-integration-and-checkpoint) within its actual scope. It does not select implementation or a new pass. Do not waive the separate final package/integration gates because a loop completed.

## Reset the cursor

A human may request reset at any intermediate checkpoint in active doc-design. Autoloop also authorizes reset after DOCS-008 when a predefined pass remains. This is an explicit exception to ordinary first-approval tasks staying complete during later edits.

1. Reconcile the current checkpoint, pending publication/hosted effects, mode and next scope. Preserve unrelated or incomplete work; do not use git reset, delete documents or allocate another preparation branch. Retain all existing development documents as version N−1 inputs for revision into version N. Git stores those versions; no copied file set or filename suffix is required.
2. In one reset commit, record the prior pass/checkpoint, reason/scope change, next pass/scope and approval basis in DOCS_PREPARATION; set the cursor to DOCS-002 and uncheck **DOCS-002 through DOCS-009** in DOCS_TASKS. Keep DOCS-001 complete, preserve existing PROJECT/design/SPEC/PLAN/layout/TASKS content and retain task IDs. Refresh HANDOFF with this reset boundary and outstanding hosted operations. Existing QC/approval evidence remains historical and does not certify the new pass.
3. Publish/read back the reset commit. If tracking is enabled, have sdd-forge [reopen the same eight issues](../../sdd-forge/references/github-docs-preparation.md#reset-a-document-design-pass), verify identity/association and open states, and resolve contradictory milestone state. Do not resume document work while required reopening is pending or unknown. Tracking-disabled resets use the same local commit/cursor without hosted writes.
4. Resume PROJECT using the retained brief and new scope. Apply the selected mode's current-pass approval policy, then revise dependents through DOCS-008. Reset grants no implementation range or unrelated scope.

## Resume or steer

Recover DOCS_PREPARATION control/evidence, DOCS_TASKS checkboxes, document/Git and hosted states before acting. A published reset with partial issue reopening needs reconciliation of those same issues, not another reset commit or pass increment. Reuse already verified effects and complete only outstanding operations. A completed pass awaiting reset/advance remains at that boundary; file presence or closed prior-pass issues do not advance it.

Retain human changes to scope, pass order or mode in DOCS_PREPARATION before dependent work. Switching to human-controlled multipass restores its PROJECT and end-of-pass checkpoints for subsequent work; do not retroactively invent approvals. Reuse existing owning records and normal continuity checkpoints rather than per-action HANDOFF updates.
