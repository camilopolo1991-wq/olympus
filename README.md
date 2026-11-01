# Olympus

The front end of the Pantheon: a pixel-art island where the gods (the bots) and the lesser gods (the loop's agents) are seen working, fed by one append-only step log.

Three claims a stranger can verify:
1. The page runs from one command and shows a goal from its first log line.
2. A new log line moves a figure within two seconds.
3. The feed serves no name and no secret: a planted token and a planted path are masked before they leave the server, and the row that proves it is in the tests.

## Layout

- `index.html`, `app.js`: the page. Phaser 4 from cdnjs, pixel-art mode, Tiled JSON map, HTML panels.
- `map.json`: the island, 16 px tiles.
- `assets/`: CC0 and CC-BY tiles and sprites, every file named in `CREDITS.md`.
- `server.py`: Python standard library only. Serves the folder on 127.0.0.1 and `/events` as Server-Sent Events, tailing the step log by byte offset. This is the piece the Forge replaces or extends under `docs/feed-contract.md`.
- `sample.log`: sixty lines in the step-log grammar, so the page runs with no real record.
- `docs/feed-contract.md`: the log grammar, the event model and the server contract. The integration point for the backend.
- `docs/research-2026-11-01.md`: the research behind the choices.
- `docs/design-brief.md`: the brief the first build was made from.
- `docs/mockup/olympus.html`: the first mockup, Canvas 2D, no dependencies, with a snapshot of two real goals. The visual starting point.
- `tests/`: the acceptance rows.

## Run

```
python server.py --log sample.log
```

Then open http://127.0.0.1:8765. Point `--log` at a real step log to watch a live goal.

## Rules of the house

- Read-only against everything outside this folder.
- No real person's name anywhere; the seats are The Chair, The Forge Master, The Messenger, The Tide, The Keeper; the roles are leader, scout, writer, reviewer, auditor.
- Every number on screen says which log line kind it counts.
- Every asset has a line in `CREDITS.md` with its author and licence.
