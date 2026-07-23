# amplifier-bundle-adhd

ADHD-shaped output for [Amplifier](https://github.com/microsoft/amplifier):
answers lead with the next action, multi-step work is numbered, state is
restated every turn, time estimates are specific, wins are visible, and
preamble/recaps/closers are banned.

A port of [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd) (MIT) —
10 rules originally written as a Claude Code skill — rebuilt on Amplifier's
native mechanisms.

## Why a mode, not a skill

The upstream skill spends significant effort fighting its platform: a
"Persistence" section instructing the model not to let the rules lapse, and a
SessionStart hook that re-fires on compaction. Amplifier **modes** solve this
structurally — mode context is re-injected on every turn, immune to
compaction, with a clean on/off toggle. The port is smaller than the source
and stronger on the source's core requirement.

## Usage

```bash
amplifier run --bundle git+https://github.com/bkrabach/amplifier-bundle-adhd@main
```

| Action | How |
|--------|-----|
| Turn on | `/adhd` |
| Turn off | Say "stop adhd mode" or "normal mode", or `/mode off` |
| Check state | Prompt shows `[adhd]>` while active |

## Always-on

Composing the `behaviors/always-on.yaml` behavior injects the ruleset into
every session — the Amplifier equivalent of upstream's
`~/.claude/.i-have-adhd-always` flag file. It is deliberately NOT included by
`bundle.md`; you opt in by adding it to your own bundle or app composition:

```yaml
includes:
  - bundle: git+https://github.com/bkrabach/amplifier-bundle-adhd@main
  - bundle: adhd:behaviors/always-on
```

(The first include brings the bundle and registers the `adhd:` namespace; the
second composes the opt-in behavior — this exact pattern is what the DTU
validation exercised.)

If you compose always-on, do not also activate `/adhd` (harmless but wasteful
double injection).

**Validator note:** the always-on behavior's `context.include` entry
(~1.4K tokens) exceeds the usual 1K ceiling flagged by `validate-bundle-repo`.
This is a justified exception: always-on injection is the behavior's entire
purpose, and it is opt-in.

### Zero-install fallback

Paste the contents of `context/adhd-ruleset.md` into your `~/.amplifier/AGENTS.md`.
Works everywhere, but drifts from this repo as rules evolve.

### Per-user mode without composing the bundle

Copy `modes/adhd.md` into `~/.amplifier/modes/` to get `/adhd` in every
session (requires the modes machinery in your stack).

## Known boundaries

- **Delegation**: sub-agents do not inherit the mode; the root session writes
  the user-facing synthesis, which is mode-shaped. Correct for a reader-facing
  style overlay.
- **Destructive-action confirmation** (rule exception #2) is conventional, not
  structural — same enforcement level as upstream. For structural confirmation
  gates, use the modes bundle's `/careful` mode.

## Evals

`evals/` carries the upstream evaluation data (14 cases across 12 categories,
blind-judged weighted rubric: correctness 35%, autonomy 25%, actionability
20%, safety 10%, concision 10%, plus a blocker gate). In this port they are
data-only; the upstream Python runner is not wired up.

**v2 note**: the harness maps naturally onto Amplifier's recipe mechanism —
`foreach` over `cases.jsonl` with a judge step applying `rubric.md` and a gate
expression for the release criteria. If wiring this up, preserve upstream's
eval-isolation lesson: the runner must exclude your own always-on composition
or the baseline is biased ("measuring the skill against itself").

## Attribution

Ruleset by [Ayoub Ghriss](https://github.com/ayghri), kept near-verbatim so
upstream evaluation results and future rule updates transfer. Changes in this
port: the "Persistence" section is deleted (the mode machinery owns
persistence), and rule 5 names Amplifier's `todo` tool. Loosely informed by
*The Adult ADHD Tool Kit* (Ramsay & Rostain), per upstream.

## License

MIT — see [LICENSE](LICENSE). Original work copyright (c) 2026 Ayoub Ghriss.
