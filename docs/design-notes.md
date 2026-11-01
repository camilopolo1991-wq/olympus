# Design notes

What the canvas produced on 2026-11-01, read from the export at docs/design/tiles.png and the session's screenshots. The canvas's own rationale text was not saved; these notes are the chair's reading of the artboards.

## 01 Overview, 1440 fluid

Header: OLYMPUS in the pixel title font with a Greek key underline, "the front of the Pantheon", then three boxes: GOAL (the last GOAL line, the labour id and its title), STATUS (RUNNING in bone white, HELD in red, DONE in green), LIVE (the last WINDOW line, the watch id, its age). Left two thirds: THE MAP. Olympus top-left on a grey crag with clouds: The Chair lit with a cyan bolt, The Tide and The Keeper as dark outlines with "not built", two dotted FUTURE plots at the edges. The Messenger as a dim figure on the pier. The Forge island bottom-right on green over sand: the smithy with its lit door, the anvil, the RECORD house, the WINDOW board, five huts with roofs in the role colours, the five figures. Under the map, five role cards: the role name in its colour, its state word, and where it is. Right column: GOAL (id, status, title, wall time and writes as Andean step meters with the kind captioned under each), DECISIONS (gold panel, the open decree with two buttons), COUNTERS (dispatches by role, PASS, FAIL, BLOCKED, PARTIAL, windows opened and closed, each with its line kind under it). Bottom: STEP LOG, last 40 lines, newest at the bottom, kind coloured.

## 02 Goal detail, 1440 fluid

Header with the labour id. Tasks T01 to T12 as rows: id, task title, role in colour; timeline bars from dispatch to pass or fail; retries as pips. Incidents list with id, text and severity. Noise list in grey.

## 03 and 04 God domains, The Chair and The Forge Master

The portrait large in its gold ring, the temple or the smithy, the god's stats (verdicts, gates judged, decrees drafted, brain notes for The Chair; labours built, decrees landed, riders for The Forge Master), and the god's agents as small figures with idle or working states.

## 05 Lesser god card

A popover for one role: name, colour, current trial, dispatch count, the last five lines about it, its hut.

## 06 Held state

The overview with the labour HELD: the map dimmed to embers, the gold banner "Gate waits for you" with three options drawn, recommendation first.

## 07 Sprite sheet spec, 640 by 400, 16 px grid shown 2x

Rows for the five roles in the role colours, four directions (down, up, left, right), three frames each (idle, walk A, walk B). Seats at 16 by 24: CHR, FRG, TID, KPR, MSG, the unbuilt ones as outlines. Portraits at 64 by 64 in the gold ring: The Chair (white beard, cyan eyes, bolt), the Forge Master (gold visor, hammer), and the unbuilt seat ring with a question mark. A state row: idle, walk, work, retd, blkd, wait. Swatches: GND, STL, GLD, AMB, CYN, BON, SKN, STN and the five role colours plus TID, KPR, MSG.

## 08 Tile sheet spec, 640 by 400

Temple pieces lit and unlit with the key pattern, the pier, huts, the Greek key and Andean step border tiles, panel bevels at 1 px, and the rest of the tiles the brief lists.

## Rationale, the chair's

- One world: the panels are pixel art too, so the map and the chrome read as one screen.
- Every number carries its line kind in grey under it, which is the honesty rule of the whole project.
- The unbuilt seats are drawn, not hidden, so the map shows what is coming and grows a domain per god.
- The role cards under the map repeat the figures' state in words, for a reader who does not watch the map.

## Alternatives considered

- Cinematic portraits beside pixel art: rejected by Fate, it clashes.
- Common dashboard words: rejected, the screen uses the mythology with the loop word beside it.
- A generic office simulator: rejected, the Pantheon map is the product.
