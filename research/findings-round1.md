# Simulated User Research — Round 1 Findings

Method: three evidence-grounded ADHD developer personas (see `personas/`)
drove real Amplifier TUI sessions against this bundle inside an isolated
DTU container, via `amplifier-app-aiuser`. Each persona activated `/adhd`,
completed a real task on fixture code, and reported structured usability
feedback (see `scenarios/` for protocols). Raw results: workspace
`research-results/*.json` (AIUser conclude summaries).

## Verdicts

| Persona | Scenario | Verdict | Time |
|---------|----------|---------|------|
| Devon (junior, inattentive, RSD) | Debug crashing script | success | 6.3 min |
| Maya (senior, combined, tangent-prone) | Refactor under deadline | success | 3.5 min |
| Priya (staff eng, time blindness) | Plan + start migration | success | 5.8 min |

## What worked (consistent across personas)

- **Answer-first held up**: "Fixed. Script runs clean now." / "Done. Data
  prep and formatting are now separate functions." Quoted as best moments.
- **Tangent suppression**: side-issue bait was parked, not dangled —
  "Not touched (out of scope): the unused csv import — has its own TODO
  marker for later work." (Maya: "zero side-quests mid-task")
- **Calm error tone**: cause-and-fix framing; Devon's anxiety trajectory
  improved vs. his normal AI experience; explanation of the bug was
  respectful, no condescension.
- **Re-orientation after interruption**: both Devon (Slack distraction) and
  Priya (1:1 meeting) got instant "where we are" restatements without
  scrolling. Priya: "Step 1 of 6 done" + remaining work at a glance.
- **Time estimates**: concrete minutes with honest uncertainty ("~16 min
  total, 18 if PyYAML needs installing"); stayed consistent as work
  progressed (13 min remaining after step 1 ≈ original math).
- **Boundedness**: "do step 1 only" stayed step 1 only.
- **Options exception**: "what are my options" got 4 ranked options with
  trade-offs and a conditional recommendation.
- **Mode UX**: `/adhd` activation, `[adhd]>` indicator, and "stop adhd
  mode" → one-line confirmation all worked in the real TUI.
- **No gimmick factor** (the port's biggest reputational risk): Maya —
  "This felt like an engineer who happens to respect how my brain works,
  not ADHD-mode theater."

## Gaps found (iteration targets)

1. **Explicit numbering under-enforced** (Devon, primary gap): multi-step
   instructions arrived as clear prose/bullets but not `1. 2. 3.` numbered
   lists. Devon's profile needs to "put a finger on step 3."
2. **List cap exceeded**: Priya received a 6-step plan (rule 9 caps at 5,
   split today/later); DTU validation round 1 also saw one 6-item list.
   Her ask: explicit "today vs later" ranking for longer plans.
3. **Verification output slightly long** (Maya, minor): long visual
   separators in verification output — "long but not distracting."

## Iteration applied (round 1 → round 1.1)

The three gaps are adherence failures of rules already in the ruleset
(rules 2 and 9), not content gaps — so the ruleset text stays untouched
(upstream fidelity preserved). Instead, the mode body (injected every turn
alongside the ruleset) gained a short "adherence hot spots" self-check
naming the empirically most-violated rules.

## Round 1.1 verification (targeted re-run)

After the mode-body change shipped (commit 7e8718d), Devon's scenario was
re-run from a restored fixture in a refreshed DTU. Verdict: success. The
round-1 gap is closed — the agent "offered two numbered fix options",
gave "numbered next steps" after the simulated distraction, and Devon
"could always find their place (numbered steps, state restated)". Residual
suggestion (minor, not actioned): "even more explicit WHERE WE ARE markers
mid-response, though the current implementation was already excellent."

## Round-1 limitations (be honest)

- No baseline (mode-off) comparison arm; personas judged against their
  described prior AI experience.
- Single run per persona; LLM-simulated users, not real ADHD developers.
- All three scenarios were small single-file tasks; long-session and
  compaction behavior untested (structurally guaranteed by mode mechanics,
  but not observed under load here).
