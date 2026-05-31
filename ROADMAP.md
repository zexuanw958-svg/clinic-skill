# Roadmap

This roadmap tracks the work needed to make `clinic-skill` easier to reuse,
evaluate, and maintain as an open-source project.

## 0.1.x - Public Maintenance Baseline

- Add OSS metadata: license, changelog, contribution guide, issue templates,
  pull request template, release checklist, and security policy.
- Publish an explicit `v0.1.0` tag that points to the first public baseline.
- Keep raw live output traces discoverable from the README.

## 0.2.x - Evaluation Harness

- Add a lightweight eval runner for the JSONL cases.
- Add a stable score sheet format for trigger, routing, doctor selection,
  end-to-end, multi-turn, and host failure cases.
- Add a small fixed live eval pack that can be repeated across model versions.
- Document pass/fail thresholds for release candidates.

## 0.3.x - Installation And Runtime Portability

- Document installation paths for Codex, Claude, and compatible local skill
  runtimes.
- Add a minimal example workspace that shows how `clinic`, `doctors`, `evals`,
  and `memory` fit together.
- Add compatibility notes for environments that do not support nested skills.

## 0.4.x - Doctor Registry Quality

- Add per-doctor quality notes: best-use cases, overlap risks, and anti-patterns.
- Add doctor selection regression cases for common redundancy failures.
- Split high-overlap doctors into clearer roles or document when not to select
  them together.

## Long-Term

- Support community-contributed doctor packs without weakening the host rules.
- Add automated checks for sensitive data in eval traces.
- Publish periodic live eval reports when major model or host-rule changes land.
