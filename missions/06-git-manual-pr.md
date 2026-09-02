# Mission: Complete A Manual Pull Request Loop

## Outcome

You can make one bounded change manually, inspect it, verify it, commit it with
a Conventional Commit, publish it, and explain it in the passport pull request.

## Why This Matters

Agents and IDE buttons are safer after you understand the underlying branch,
working tree, staged diff, commit, remote branch, and review boundary.

## Before You Start

Git identity, GitHub authentication, and access to your personal exercise fork
must work. Do not use an AI agent for the implementation in this mission.

## Machine And Shell

**Your computer - PowerShell, zsh, or bash inside the passport repository.**
The Git commands below are the same on all three systems.

## Steps

1. Confirm that you are not on `main`:

```bash
git status --short --branch
```

2. Open `workspace/manual_task/README.md` and complete its manual task.
3. Inspect only the intended files:

```bash
git status --short
git diff -- workspace/manual_task
```

4. Run the fixture verification command documented in that workspace.
5. Stage only the intended files and inspect the staged diff:

```bash
git add -- workspace/manual_task/project-note.md evidence/git/manual-pr.md
git diff --cached --check
git diff --cached
```

6. Commit with a concise `type(scope): summary` subject. Use `test`, `fix`,
   `feat`, or `docs` only when it describes the actual change.
7. Push the branch and update the existing draft assessment pull request.

## Expected Result

The working tree contains only intentional changes, verification succeeds, the
commit subject explains the change, and the draft pull request shows the diff.

## Independent Verification

Run:

```bash
git log -1 --oneline
git status --short --branch
```

Compare the local commit with the pull request. Do not report a check as passed
unless you observed its result.

## Evidence To Submit

Complete `evidence/git/manual-pr.md` and the pull-request template. Do not paste
a full AI transcript, credential, unrelated repository history, or local
configuration.

## If Blocked

Do not use `git reset --hard`, broad deletion, or force push as a first repair.
Preserve `git status`, the current branch, and the diff, then use the
[first safe PR lab](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/first-safe-pr.md) recovery section or ask
for help through the non-secret dashboard issue form.

## Understand Before Accepting AI Output

This mission is deliberately manual. An agent may explain a Git concept but
must not perform the change, invent test output, or choose files to stage.

## Finish And Continue

The controller queues the required review automatically. After that
asynchronous review, Git is established as the manual baseline for optional
Python and AI-agent missions.
