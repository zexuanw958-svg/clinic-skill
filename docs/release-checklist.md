# Release Checklist

Use this checklist before publishing a tagged release.

## 1. Scope The Release

- [ ] Write a one-sentence release goal.
- [ ] List user-visible behavior changes.
- [ ] List eval or documentation changes.
- [ ] Confirm whether memory behavior changed.

## 2. Run Evaluation

- [ ] Review `evals/README.md`.
- [ ] Run or manually check the affected JSONL suites.
- [ ] For behavior changes, record a live trace under `evals/results/`.
- [ ] Check for host failure regressions:
  - fake consensus
  - over-summary
  - ignored latest-turn evidence
  - mode flattening
  - generic action-list output

## 3. Review Safety And Privacy

- [ ] Confirm new examples contain no private user data.
- [ ] Confirm memory updates remain explicit and opt-in.
- [ ] Confirm advice boundaries are clear for medical, legal, financial, and
  security-adjacent topics.

## 4. Update Project Metadata

- [ ] Update `CHANGELOG.md`.
- [ ] Update `README.md` if entry points or behavior changed.
- [ ] Update `ROADMAP.md` if priorities changed.
- [ ] Tag the release.

## 5. Publish Notes

Release notes should include:

- what changed
- why it matters
- which evals were checked
- known limitations
