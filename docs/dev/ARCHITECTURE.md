# Architecture

## Context and major blocks

The [project brief](PROJECT.md) defines a static, single-player browser game. Three blocks keep game rules testable without browser state:

| Block | Responsibility | Dependency direction |
| --- | --- | --- |
| Domain engine | Own board, active piece, score, random source and lifecycle; apply commands and elapsed game time | Pure TypeScript; depends only on explicit inputs |
| Application controller | Translate keyboard/button input and animation time into engine calls; own browser listener and frame lifecycle | Calls domain and presentation; domain never calls back into browser |
| Presentation | Draw the board and active piece on Canvas; show semantic status and controls in HTML | Consumes snapshots; submits intents to controller |

The controller serializes each input/time transition, then publishes a complete snapshot to the renderer. Rendering cannot mutate the board. A single engine state transition owns lock, line removal, score and subsequent spawn so observers cannot see partially settled state.

## Ownership and verification boundaries

Board coordinates and shape geometry belong to domain functions. A seeded/random-number input and explicit elapsed time allow reproducible state-machine tests. Browser clocks, events and DOM references stay in adapters. Read-only snapshots avoid hidden shared writable state across layers. One controller owns requestAnimationFrame and listeners; dispose/restart cannot create parallel loops.

Use ordinary functions and a small state machine, with constructor/factory injection for randomness and time. A framework or event bus would add indirection without a second consumer. Canvas suits the board grid; HTML retains keyboard-operable controls and text status. The tradeoff is that Canvas cells need an accessible textual status beside them.

## Piece services and timing

Domain geometry supplies rotation candidates and a single landing query used by hard drop and ghost. The randomizer owns the seven-bag sequence; hold owns one stored piece identity and per-piece eligibility. The engine owns the grounded timer and resolves gravity, commands and deadlines in one chronological stream. Presentation reads ghost/hold views rather than independently simulating them.

Ghost visibility is a presentation projection over the domain landing result. Hiding the ghost never changes movement, locking or the landing query.

## Penetrator policy

An active-piece mode selects ordinary or penetrator traversal within the same geometry/landing boundary. Both modes share board storage and the atomic lock guard. Traversal permission never grants permission to overwrite settled cells. The engine owns bonus inventory and activation consumption; view code owns only the corresponding symbols and white active-piece style. Settled cells keep their piece identity palette after lock.

## Configuration boundary

A typed settings model supplies validated values and defaults. The controller owns the current settings snapshot; it applies feature flags to commands, supplies rule-policy changes to the engine, and gives visibility preferences to presentation. Disabled controls do not clear held pieces, queues or bonuses. Native HTML form focus is isolated from gameplay input handling.

A browser configuration adapter reads cookies and URLSearchParams into the settings model, resolves each field independently, and writes selected values through cookie and history APIs. Domain code has no cookie, URL or storage dependency. Browser storage errors leave in-memory play available and expose a non-blocking status; failed persistence cannot roll back an already selected setting. Only six allowlisted keys are parsed or written; query input is never HTML.

## Component route

[DECOMPOSITION](DECOMPOSITION.md) owns logical interfaces and collaboration; [SPEC](SPEC.md) owns observable contracts. Browser provisioning and isolation remain governed by [the central policy](../../BROWSER_DEV_POLICY.md).
