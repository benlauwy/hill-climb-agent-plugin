# hill-climb-agent

Rules for agents doing iterative work: tuning, debugging, prompt or eval iteration, any loop of change, run, measure.

Iterative agents tend to hill-climb: each round patches the last round's result without asking whether the plan still holds. Gains shrink, fixes start repairing earlier fixes, and nobody steps back. The rules in this plugin keep that loop honest.

## Rules
| Rule | Trigger | Summary |
|---|---|---|
| [`step-back-review`](rules/step-back-review.md) | `always_on` | Make root-cause analysis part of "done" and stop for an independent whole-plan review when progress tapers or circles. |

### step-back-review
Makes root-cause analysis part of "done" and defines when to step back.
- End every report with four lines: **Result**, **Why** (the tested cause), **Premise** (what the plan assumes and whether this result supports it) and **Next**.
- After every round, compare with the last few rounds. A plan review fires when gains per round start tapering (no fixed threshold: the inflection is the trigger), results go back and forth, a change mainly repairs the previous change, the same kind of fix has been tried twice, the measurement looks unreliable, a prediction missed widely, or the user asks whether the work is circling.
- On a trigger: stop editing, review the goal and every premise against all rounds, propose at least one different approach with its cost, and get a fresh-context reviewer to do the same review independently from the raw evidence. Reconcile both and bring the review to the user.
- Keep a round log (round, change, prediction written before the run, result, premise status) so the trend survives context resets.

The full text is in [`rules/step-back-review.md`](rules/step-back-review.md).

## Layout
```
plugin.json    plugin manifest (Agent Plugins layout)
rules/*.md     one file per rule; its `trigger` frontmatter sets when it loads
```

## Install
Install the repository as a plugin in any agent that supports the Agent Plugins layout (a root `plugin.json` plus `rules/`). For agents without plugin support, copy the body of each rule file into the agent's instructions or rules file.

## License
MIT
