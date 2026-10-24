# Component decomposition

[ARCHITECTURE](ARCHITECTURE.md) establishes domain, controller and presentation blocks. Components below own cohesive decisions; these are logical interfaces, not mandatory classes.

| ID | Component | Responsibility and state | Provided/required boundary | Verification seam |
| --- | --- | --- | --- | --- |
| C-BOARD | Board and geometry | Own settled cells and immutable tetromino masks; validate bounds/collision, rotate and compact rows. | Placement/clear queries; no DOM or clocks. | Table-driven geometry and compaction fixtures. |
| C-ENGINE | Game state machine | Own active piece, score, lifecycle and lock/spawn transaction. | createGame, dispatch, advance and snapshot; inject random input. | Deterministic command/time sequences. |
| C-INPUT | Input and clock controller | Own listeners and frame time; order intents and prevent browser defaults only for game controls. | Domain commands and elapsed monotonic game time. | Fake clock plus real browser keyboard/focus checks. |
| C-VIEW | Canvas and HTML view | Own drawing and semantic status; consume state without mutation. | render(snapshot); restart intent. | Screenshots and status assertions in target browsers. |

## Collaboration and lifecycle

The application creates one engine and one controller. C-INPUT converts events into commands, advances the engine with active elapsed time, and asks C-VIEW to draw the resulting snapshot. C-ENGINE calls C-BOARD for legal geometry and owns all lifecycle transitions. C-VIEW may emit UI intents but cannot change domain state. A terminal game rejects gameplay commands; restart creates a clean game through the same application owner. Disposal cancels the owned frame and listeners.

No component reads a browser clock implicitly. Randomness is supplied explicitly and snapshots are read-only. Invalid external intents are rejected before state mutation; development fixtures cannot become production query parameters or test backdoors.

## Contract owner

[SPEC](SPEC.md) defines command outcomes, geometry, timing, invalid-input handling and objective acceptance. There are no additional component children: current responsibilities fit this entry without duplicating contracts.
