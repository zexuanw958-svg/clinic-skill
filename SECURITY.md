# Security Policy

`clinic-skill` is a prompt-and-workflow repository. It does not run a server,
process payments, or store remote user data by itself. The main safety risks
are prompt behavior, local memory handling, and accidental inclusion of
sensitive information in examples or evaluation traces.

## Supported Versions

The `main` branch is the supported development line until the project starts
publishing tagged releases.

## What To Report

Please open a private security advisory or contact the maintainer if you find:

- a prompt path that encourages disclosure of secrets, credentials, or private
  personal data
- a memory update rule that stores sensitive information without explicit user
  confirmation
- an evaluation trace that includes private data
- a workflow instruction that could cause unsafe medical, legal, financial, or
  security advice to be presented as authoritative

## What Not To Report

Please use normal issues for:

- unclear wording
- weak doctor selection
- missing eval coverage
- examples that are unconvincing but not sensitive

## Maintainer Response

For security-sensitive reports, the maintainer will:

1. acknowledge the report when seen
2. reproduce and scope the issue
3. remove exposed sensitive content if needed
4. patch the relevant prompt, memory, or eval rule
5. document the fix in `CHANGELOG.md`

Because this is currently a small maintainer-led project, response times are
best effort rather than SLA-backed.
