# Design tokens

Source: the brief, the feed contract and the canvas export at docs/design/tiles.png (overview, goal detail, sprite sheet, tile sheet). The canvas's own token reply was not saved; these values are the brief's and were read back from the export. A builder that measures a different value in the export follows the export and notes it here.

## Colours

| token | hex | use |
|---|---|---|
| ground | #07080c | page background, sea at night |
| panel | #1b1f27 | panel fill, map chrome |
| steel | #2d3745 | panel borders at 1 px, inactive bevels |
| gold | #e3b341 | titles, Greek key borders, the leader, The Chair's accent, meters |
| amber | #ff8a3d | ember, the anvil when a writer works, the Forge Master's accent, wall-time meter fill |
| cyan | #35d6ff | live signals: an open watch (window), the bolt over The Chair, the LIVE box |
| bone | #e9e4d6 | body text |
| grey | #8a93a3 | captions under numbers, the kind each number counts |
| green | #46c46e | PASS, DONE, the writer |
| red | #e5484d | FAIL, HELD, INCIDENT, the auditor |
| blue | #4c8dff | DISPATCH, the scout |
| violet | #c678dd | the reviewer |
| teal | #2a9d8f | The Tide's accent (unbuilt: outline only) |
| ash violet | #6f5a8f | The Keeper's accent (unbuilt: outline only) |
| silver | #b8c0cc | The Messenger's accent (unbuilt: dim figure) |

## Fonts

| use | font | size at 1x |
|---|---|---|
| titles, panel headers, big numbers | Press Start 2P (Google Fonts) | 16 px titles, 10 px panel headers, 20 px big numbers |
| panel body, labels, buttons | VT323 (Google Fonts) | 18 px body, 14 px labels |
| step log ticker, hashes | monospace (system) | 12 px |

## Layout

| token | value |
|---|---|
| page width | fluid, designed at 1440 px; map takes two thirds, panels one third (panel column 440 px) |
| map canvas | 480 by 270 logical px, shown at 3x (1440 by 810) with pixel-perfect scaling; 16 px tiles, 30 by 17 tiles visible |
| map zoom lever | 2x, 3x, 4x |
| panel padding | 12 px; panel gap 12 px |
| borders | 1 px steel; active panel 1 px gold; Greek key strip 8 px tall under every panel header |
| meters | Andean step pattern, 8 px tall, fill in amber (wall time) or cyan (writes) |
| figure | 16 by 24 px (one tile wide, one and a half tall), 3 frames per direction, 4 directions |
| portrait | 64 by 64 px in a 72 px gold ring, 2 px ring |
| temple | 48 by 40 px footprint; unbuilt seats drawn as 1 px outlines with the label "not built" |
| hut | 16 by 16 px, roof in the role colour |
| ember intensity lever | 0 to 4, number of ember particles per frame over the anvil |

## State to visual, one row per log line kind

| kind | what changes on screen |
|---|---|
| START | labour status RUNNING; day counter starts; the record house door lights gold |
| DISPATCH scout | Argus walks from his hut to the record house; a white dot above him while away; scout counter +1 |
| DISPATCH writer | Brontes walks to the anvil; the anvil glows amber and embers rise; writer counter +1 |
| DISPATCH reviewer | Momus walks to the record house; reviewer counter +1 |
| RETURNED, ANSWERED, DONE | the figure walks home; its hut window lights for 2 s |
| PASS | figure home; task row turns green; PASS counter +1; XP +10; the chronicle stamp if the line names a commit |
| FAIL, FAIL(n) | figure home; task row turns red with n pips; FAIL counter +1; Momus's catches +1 |
| BLOCKED | figure sits at its hut, grey; BLOCKED counter +1 |
| PARTIAL | figure home; task row gold; PARTIAL counter +1 |
| LANDED, LANDED-PARTIAL | task row green or gold with "landed"; the chronicle stamp |
| TRIPWIRE OPEN | the WINDOW board lights cyan; Daedalus walks to the board; LIVE box shows the watch id and its age |
| TRIPWIRE CLOSE | the board goes dark; Daedalus walks home; streak +1 when the close text holds "exit 0" without a difference, else the streak resets |
| INCIDENT, DENIED, DENIAL, DEVIATION | the frame flashes red once; omen list +1 |
| NOISE, OWNER-NOISE | omen list +1 in grey, no flash |
| ROLLBACK | a small scroll icon over the writer's hut for 2 s |
| COMMIT | the chronicle stamp over the record house for 2 s; commits counter +1 |
| PUSH | a rider leaves the pier toward the sea edge for 3 s; pushes counter +1 |
| HELD | labour status HELD; the map dims to embers; the gold gate banner shows with the gate text |
| CLOSED, or a GOAL line holding CLOSED DONE | labour status DONE; the record house glows; the badge "labour closed" |
| GATE, NEEDS-DECISION | the decisions banner shows the question and two or three options |
| RULING | the banner clears; a bolt flashes over The Chair; the badge "verdict" |
| REPORT, FINDING, CORRECTION, DECISION, NOTE | ticker only |
| unknown kind | ticker only, grey |
