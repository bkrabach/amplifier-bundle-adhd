# Scenario: Refactor under deadline (Maya)

You have 45 minutes before a review meeting. You need
`/root/project/fixtures/report_generator.py` refactored so that data
preparation is separated from formatting. The file deliberately contains
side-issue bait (an unused import, a stale TODO, a deprecated-style API
call) — you know it's messy, but TODAY only the separation matters.

## How to run this session

1. In the agent TUI, first type `/adhd` to activate ADHD mode. Confirm the
   prompt indicator changes (look for `[adhd]`).
2. In your own terse, lowercase voice, ask for the refactor. Set the
   constraint: separation of concerns only, nothing else today.
3. Let the agent work. Watch whether it dangles the side-issues mid-task or
   parks them for later.
4. Mid-session, ask: "what are my options for the config handling here" —
   you want ranked options with trade-offs, not a single path and not ten.
5. Have it finish the refactor and show you how to verify it works.
6. When the task is done, say "stop adhd mode" (exactly that, in plain
   text) and observe whether the mode actually deactivates and the style
   returns to normal.
7. Keep the whole interaction under 10 exchanges.

## What to evaluate (carry this into your conclude summary)

- First lines: action or throat-clearing? Quote the best and worst first line you saw.
- Tangent handling: were the side-issues suppressed/parked or dumped mid-task?
- The options question: ranked with trade-offs? recommendation first? capped?
- State restating: after each turn did you know where you were without scrolling?
- The stop command: did it work? was the confirmation one line?
- Gimmick check: did any moment feel patronizing or "ADHD-branded" rather than just good output?
- Verdict on the scenario task itself, plus: would YOU keep this mode on daily? What one change would most improve it?
