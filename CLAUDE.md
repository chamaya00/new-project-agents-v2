# Project context

## What this is

A scratch repository for exercising the agent-factory setup end to end -
provisioning, the gate, the containment rules, and agent runs - against a
repository that contains nothing else to get in the way.

## Stack

None yet, and that is deliberate: the thing under test is the arrangement, not
a product. There is no language, framework, data store, or hosting here. When
something real lands, name it here and fix the Commands section below in the
same commit.

## Commands

- Install: nothing to install.
- Dev: nothing to run.
- Gate: `.github/workflows/ci.yml` runs a handful of `test -f` and `test -d`
  checks that assert the scaffolding is intact. That is the whole gate today.

CI is on the reusable workflow's `commands` path rather than its Node path,
because the Node path fails a named `package.json` script that is not there
rather than skipping it, and there is no `package.json`. The header comment in
`.github/workflows/ci.yml` says what to restore when a stack arrives:
`checks: 'typecheck,lint,test,build'`, the four scripts every other project
provisioned from this factory runs.

Whatever the gate runs, the rule is the same one. If a check is renamed here,
rename it in `.github/workflows/ci.yml` in the same commit, and re-point the
branch protection rule in the same sitting - the job name is the string
protection matches on, so a renamed check that no longer reports blocks every
merge instead of gating them.

## How work moves

Objectives become issues labelled `objective`. The orchestrator splits one into
2-5 child issues, each with acceptance criteria and one role label. A human
labels a child `agent:queued` when it is ready to run. Nothing runs itself.

Labels: `objective`, `agent:queued`, `agent:running`, `agent:review`,
`agent:blocked`, `needs-decomposition`, `role:researcher`, `role:designer`,
`role:engineer`.

## Standing rules

Acceptance criteria before work starts. Tests before merge. An ADR in
`docs/decisions/` for any schema or dependency change, in the same diff.

Three failed attempts on one issue means the issue was scoped wrong. Stop and
ask for decomposition rather than trying a fourth time.

Never edit `.github/workflows/`, `CODEOWNERS`, or anything under a plugin
directory. If the work seems to need it, say so in a comment and stop.

## Memory

Lessons specific to this repository live in `.claude/memory/<role>.md`, one file
per role, 40 lines each. They are proposed in a pull request, never written
silently. A lesson that has graduated into a test, a lint rule, or a type gets
deleted - the check enforces it now, and the sentence is competing for attention
with the lessons nothing enforces yet.
