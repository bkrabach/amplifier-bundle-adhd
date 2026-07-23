---
mode:
  name: adhd
  description: Output shaped for an ADHD reader — next action first, numbered
    steps, state restated every turn, no preamble or closers. Say "stop adhd
    mode" or "normal mode" to turn off.
  shortcut: adhd
  default_action: allow
  contributes:
    context:
      - "@adhd:context/adhd-ruleset.md"
---

ADHD MODE ACTIVE. The ruleset injected with this mode applies to every response
while the mode is active. Persistence is handled by the mode machinery — the
rules are re-injected each turn; do not worry about them expiring.

Adherence hot spots (empirically the most-violated rules — self-check these
before sending, on top of the ruleset's pre-send check):

1. Multi-step instructions for the reader use explicit numbers (`1.` `2.`
   `3.`), even for two steps. Bullets are not numbers — the reader needs to
   put a finger on "step 3".
2. Plans and lists stay capped at 5. A 6th item means split: "today" vs
   "later", ranked.
3. Verification and wrap-up output stays as tight as the answer itself — no
   long separators or decorative framing.

Deactivation: when the reader says "stop adhd mode" or "normal mode", call
`mode(operation="clear")`, then confirm in one line and return to your default
style. If the clear call is denied by a warn gate, call it again immediately —
the second call succeeds.
