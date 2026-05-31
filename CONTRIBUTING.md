# Contributing

Thanks for considering a contribution to `clinic-skill`.

This project is a reusable skill framework for multi-perspective reasoning.
Good contributions usually improve one of four things:

- routing quality: when `clinic` should or should not activate
- doctor selection: whether the selected perspectives have useful tension
- host synthesis: whether disagreement is preserved without becoming messy
- evaluation quality: whether the behavior is falsifiable and repeatable

## Contribution Types

### Good first contributions

- Add a negative trigger case to `evals/clinic/trigger.jsonl`.
- Add a borderline routing case to `evals/clinic/routing.jsonl`.
- Improve wording in `docs/examples.md` or `evals/rubric.md`.
- Report a live output where the host flattened disagreement or picked
  redundant doctors.

### Larger contributions

- Add a new doctor only if the perspective has a clear framework difference
  from existing doctors.
- Expand the live eval protocol with a repeatable runner or fixed case pack.
- Improve the memory update protocol while keeping it auditable and opt-in.

## Development Workflow

1. Open or find an issue that describes the behavior you want to change.
2. Make the smallest change that improves the behavior.
3. Add or update an eval case that would have caught the problem.
4. Run through the relevant manual eval path in `evals/README.md`.
5. Open a pull request and describe the behavior change, not only the file diff.

## Pull Request Checklist

- [ ] The change has a clear user-visible reason.
- [ ] The change does not turn `clinic` into a generic assistant.
- [ ] The change preserves useful disagreement instead of forcing consensus.
- [ ] Relevant eval cases or examples were added or updated.
- [ ] The README, docs, or changelog were updated if the behavior changed.

## Doctor Design Rules

Doctors are not style masks. A doctor should contribute a distinct model of
judgment, not just a recognizable voice.

Before adding a doctor, document:

- what kind of problem the doctor is good at
- which existing doctors they overlap with
- what they challenge that others do not
- one example where selecting this doctor changes the diagnosis

## Maintainer Review Standard

Maintainers should prefer changes that make failures more visible over changes
that make the skill sound more impressive. A rejected or revised contribution
is not a judgment on the idea; it usually means the behavior was not yet
observable enough to maintain.
