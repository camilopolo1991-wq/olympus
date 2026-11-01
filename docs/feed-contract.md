# Feed contract: how Olympus is fed, and what the backend must keep

This file is the integration point. The first server (`server.py`) is a tail over one file. A later backend may add Claude Code hook events and Hermes session summaries, but it keeps this contract, so the page never changes when the backend does.

## 1. The source of truth

One append-only, monotonic step log, one line per step, written by the loop and gated by a secret-and-name scan at every commit. Measured on 2026-11-01: 1,620 lines since 2026-10-22, 1-second timestamps, a peak of 2 lines per second and 10 per minute.

Grammar of a regular line:

```
- <UTC> <GOAL> <STEP> <KIND> <free text>
```

- `<UTC>`: `YYYY-MM-DDTHH:MM:SSZ`.
- `<GOAL>`: the goal id, like `KIT-06`, or an owner pseudo-goal like `OWNER-2026-10-31`.
- `<STEP>`: `T<nn>` (a task), `W<nn>` (a window), `GOAL`, `START`, `CLOSE`, `AUDIT` or another word.
- `<KIND>`: the fifth word. About three percent of lines have a shifted fifth word; a parser treats an unknown kind as a plain note and never drops the line.

Kinds and what they drive:

| kind | drives |
|---|---|
| START | goal RUNNING |
| DISPATCH `<role>` | the role figure leaves its hut for its site; `<role>` is the sixth word: scout, writer, reviewer (the auditor appears only through audit run logs) |
| RETURNED, DONE, PASS, FAIL, FAIL(n), BLOCKED, PARTIAL, LANDED, LANDED-PARTIAL, ANSWERED | the figure returns; the task's last word; FAIL(n) sets retries n |
| TRIPWIRE OPEN / TRIPWIRE CLOSE | the window `W<nn>` opens or closes; the board lights while open |
| INCIDENT, DENIED, DENIAL, DEVIATION, NOISE, OWNER-NOISE | incident list; INCIDENT flashes |
| ROLLBACK | a writer recorded its rollback before editing |
| COMMIT, LANDED, PUSH | record stamp; the sha is a hex token of 7 to 40 characters in the text |
| HELD | goal HELD; the map dims; the gate banner shows |
| CLOSED, or a GOAL line holding "CLOSED DONE" | goal DONE |
| GATE, NEEDS-DECISION, RULING, DECISION, FINDING, CORRECTION, REPORT | decisions and notes |

## 2. Entities

- God: a Hermes profile; static; title from the profile's `ui_meta.title`. Busy from the modification time of a fresh dispatch run log only, never its content.
- Lesser god: one of five roles. Working from its DISPATCH until a returning kind on the same step.
- Goal: id, status PLANNING, RUNNING, HELD, DONE; header fields from the plan file's Live line when available.
- Task: `(goal, T<nn>)`, last word, retries.
- Window: `(goal, W<nn>)`, open or closed.
- Incident, Commit, Decision: as above.

## 3. The server contract

- `GET /` serves `index.html` and the folder, on 127.0.0.1 only.
- `GET /events` is Server-Sent Events, `text/event-stream`, UTF-8. Each event: `id: <byte offset after the line>`, `data: <json>`. A client that reconnects sends `Last-Event-ID`; the server resumes from that offset. On connect without an id the server replays the whole file, then streams.
- Event JSON: `{"seq": <offset>, "utc": "...", "goal": "...", "step": "...", "kind": "...", "role": "<role or null>", "text": "..."}`.
- Polling: stat the file every 500 ms; read from the last offset; emit complete lines only; keep a partial tail; if the size shrinks, reset to 0 and replay.
- Masking before any line leaves the process: every token of 16 or more hex characters is cut to its first 8; every path of three or more segments is cut to its last two; where the loop's redactor module is available, the line passes through it as well. A test plants one token and one path in a fixture log and asserts the masked output.
- Idle: when no goal is running (no START without a later CLOSED or HELD), poll every 30 s.
- Nothing is written anywhere by the server.

## 4. Later sources, same events

- Claude Code hooks: `SubagentStart` and `SubagentStop` carry `agent_type` (the agent file's name, for example `loop-scout`). An http hook or an async command hook can post the JSON to this server, which turns it into an event with kind `AGENT-START` or `AGENT-STOP` and `role` from the agent type. These move a figure before its log line lands. Enabling a hook is a settings edit, the owner's gate.
- Hermes session summaries: a profile's state database, opened read-only, sessions table only (model, tokens, cost, tool calls, started, ended), never the messages table. One tile per god. The owner's gate.
- Telemetry: an OTLP receiver for cost per agent name. Later.

## 5. What never changes

The event JSON shape, the masking rule, the read-only rule, the seat titles and role names, and the rule that every number on screen names the line kind it counts.
