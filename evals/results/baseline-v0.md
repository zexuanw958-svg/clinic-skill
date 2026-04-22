# Clinic Baseline v0

Date: 2026-04-22

Version under evaluation:

- `clinic/SKILL.md` at repository state before any v1 fixes
- baseline commit ancestry includes `76bb830`

Method:

- manual evaluation against the current skill specification
- this is a design-level baseline, not a live execution trace
- scores estimate the behavior implied by the current skill rules

## Summary

The current `clinic` design is strong at:

- defining a distinctive host role
- maintaining a broad and useful doctor roster
- encouraging adversarial or non-flattering doctor selection

The current design is weak at:

- trigger precision
- routing stability on mixed cases
- unnecessary confirmation friction
- preserving disagreement through the host summary and prescription

## Aggregate Scores

| Layer | Metric | Baseline |
|---|---|---:|
| trigger | accuracy | 8/12 |
| routing | accuracy | 8/10 |
| doctor_selection | average score | 10/12 |
| end_to_end | summary fidelity average | 1.0/2 |
| end_to_end | disagreement preservation average | 0.8/2 |
| end_to_end | actionability average | 1.2/2 |

## Trigger Baseline

| Case | Expected | Predicted | Result | Note |
|---|---:|---:|---:|---|
| `trigger-001` | false | true | 0 | Over-triggered by generic `帮我看看`. |
| `trigger-002` | true | true | 1 | Fits explicit trigger language and topic. |
| `trigger-003` | true | true | 1 | Explicit `会诊`. |
| `trigger-004` | false | true | 0 | Over-triggered by generic `帮我想想`. |
| `trigger-005` | true | true | 1 | Strong fit for clinic-style counseling. |
| `trigger-006` | true | true | 1 | Open discussion case fits. |
| `trigger-007` | false | false | 1 | Better routed to a vertical content skill. |
| `trigger-008` | true | true | 1 | Strong fit. |
| `trigger-009` | false | true | 0 | `我想问问` is too broad and catches factual queries. |
| `trigger-010` | true | true | 1 | Explicit named-doctor trigger. |
| `trigger-011` | false | true | 0 | Generic `帮我看看` risks swallowing legal review tasks. |
| `trigger-012` | true | true | 1 | Strong fit for viewpoint review. |

Trigger takeaways:

- Broad trigger phrases are the main source of precision loss.
- `clinic` is currently too likely to absorb routine assistant work.

## Routing Baseline

| Case | Expected | Predicted | Result | Note |
|---|---|---|---:|---|
| `routing-001` | 审视 | 审视 | 1 | Clear opinion review. |
| `routing-002` | 求助 | 决策 | 0 | Mixed wording may be pulled toward decision mode too early. |
| `routing-003` | 决策 | 决策 | 1 | Clear option selection. |
| `routing-004` | 开放 | 开放 | 1 | Topic discussion. |
| `routing-005` | 审视 | 审视 | 1 | Strong opinion review. |
| `routing-006` | 求助 | 决策 | 0 | Current rules do not define priority for hybrid cases. |
| `routing-007` | 决策 | 决策 | 1 | Concrete option comparison. |
| `routing-008` | 开放 | 开放 | 1 | Conceptual discussion. |
| `routing-009` | 审视 | 审视 | 1 | Explicit thesis plus self-doubt. |
| `routing-010` | 求助 | 求助 | 1 | Mostly introspective rather than option-based. |

Routing takeaways:

- The four modes are conceptually sound.
- The current spec lacks conflict-resolution priority for hybrid inputs.

## Doctor Selection Baseline

| Case | Score | Note |
|---|---:|---|
| `doctors-001` | 2 | Spec strongly supports a skeptical and risk-aware roster. |
| `doctors-002` | 2 | Decision + entrepreneurship + risk is well covered. |
| `doctors-003` | 2 | Good balance of psychology, stoicism, and real-world hierarchy. |
| `doctors-004` | 1 | Product and attention angles are easy; institutional critique is less guaranteed. |
| `doctors-005` | 2 | Strong conceptual fit. |
| `doctors-006` | 1 | Risk of selecting only creator-economy optimists without enough tension. |

Doctor-selection takeaways:

- The roster quality is already a strength.
- The main weakness is not doctor inventory but the lack of stronger selection constraints.

## End-to-End Baseline

### `e2e-001`

- Summary fidelity: `1/2`
- Disagreement preservation: `1/2`
- Actionability: `1/2`
- Notes:
  - likely to over-confirm roster before doing useful work
  - likely to summarize into a neat conclusion instead of preserving conceptual disagreement

### `e2e-002`

- Summary fidelity: `1/2`
- Disagreement preservation: `0/2`
- Actionability: `1/2`
- Notes:
  - strong risk that the host will compress value conflict and loss aversion into one blended answer
  - current prescription format pushes toward a synthesized decision

### `e2e-003`

- Summary fidelity: `1/2`
- Disagreement preservation: `1/2`
- Actionability: `2/2`
- Notes:
  - likely to produce useful next steps
  - still vulnerable to flattening competing interpretations

### `e2e-004`

- Summary fidelity: `1/2`
- Disagreement preservation: `1/2`
- Actionability: `1/2`
- Notes:
  - concept discussion is supported
  - summary may still drift toward one "correct" definition

### `e2e-005`

- Summary fidelity: `1/2`
- Disagreement preservation: `1/2`
- Actionability: `2/2`
- Notes:
  - explicit named doctors help
  - current flow still inserts avoidable confirmation friction

### `e2e-006`

- Summary fidelity: `1/2`
- Disagreement preservation: `1/2`
- Actionability: `0/2`
- Notes:
  - if routing is governed by broad trigger phrases alone, this can enter the clinic incorrectly
  - failure here is mostly inherited from trigger precision

## Main Problems Confirmed By Baseline

1. Broad trigger phrases reduce precision.
2. Hybrid inputs can drift between `求助` and `决策`.
3. The mandatory roster-confirmation step adds friction.
4. The host is encouraged to over-synthesize disagreement.
5. The prescription format is too eager to output one neat action plan in decision cases.

## Recommended v1 Priorities

1. Narrow trigger conditions.
2. Add explicit routing priority for hybrid cases.
3. Change roster confirmation from default behavior to conditional behavior.
4. Preserve disagreement more explicitly in the host summary.
5. Split decision-mode prescription into:
   - decision framework
   - validation step
   - optional recommendation
