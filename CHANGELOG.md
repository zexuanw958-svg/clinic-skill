# Changelog

All notable changes to `clinic-skill` are documented here.

This project uses human-readable release notes instead of generated changelog
entries because the important changes are usually workflow and evaluation
changes, not only code diffs.

## Unreleased

- No changes yet.

## 0.1.0 - 2026-05-31

### Added

- Initial public `clinic` skill for multi-perspective consultation.
- Host workflow for trigger detection, routing, doctor selection, consultation
  synthesis, and prescription output.
- Doctor registry with philosophy, decision, psychology, entrepreneurship,
  AI, education, content, product, and social-strategy perspectives.
- Evaluation suite covering trigger, routing, doctor selection, end-to-end
  behavior, multi-turn behavior, and host failure cases.
- Live evaluation protocol and first raw live comparison trace:
  `evals/results/live-2026-04-26.md`.
- Auditable local memory templates under `memory/`.
- Installation and runtime notes for Codex, Claude, and compatible local skill
  environments.
- Open-source maintenance metadata: license, contribution guide, security
  policy, roadmap, release checklist, issue templates, and pull request template.
- Explicit maintainer workflow documentation for triage, evaluation, release,
  and documentation updates.

### Changed

- README now prioritizes raw evaluation output over polished examples.
- Host rules were tightened to avoid fake consensus, over-summary, premature
  closure, and mode flattening.
- README now exposes project signals, maintenance status, and repository map
  links for first-time users and reviewers.
