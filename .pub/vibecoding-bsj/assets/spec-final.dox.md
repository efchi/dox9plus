# Bullshit Jobs — Isometric Corporate Simulation PoC

Specification in [Dox](https://github.com/efchi/dox9plus) notation. Hobby project, vibecoded PoC, built to demonstrate the use of the *dox-assistant* skill in a dedicated article.

## 1. Goals and Context

> **[G 1]** Build a working PoC of an isometric browser-game within a limited timeframe, sufficient to produce a demonstrative article about Dox Assistant.

> **[BR 1]** This is a hobby project: no expectation of production-grade quality or scalability.

> **[BR 2 .Must]** The project must demonstrate practical use of the dox-assistant skill, from specification to implementation.

> **[D 1]** The code will be generated via vibecoding starting from this Dox specification, not hand-written.

> **[D 2]** The game is single-player: a single user observes/interacts with multiple autonomous characters on the map, in a simulation style (akin to *The Sims*).

> **[D 3]** The PoC uses a single fixed map (no multi-level/multi-area support).

> **[BR 3]** English is the reference language for both this specification and the game's UI text.

## 2. Setting and Narrative

> **[D 4]** Setting: a corporate management simulation inspired by David Graeber's *Bullshit Jobs*. The user plays as the CEO; the "little guys" are employees, split into 5 classes.

> **[D 5]** The characters are anonymous, generic units, with no individual names or narrative personalities.

> **[G 2]** Gameplay goal: keep the company running for as long as possible.

> **[O 1] 🟢** Shared leaderboard of survival times across players.

> **[D 6]** For this PoC: local score/record only, no shared backend/persistence. The shared leaderboard (**[O 1]**) remains an option to be validated in the future.

## 3. Game Mechanics

### 3.1 Lifecycle and Game Over

> **[FR 1]** The game ends when all characters have left (empty map).

> **[FR 2]** Each character has an energy/happiness stat, on a 0–100 scale (**[TR 11]**). Below a threshold, the character enters burnout (sprite turns red, berserk-style); after a prolonged period in burnout, the character disappears from the map (fade out).

> **[A 1] 🟡** Burnout threshold: happiness < 20. Value is illustrative, to be balanced via playtesting.

> **[A 3] 🟡** Burnout duration before disappearance varies per class, instead of a single global value (illustrative, to be balanced via playtesting):

| Class | Ticks in burnout before leaving |
|---|---|
| Flunkies | 18 |
| Goons | 10 |
| Duct Tapers | 20 |
| Box Tickers | 12 |
| Task Masters | 8 |

> **[D 7]** Happiness has a baseline decay over time (constant entropy at the start of a run), independent of neighbor effects — this ensures constant pressure on the player even in the absence of negative interactions.

> **[D 14]** The baseline decay (**[D 7]**) is not actually constant across a whole run: it ramps up gradually as the run progresses, up to a cap, so pressure on the player increases over time instead of staying flat.

> **[TR 23]** Decay increases linearly with elapsed simulation ticks (base rate + a small per-tick increment), capped at a maximum rate.

### 3.2 Hiring and Firing

> **[FR 3]** The CEO can hire new characters by spending currency (BSJ), and can fire existing characters, also at a currency cost.

> **[A 2] 🟡** Hiring costs more than firing (full cost vs. a small exit penalty, not free). Exact values to be balanced via playtesting.

> **[FR 16]** When hiring, the player chooses the target cell for the new employee by clicking an empty tile (placement mode), instead of automatic random placement.

> **[TR 22]** While in placement mode, empty cells are visually highlighted as valid targets; clicking an occupied cell (or anywhere else that isn't a valid empty tile) cancels placement — and, if a character sits on that cell, selects it instead.

> **[FR 4]** The game starts with a team already present on the map: larger in size and skewed toward low-impact roles (e.g. many Flunkies, few Task Masters).

### 3.3 Classes and Interactions

> **[D 8]** Interaction between adjacent characters is governed by a fixed relation matrix per class pair, which acts **exclusively on neighbors' happiness** (not directly on currency). Each character has individual stats that vary with some randomness around a class-defined baseline distribution.

> **[D 9]** Each class has its own base individual economic value; the actual currency output is modulated by the character's happiness: `output = class_base_value × happiness / 100`. This is the only channel linking the social mechanic (happiness) to the economic one (CEO's currency) — low happiness reduces productivity, not just burnout risk.

> **[TR 14]** Adjacency rule for character interaction: 4 neighbors (N/S/E/W), no diagonals.

> **[FR 17]** Selecting a character reveals its adjacency effects: a visual link is drawn to each neighbor, color-coded and weighted by the sign and magnitude of the happiness effect that neighbor exerts (per **[D 8]**).

> **[D 10]** Confirmed characterization of the 5 classes:

| Class | Base individual value (currency) | Effect on neighbors (happiness) |
|---|---|---|
| Flunkies | Low | Strongly raises |
| Goons | High (generates) | Lowers |
| Duct Tapers | — | Stabilizes (reduces variance), mild positive |
| Box Tickers | High upkeep cost (consumes) | Neutral |
| Task Masters | Positive (generates) | Strongly lowers |

> **[FR 5]** For each simulation tick, the system: (a) applies the baseline happiness decay (**[D 7]**); (b) applies the adjacency matrix effects to neighbors' happiness (**[D 8]**); (c) computes each character's currency output, modulated by happiness (**[D 9]**), and adds/subtracts it to/from the CEO's currency.

> **[D 11]** Needs/stats beyond happiness will be few and simple; the concrete list will be defined at a later stage.

> **[D 12]** Character sprites are visually distinct per class (a unique silhouette/shape per class), not merely a recolor of a shared base sprite — narrows **[Opn 4]**. Task Master's base color was additionally moved away from red, to avoid it reading the same as the (also red) burnout tint (**[TR 24]**).

> **[TR 21]** Character sprites are pre-rendered once per class on a small native-resolution off-screen canvas and scaled up with nearest-neighbor (pixelated) sampling. This guarantees a uniform, genuinely blocky pixel-art rendering technique across all classes — every instance of a given class shares an identical sprite bitmap — while the underlying drawing still differs per class (silhouette + accessory, **[D 12]**).

> **[TR 24]** The in-burnout state is emphasized for legibility: the color tint pushes further toward a saturated danger red than earlier revisions, and the exclamation-mark indicator (**[FR 2]**) is enlarged, outlined, and given a background badge for contrast.

> **[Opn 1] 🔵** Define the concrete list of needs/stats beyond happiness, and how they influence autonomous behavior.

> **[FR 6 .Must]** Characters' needs decay over time (happiness included, **[D 7]**); characters act in full autonomy to satisfy them, with no direct user intervention required on movement.

> **[FR 7]** Characters move autonomously on the isometric map, guided by their needs/states, with no need for direct user commands for each individual movement.

> **[Opn 2] 🔵** Define movement logic in detail (pathfinding, destinations, priority among needs).

### 3.4 CEO Actions

> **[FR 8]** Through the action buttons on the selected character, the user does not control it directly but triggers actions that affect the world/simulation (e.g. hiring, firing, other managerial decisions).

> **[FR 18]** The CEO can trigger a "Pep Talk" action on the selected character, at a currency cost, giving an instant happiness boost to that character and its neighbors.

> **[FR 19]** The CEO can trigger "Free Pizza Friday", at a currency cost, giving an instant happiness boost to every character on the map; the action is subject to a cooldown.

> **[Opn 3] 🔵** Two concrete actions beyond hire/fire are now decided (**[FR 18]**, **[FR 19]**); the complete list otherwise remains open for future iterations.

### 3.5 Random Events

> **[FR 20]** Random events occasionally interrupt the simulation with a two-option choice, each with a different cost/effect trade-off. The simulation tick (**[FR 5]**) pauses while a choice is pending.

> **[D 13]** A fixed pool of five themed events is used for this PoC (e.g. compliance audits, viral posts, reorgs, team-building, and office perks), each offering a "pay currency" option against a "take the happiness hit" option (or similar trade-off).

> **[Opn 5] 🔵** Expand and rebalance the random event pool beyond the initial five events.

## 4. Functional Requirements — User Interaction

> **[FR 9]** The user can click a character to view its stats.

> **[FR 10]** The user interacts exclusively via mouse clicks: selecting a character and activating action buttons. No keyboard input is planned.

> **[FR 11]** The user can pan the map (zoom is a fixed rendering scale, not a user control — **[TR 16]**).

> **[FR 12]** The selected character is highlighted with a visual indicator (e.g. a differently colored "floor" tile under the character).

> **[FR 13]** The hire control panel doubles as the class legend: each button carries a color swatch identifying its class. A separate legend panel is not shown.

> **[TR 19]** The hire panel is positioned at the top-left of the play area (not bottom-left), sized larger, with a larger button font than the original implementation.

> **[FR 14]** Buttons (hire panel, fire action) give immediate visual feedback when clicked (a pressed/flash state), independent of whether the underlying action succeeds.

> **[FR 15]** Currency (BSJ) and current staff headcount are shown in a dedicated panel, in the position previously occupied by the legend. These two values are no longer shown in the top ticker, which now only shows survival time and the best local record.

> **[TR 20]** The currency readout uses a green gradient and visually pulses (brighter/scaled up on increase, dimmer/hue-shifted on decrease) whenever the displayed value changes.

## 5. Technical Requirements

> **[TR 1 .Must]** Tech stack: vanilla HTML/CSS/JS, no framework.

> **[TR 2]** Isometric view rendered via Canvas 2D (`<canvas>` + 2D context).

> **[TR 3]** The map is made of a grid of isometric tiles based on images/sprites.

> **[TR 4]** Graphic assets (tiles, character sprites) will be generated with the assistant's help at a later stage.

> **[TR 5]** Character movement is animated via multi-frame sprite sheets.

> **[TR 6]** The map is represented internally as a 2D array (rectangular grid).

> **[TR 7]** Map size: 15×15 tiles.

> **[TR 8]** Rendering/animation uses `requestAnimationFrame`; character state/needs updates (**[FR 5]**) are handled with a separate fixed-interval tick, decoupled from the frame rate.

> **[TR 9]** The stats/actions panel for the selected character is an HTML overlay positioned above the canvas (not drawn inside the canvas).

> **[TR 10]** Map panning happens via mouse movement over the play area (edge-panning), not via click-and-drag.

> **[TR 17]** The camera is clamped to the map's actual bounds, with only a small padding margin — panning cannot reveal a wide area of empty space beyond the map edges.

> **[TR 18]** The edge-pan trigger zone (**[TR 10]**) is kept narrow, so it does not fire while the pointer is simply travelling across the play area toward a side panel.

> **[TR 11]** Happiness/energy on a 0–100 scale.

> **[TR 12 .Must]** Pixel art visual style, inspired by Final Fantasy Tactics Advance / Balatro, with a bright, high-saturation palette (avoid low-contrast/dark tones).

> **[TR 13]** Isometric tile size: 64×32 px.

> **[TR 15]** Character movement uses continuous, interpolated motion between adjacent grid cells (smooth glide at a fixed speed), animated via multi-frame sprite sheets (**[TR 5]**). *(v3: reverses the discrete cell-to-cell jump introduced in v2 — see Changelog.)*

> **[TR 16]** The map view renders at a fixed ~150% magnification from the start of the game; there is no in-game zoom control (**[FR 10]**'s mouse-only interaction is unaffected).

> **[TR 25]** Lightweight audio and milestone-toast feedback are layered on top of the simulation: short synthesized tones (Web Audio API, no external audio assets) on key actions/events (hire, fire, pep talk, pizza, burnout onset, event opening, milestones), and transient on-screen toast notifications at fixed survival-time milestones.

> **[Opn 4] 🔵** Define the exact format/size of the source character artwork and the finalized color palette (silhouette distinction per class and rendering technique are decided, **[D 12]**, **[TR 21]**).

## 6. Open Points and Assumptions — Summary

- **[Opn 1] 🔵** Needs/stats beyond happiness, and how they influence behavior.
- **[Opn 2] 🔵** Character movement and pathfinding logic.
- **[Opn 3] 🔵** Complete list of CEO actions beyond hire/fire/pep talk/pizza (**[FR 18]**, **[FR 19]** now decided).
- **[Opn 4] 🔵** Source character artwork exact format/size and finalized color palette (silhouette distinction and rendering technique already decided, **[D 12]**, **[TR 21]**).
- **[Opn 5] 🔵** Expand/rebalance the random event pool beyond the initial five events.
- **[A 1] 🟡** Exact burnout threshold value.
- **[A 2] 🟡** Exact hire/fire cost values.
- **[A 3] 🟡** Per-class burnout duration before disappearance (see table in section 3.1).
- **[O 1] 🟢** Shared leaderboard (future option, out of scope for the PoC).

## Changelog

- Consolidated the currency channels (D 9) into a single mechanism: individual output modulated by happiness, instead of two independent effects (individual + direct social effect on currency).
- Added baseline happiness decay (D 7) to ensure constant pressure on the player.
- Fixed numbering: restored D 2 and D 3 (single-player/simulation, single map), which had been mistakenly omitted in an earlier version of the document. Consolidated the two duplicate open points about stats (now Opn 1).

### v2

- Added **[BR 3]**: English adopted as the reference language for both this specification and the game's UI text (the implemented UI had drifted to Italian; this closes that inconsistency).
- Reduced map size from 50×25 to **15×15** tiles (**[TR 7]**), for better playability and readability at the intended zoom level.
- Added **[TR 15]**: character movement is now specified as a direct, discrete transition between adjacent grid cells, with no continuous/interpolated intermediate position — supersedes the implicit continuous-glide behavior of the first implementation.
- Added **[TR 16]** and updated **[FR 11]**: introduced a single discrete zoom level (~200%), reversing the earlier "zoom is not planned" decision.
- Refined **[TR 12]**: specified a bright, high-saturation palette — the first implementation had defaulted to low-contrast, overly dark tones.
- Added **[D 12]**: character sprites must be visually distinct per class (unique silhouette, not just a recolor), narrowing **[Opn 4]** accordingly.

### v3

- Reversed **[TR 15]**: back to continuous, interpolated movement between adjacent cells (smooth glide), superseding the discrete cell-to-cell jump introduced in v2. Movement is still strictly cell-to-adjacent-cell (**[TR 14]**'s adjacency model is unaffected) — only the transition's visual continuity changes.
- Amended **[TR 16]**: removed the interactive zoom toggle — the map now renders at a fixed ~150% scale from the start, with no zoom control exposed to the user. Reverted **[FR 11]** to pan-only accordingly.

### v4

- Added **[TR 17]**: the camera is now clamped tightly to the map's actual bounds (small padding only), instead of the earlier generous canvas-fraction margins — reduces empty space visible while panning.
- Added **[TR 18]**: shrank the edge-pan trigger zone (**[TR 10]**) so it no longer fires while the pointer is travelling toward a side panel.
- Added **[FR 13]** and **[TR 19]**: the hire panel now doubles as the class legend (per-button color swatch); the separate legend panel is removed. The hire panel moved to the top-left, enlarged, with a larger button font.
- Added **[FR 14]**: buttons now give immediate visual click feedback (pressed/flash state).
- Added **[FR 15]** and **[TR 20]**: currency (BSJ) and staff headcount moved into a dedicated panel (former legend position), with a green gradient currency readout that pulses on increase/decrease; both values removed from the top ticker (now showing only survival time and best record).
- Added **[TR 21]**: character sprites are now pre-rendered per class on an off-screen canvas and scaled up with nearest-neighbor sampling, for a genuinely pixel-art look that is uniform in technique across classes while remaining structurally distinct — refines the sprite work introduced by **[D 12]** and narrows **[Opn 4]** further.
### v5

- Added **[FR 16]** and **[TR 22]**: hiring now uses manual placement — the player picks the target cell by clicking an empty tile, with valid cells highlighted; clicking an occupied cell cancels placement and selects that character.
- Added **[FR 17]**: selecting a character now draws color-coded adjacency links to its neighbors, making the effect of **[D 8]**'s relation matrix visible instead of purely implicit.
- Added **[FR 18]** ("Pep Talk") and **[FR 19]** ("Free Pizza Friday"): two new CEO actions with instant happiness effects, at a currency cost; narrows **[Opn 3]**.
- Added **[FR 20]**, **[D 13]**, and **[Opn 5]**: introduced a pool of five random two-choice events that pause the simulation tick while a choice is pending.
- Added **[D 14]** and **[TR 23]**: baseline happiness decay (**[D 7]**) now ramps up gradually over a run instead of staying flat, for a rising difficulty curve.
- Split **[A 1]** into the burnout threshold (unchanged) and a new **[A 3]**: burnout duration before disappearance is now per-class instead of a single global value (see table in 3.1).
- Added **[TR 24]** and amended **[D 12]**: the in-burnout tint is more saturated and the exclamation-mark indicator is enlarged/outlined for legibility; Task Master's base color was moved away from red to avoid clashing with the (also red) burnout tint.
- Added **[TR 25]**: lightweight Web Audio sound cues and survival-milestone toast notifications, no external assets.