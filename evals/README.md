# Clinic Eval Suite

This directory defines the first evaluation suite for `clinic`.

The suite is intentionally hybrid:

- External benchmarks provide non-self-referential anchors.
- Custom `clinic` cases measure the real orchestration behavior of the skill.

## Scope

The suite evaluates four layers:

1. `trigger`: should `clinic` activate at all
2. `routing`: which mode should the host choose
3. `doctor_selection`: which doctors should be selected and why
4. `end_to_end`: whether the full consultation is useful without flattening disagreement

## External References

These are not mirrored into the repository. They are used as reference sources when expanding the suite:

- `GAIR/AgencyBench`
  - Use for rubric design, long-horizon task framing, and deliverable-based scoring.
- `lingfengzhou/PersonaEval`
  - Use for persona separation and role-identification style checks.
- `awsaf49/persona-chat`
  - Use as a secondary reference for persona consistency.

## Files

- `rubric.md`
  - Shared scoring rules
- `clinic/trigger.jsonl`
  - Triggering ground truth
- `clinic/routing.jsonl`
  - Mode routing ground truth
- `clinic/doctor_selection.jsonl`
  - Doctor selection expectations
- `clinic/end_to_end.jsonl`
  - Full-chain consultation eval set

## Evaluation Philosophy

We are not trying to prove the skill is "smart".

We are trying to answer narrower questions:

- Does it activate only when appropriate?
- Does it classify the user's need consistently?
- Does it pick sufficiently distinct doctors?
- Does it preserve disagreement rather than collapsing it into bland synthesis?
- Does it produce actionable output when action is appropriate?

## Recommended Process

1. Freeze the current `clinic/SKILL.md` version.
2. Run a baseline pass on all four files.
3. Record results in a spreadsheet or future `results/` directory.
4. Iterate the skill.
5. Re-run the same suite before adding new cases.

## Notes

- This first version is optimized for manual or semi-manual evaluation.
- The JSONL schema is designed so an automated judge can be added later.
