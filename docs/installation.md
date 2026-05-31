# Installation And Runtime Notes

This guide explains how to install and smoke-test `clinic-skill` in local skill
runtimes such as Codex, Claude, or compatible agent environments.

`clinic-skill` is a prompt-and-workflow repository. There is no package install
step, build step, server, or database. Installation means placing the skill
files where your agent runtime can discover them.

## Repository Layout

```text
clinic-skill/
  clinic/
    SKILL.md                # main host skill
  doctors/
    <doctor>/SKILL.md       # referenced perspective skills
  evals/
    clinic/*.jsonl          # regression/eval cases
    results/*.md            # recorded baseline and live eval traces
  memory/
    *.md                    # optional local auditable memory templates
```

The main entry point is `clinic/SKILL.md`. The `doctors/` directory contains the
perspective skills the host can select. The `evals/` directory is for maintainers
and does not need to be loaded at runtime unless you are testing behavior. The
`memory/` directory is optional and should remain local, explicit, and auditable.

## Option A: Use The Repository Directly

Clone the repository:

```bash
git clone https://github.com/zexuanw958-svg/clinic-skill.git
cd clinic-skill
```

Point your skill runtime at the repository root, or at the specific `clinic/`
entry point if your runtime loads one skill at a time.

Use this option when your runtime supports relative references or when you want
to keep the full repository, docs, evals, and memory templates together.

## Option B: Copy Into A Skill Directory

If your runtime uses a fixed skill directory, copy the relevant folders:

```bash
mkdir -p /path/to/skills/clinic-skill
cp -R clinic doctors memory /path/to/skills/clinic-skill/
```

Keep `clinic/` and `doctors/` together. The host skill expects the doctor skills
to be available by name. If your runtime cannot load nested or adjacent skills,
install the doctor skills individually and keep their names unchanged.

## Codex Notes

For Codex-style skill runtimes:

1. Place this repository under a configured skill root.
2. Ensure `clinic/SKILL.md` is discoverable as the `clinic` skill.
3. Ensure doctor skills under `doctors/*/SKILL.md` are also discoverable.
4. Start with an explicit trigger such as `/clinic` or `/诊所`.

Minimal smoke test:

```text
/clinic 我是不是把勤奋当成了思考的替代品？
```

Expected behavior:

- The host should enter consultation mode.
- It should select 2-3 relevant doctors rather than answer as a generic
  assistant.
- It should preserve competing explanations instead of forcing a single
  conclusion.

## Claude Notes

For Claude-style skill directories:

1. Copy `clinic/` into the skill directory.
2. Copy each `doctors/<name>/` directory into the same skill root if the runtime
   resolves skills by name.
3. Keep the doctor directory names unchanged, for example
   `munger-perspective`, `feynman-perspective`, and `adler-perspective`.
4. Invoke the skill explicitly if automatic triggering is not available.

If your runtime does not support one skill invoking or referencing another, use
`clinic/SKILL.md` as the host spec and manually load the doctor skills that are
relevant to your test.

## Memory Setup

The files under `memory/` are templates for local, auditable memory. They are not
required for the first run.

Use memory only when:

- the user explicitly wants longitudinal memory
- the memory files stay local and inspectable
- each write is proposed and confirmed before it is saved

Do not store secrets, credentials, identity documents, private medical/legal/
financial conclusions, or anything the user asked not to retain.

## Evaluating A Local Install

After the smoke test, compare the output against the goals in:

- `evals/README.md`
- `evals/rubric.md`
- `docs/examples.md`

Common install or runtime problems:

- The host answers directly without selecting doctors.
- All selected doctors come from the same frame and produce redundant advice.
- The final diagnosis flattens disagreement into a bland consensus.
- The runtime cannot discover doctor skills because only `clinic/` was copied.

If you hit one of these, open an issue with the input, the runtime, and the
observed output.
