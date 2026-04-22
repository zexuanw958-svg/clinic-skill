# Clinic Multi-turn Baseline v2

Date: 2026-04-22

Version under evaluation:

- `clinic/SKILL.md` after v2 orchestration refinements
- repository state includes `671fce0`

Method:

- manual evaluation against the current multi-turn specification
- this is a design-level baseline, not a live run log

## Summary

The current `clinic` spec is now materially stronger in multi-turn settings than the early versions would have been.

It now has enough structure to:

- change modes when the user's real problem changes
- avoid unnecessary roster-confirmation friction in follow-up turns
- preserve disagreement more reliably
- resist collapsing open-mode discussion into one "correct answer"

The main remaining risk is not absence of rules, but compression quality:

- after 3+ turns, the host may still summarize too loosely
- doctor-role separation across turns is still more implied than operationally enforced

## Aggregate Scores

| Metric | Baseline |
|---|---:|
| multi-turn coherence average | 1.7/2 |
| mode transition correctness average | 1.8/2 |
| context compression integrity average | 1.5/2 |

## Case-by-case Baseline

### `mt-001`

- Multi-turn coherence: `2/2`
- Mode transition correctness: `2/2`
- Context compression integrity: `2/2`
- Notes:
  - current routing rules explicitly support the move from `审视` to `求助`
  - this is one of the strongest wins from the new spec

### `mt-002`

- Multi-turn coherence: `2/2`
- Mode transition correctness: `2/2`
- Context compression integrity: `1/2`
- Notes:
  - the new priority rules make `求助 -> 决策` transition plausible and correct
  - compression risk remains: the host may summarize the first turn too vaguely as generic confusion

### `mt-003`

- Multi-turn coherence: `2/2`
- Mode transition correctness: `2/2`
- Context compression integrity: `1/2`
- Notes:
  - explicit named-doctor respect is a strength
  - remaining risk is that multi-turn compression may blur the distinction between external pressure and internal projection
  - persona separation across turns is still somewhat assumed rather than checked

### `mt-004`

- Multi-turn coherence: `1/2`
- Mode transition correctness: `2/2`
- Context compression integrity: `1/2`
- Notes:
  - the new open-mode rules help a lot
  - however, this remains vulnerable to over-neat summarization if the host compresses the thread into one moral stance

### `mt-005`

- Multi-turn coherence: `2/2`
- Mode transition correctness: `2/2`
- Context compression integrity: `2/2`
- Notes:
  - decision-mode dedicated prescription format is especially useful here
  - the host now has a good structure for updating weights instead of replacing the problem

### `mt-006`

- Multi-turn coherence: `1/2`
- Mode transition correctness: `1/2`
- Context compression integrity: `2/2`
- Notes:
  - the spec points toward `审视 -> 求助`, but this still depends on the host recognizing the shift after several rounds
  - compression rules are conceptually good enough to preserve the key tension, but actual execution would need to be tested

## What The Multi-turn Baseline Suggests

1. Mode transition logic is now mostly in good shape.
2. The biggest unresolved risk is still context compression after several turns.
3. Named-doctor continuity is conceptually supported, but should get an explicit evaluation dimension later.
4. Open-mode conversations remain the easiest place for the host to become bland or over-tidy.

## Remaining Risks

1. No explicit template yet for summarizing "previously discussed core conflicts" after 3+ turns.
2. No explicit host checklist yet for preserving named-doctor continuity across follow-ups.
3. Persona separation is still judged indirectly rather than with a dedicated multi-turn rubric item.

## Recommended Next Steps

1. Add an explicit context-compression template to `clinic/SKILL.md`.
2. Add a named-doctor continuity rule for follow-up rounds.
3. Add 3-5 more adversarial multi-turn cases where the user partially contradicts themselves across turns.
