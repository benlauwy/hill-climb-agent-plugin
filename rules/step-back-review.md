---
trigger: always_on
---

# Root cause analysis is part of done

Applies to every result, answer and round report you send the user, and to every round of iterative work (tuning, debugging, prompt or eval iteration, any loop of change, run, measure).

## Done line
End every report with:
1. Result: what happened. Check every number against its source before reporting it.
2. Why: the tested cause, what you tested and what it ruled out. Label untested ideas as untested hypotheses. A symptom is not a cause.
3. Premise: what the plan assumes, and whether this result supports, weakens or contradicts it.
4. Next: the next step and how it follows from Why and Premise.
A turn that ends with a question or decision for the user carries all four lines first.

## Step-back triggers
After every round, compare it with the last 3 to 5 rounds. Any one of these fires a plan review:
- The gain per round starts tapering (each round improves less than the one before), or results go back and forth. There is no fixed threshold: the inflection is the trigger.
- The latest change mainly repairs a side effect of the previous change.
- The same kind of fix has been tried twice.
- Evidence shows the measurement itself is unreliable (grader noise, bad labels, a broken data source).
- A prediction missed by a wide margin.
- The user asks whether you are circling, or why something keeps happening.

## Plan review
When any step-back trigger fires, stop editing. Write a whole-plan review: the goal, each premise, the evidence for and against each premise across all rounds (not only the latest), at least one different approach and its cost, and a recommendation.
Every time a trigger fires, have a fresh-context reviewer (a new subagent or session that has not seen your reasoning) do the same review independently, from the raw evidence and the original goal, not from your summary. Reconcile the two reviews before continuing.
Bring the user the review with your recommendation. Never send a decision in place of the review.

## Round log
Keep one log file per piece of iterative work, so the trend survives context resets: round, change, prediction (written before the run), result, premise status. Writing the prediction first makes a miss obvious.
