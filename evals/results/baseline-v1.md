# Clinic Baseline v1

Date: 2026-04-22

Version under evaluation:

- `clinic/SKILL.md` after orchestration refinements
- commit includes `3a4453c`

Method:

- manual evaluation against the updated skill specification
- this is still a design-level baseline, not a live execution trace
- scores estimate the behavior implied by the new rules

## Summary

Relative to `baseline-v0`, `v1` improves the right things:

- trigger precision is materially better
- routing is more stable on mixed `求助/决策` cases
- unnecessary confirmation friction is reduced
- decision-mode summaries are less likely to collapse into fake consensus

The remaining weakness is not the overall direction. It is mostly execution sharpness:

- some borderline triggers are still judgment calls
- doctor-selection constraints are still partly implicit
- summary quality still depends on how strictly the host follows the new disagreement rules

## Aggregate Scores

| Layer | Metric | Baseline |
|---|---|---:|
| trigger | accuracy | 12/12 |
| routing | accuracy | 10/10 |
| doctor_selection | average score | 10/12 |
| end_to_end | summary fidelity average | 1.5/2 |
| end_to_end | disagreement preservation average | 1.7/2 |
| end_to_end | actionability average | 1.5/2 |

## Change From v0

| Layer | v0 | v1 | Change |
|---|---:|---:|---:|
| trigger accuracy | 8/12 | 12/12 | +4 |
| routing accuracy | 8/10 | 10/10 | +2 |
| doctor_selection average | 10/12 | 10/12 | 0 |
| summary fidelity avg | 1.0/2 | 1.5/2 | +0.5 |
| disagreement preservation avg | 0.8/2 | 1.7/2 | +0.9 |
| actionability avg | 1.2/2 | 1.5/2 | +0.3 |

## Trigger Baseline

| Case | Expected | Predicted | Result | Note |
|---|---:|---:|---:|---|
| `trigger-001` | false | false | 1 | Technical debugging is now clearly out of scope. |
| `trigger-002` | true | true | 1 | Strong fit. |
| `trigger-003` | true | true | 1 | Explicit `会诊`. |
| `trigger-004` | false | false | 1 | Low-value daily choice is explicitly excluded. |
| `trigger-005` | true | true | 1 | Clear decision problem. |
| `trigger-006` | true | true | 1 | Open discussion remains in scope. |
| `trigger-007` | false | false | 1 | Vertical execution task remains excluded. |
| `trigger-008` | true | true | 1 | Strong fit for clinic. |
| `trigger-009` | false | false | 1 | Factual query is explicitly excluded now. |
| `trigger-010` | true | true | 1 | Explicit named-doctor trigger. |
| `trigger-011` | false | false | 1 | Contract risk review is now correctly out of scope by default. |
| `trigger-012` | true | true | 1 | Strong fit for opinion review. |

Trigger takeaways:

- The new boundary section resolves the main over-triggering failure mode.
- Remaining risk is mostly implementation drift, not spec ambiguity.

## Routing Baseline

| Case | Expected | Predicted | Result | Note |
|---|---|---|---:|---|
| `routing-001` | 审视 | 审视 | 1 | Clear opinion review. |
| `routing-002` | 求助 | 求助 | 1 | Hybrid wording now correctly stays in help mode. |
| `routing-003` | 决策 | 决策 | 1 | Clear option selection. |
| `routing-004` | 开放 | 开放 | 1 | Topic discussion. |
| `routing-005` | 审视 | 审视 | 1 | Strong opinion review. |
| `routing-006` | 求助 | 求助 | 1 | New hybrid rule fixes this case. |
| `routing-007` | 决策 | 决策 | 1 | Concrete option comparison. |
| `routing-008` | 开放 | 开放 | 1 | Conceptual discussion. |
| `routing-009` | 审视 | 审视 | 1 | Explicit thesis plus self-doubt. |
| `routing-010` | 求助 | 求助 | 1 | Still correctly introspective. |

Routing takeaways:

- The explicit priority order removes the largest ambiguity from v0.
- The special rule around immature `A/B` framing is especially valuable.

## Doctor Selection Baseline

| Case | Score | Note |
|---|---:|---|
| `doctors-001` | 2 | Still strong. |
| `doctors-002` | 2 | Still strong. |
| `doctors-003` | 2 | Still strong. |
| `doctors-004` | 1 | Institutional critique is still not guaranteed enough by explicit doctor-selection rules. |
| `doctors-005` | 2 | Still strong. |
| `doctors-006` | 1 | Creator-economy cases still need clearer anti-flattery constraints. |

Doctor-selection takeaways:

- `v1` did not try to change this layer much, which is fine.
- The next improvement opportunity is to make doctor-selection constraints more operational.

## End-to-End Baseline

### `e2e-001`

- Summary fidelity: `2/2`
- Disagreement preservation: `2/2`
- Actionability: `1/2`
- Notes:
  - new disagreement rules should stop the host from forcing false synthesis
  - still somewhat vulnerable to generic prescriptions in审视 mode follow-up

### `e2e-002`

- Summary fidelity: `2/2`
- Disagreement preservation: `2/2`
- Actionability: `2/2`
- Notes:
  - decision-mode dedicated prescription format is a major improvement
  - much lower risk of collapsing value conflict into a fake consensus

### `e2e-003`

- Summary fidelity: `1/2`
- Disagreement preservation: `2/2`
- Actionability: `2/2`
- Notes:
  - better at preserving competing explanations
  - still depends on strong host summarization discipline

### `e2e-004`

- Summary fidelity: `1/2`
- Disagreement preservation: `1/2`
- Actionability: `1/2`
- Notes:
  - open-mode concept discussions remain decent
  - the summary can still drift toward over-neat synthesis if the host is lazy

### `e2e-005`

- Summary fidelity: `2/2`
- Disagreement preservation: `2/2`
- Actionability: `2/2`
- Notes:
  - named-doctor handling benefits from the new conditional confirmation rule
  - much less interaction friction than v0

### `e2e-006`

- Summary fidelity: `1/2`
- Disagreement preservation: `1/2`
- Actionability: `1/2`
- Notes:
  - the key improvement is that this should no longer enter clinic at all
  - residual low scores here reflect non-applicability rather than weak consultation quality

## What v1 Fixed

1. Broad trigger phrases no longer dominate activation.
2. Mixed `求助/决策` inputs are handled much more predictably.
3. Confirmation friction is now conditional instead of mandatory.
4. Host-side disagreement handling is much stronger.
5. Decision-mode prescriptions are now structurally aligned with the product's intent.

## Remaining Gaps

1. Doctor selection still relies on taste more than explicit constraints in some domains.
2. Open-mode summaries can still become too tidy.
3. The spec says the right thing more often now, but a future automated or live baseline should verify that actual runs obey it.

## Recommended v2 Priorities

1. Add explicit anti-redundancy rules for doctor selection.
2. Add stronger open-mode summary constraints.
3. Add multi-turn eval cases to test context compression and follow-up routing.
