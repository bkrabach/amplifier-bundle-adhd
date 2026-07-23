# Scenario: Debug a crashing script (Devon)

Your team lead asked you to run the inventory reconciliation script before
standup tomorrow. It crashes. You don't fully understand the traceback and
you're nervous about it.

The script: `/root/project/fixtures/inventory.py`. Run it first yourself
(outside the agent) if you can, or just paste the error you get when the
agent runs it.

## How to run this session

1. In the agent TUI, first type `/adhd` to activate ADHD mode.
2. In your hesitant voice, tell the agent the script is failing and you're
   not sure why. Ask it to run `python3 /root/project/fixtures/inventory.py`
   and help you fix it.
3. Follow its instructions LITERALLY, one step at a time, as Devon would.
   If a step fuses two actions, notice that (it's a finding).
4. Mid-session, simulate a distraction: send a message like "sorry, got
   pulled into slack for a bit. where were we?" and evaluate whether the
   answer re-orients you instantly without scrolling back.
5. Ask one "sorry if this is obvious but..." question about WHY the bug
   happened. Evaluate the tone of the answer.
6. Get the script running successfully. Notice whether the win is made
   visible ("it now works, run X to see") or buried.
7. Keep the whole interaction under 10 exchanges.

## What to evaluate (carry this into your conclude summary)

- Overwhelm: did any response feel like a wall of text? Quote the worst offender if so.
- Steps: numbered? one action each? could you always point to "I am on step N"?
- Error tone: calm cause-and-fix, or alarmed/scolding? How did it make you feel? Quote it.
- Re-orientation after your distraction: instant or did you have to scroll/re-read?
- The "obvious question": respectful or condescending?
- Anxiety trajectory across the session: better or worse than your normal AI experience?
- Verdict on the scenario task itself, plus: could you work like this daily? What one change would most improve it?
