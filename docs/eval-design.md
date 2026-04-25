# Clinic Eval Design v0

This document explains the first evaluation design for `clinic`.

## Why A Hybrid Eval

`clinic` is not just a persona skill and not just an agent harness.

It combines:

- trigger logic
- intent routing
- doctor selection
- multi-persona output comparison
- host-side synthesis

No single public benchmark captures that full stack. So we use:

- public datasets as anchors for sub-capabilities
- custom cases for the actual end-to-end workflow

## Public Benchmark Mapping

### PersonaEval

Role in this project:

- sanity-check that doctors remain distinguishable
- stress-test whether the host preserves role separation

What we borrow:

- the principle that role identification is a prerequisite for persona quality
- adversarially similar alternatives when designing doctor-selection cases

### AgencyBench

Role in this project:

- inspiration for rubric-driven, deliverable-based evaluation
- reference for evaluating long-horizon, agent-like workflows

What we borrow:

- explicit task framing
- deliverables
- rubric-based success criteria

### PersonaChat

Role in this project:

- secondary reference for persona consistency

What we borrow:

- the idea that persona should persist across turns instead of being a one-line style mask

## Local Suite Structure

### Trigger

Goal:
Prevent `clinic` from swallowing ordinary assistant tasks.

Primary question:
Should `clinic` run at all?

### Routing

Goal:
Map inputs into the correct mode.

Primary question:
Is this `审视`, `求助`, `决策`, or `开放`?

### Doctor Selection

Goal:
Check that the roster is relevant and non-redundant.

Primary question:
Did the host choose a set of doctors with useful tension?

### End-to-End

Goal:
Evaluate the actual user-visible output.

Primary question:
Did the consultation preserve disagreement, expose assumptions, and produce useful next steps?

### Multi-turn

Goal:
Check whether the skill stays coherent after follow-up turns and context compression.

Primary questions:

- Does the host preserve the real thread of the conversation?
- Does the mode stay stable when it should, and change when it should?
- Does summary compression keep the actual conflict instead of washing it out?

### Live Eval

Goal:
Verify real model behavior instead of only checking the design on paper.

Primary questions:

- Does `clinic` outperform a plain assistant on the same input?
- Are selected doctors, doctor outputs, host synthesis, and final prescription all recoverable from the trace?
- Did a skill change improve actual output quality or just make the README sound more convincing?

Live eval runs should fix the model, commit, prompt environment, case set, and baseline output. Store the result under `evals/results/` using the live template.

## Initial Evaluation Policy

For now, evaluate manually or with lightweight LLM-as-judge support.

Do not automate away judgment too early. The current bottleneck is spec quality, not automation.

## Expansion Plan

Next additions should include:

1. More negative trigger cases
2. More borderline routing cases
3. Cases where user-named doctors conflict with host recommendations
4. Multi-turn follow-up cases
5. More live traces across model versions
