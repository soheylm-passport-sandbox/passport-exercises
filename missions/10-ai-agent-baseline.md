# Mission: Use A Safe Agent Loop After The Manual Baseline

## Outcome

You can bound an agent task, control context and commands, review the diff,
verify the result personally, and reject a plausible but inferior suggestion.

## Why This Matters

An agent can read files, edit code, execute commands, and publish changes. It is
not merely a model or chatbot, and fluent output does not transfer
responsibility away from the account owner.

## Before You Start

Complete the manual Git task and choose the approved AI access route. Read
[agents, models, providers and interfaces](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/ai/agents-and-interfaces.md)
and confirm the training content is permitted for the selected service.

## Machine And Shell

**Your computer - approved editor agent plus PowerShell, zsh, or bash.** Use the
separate agent fixture in `workspace/agent_task`; do not repeat the manual task.

## Steps

Give the agent this structure, adapted to the fixture:

```text
Goal: complete the bounded behavior described in the agent fixture.
Context: inspect only the fixture source, tests, and README first.
Constraints: do not edit outside the fixture, add dependencies, use secrets,
submit remote jobs, or claim checks ran without output.
Verification: run the fixture test and inspect the final diff.
Output: explain the cause, smallest change, commands run, and limitations.
```

Use the loop: explore, plan, constrain, edit, review, verify, record. Stop the
agent if it requests credentials, unrelated files, protected data, or broader
commands than the task requires.

## Expected Result

The bounded task passes, changes remain inside the allowed fixture, and you can
explain one suggestion you accepted and one you rejected or revised.

## Independent Verification

Run the relevant tests yourself after the agent stops. Inspect `git status`,
`git diff --check`, and the complete diff. Compare actual output with the
agent's summary.

## Evidence To Submit

Complete `evidence/ai/agent-baseline.md`. Do not include an API key, full chat
transcript, account screenshot, unpublished data, or billing details.

## If Blocked

Start a new bounded agent thread if context has become inconsistent. Return to
the clean baseline when edits spread outside the fixture. Use the
[manual versus agent lab](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/manual-vs-agent.md) for recovery.

## Understand Before Accepting AI Output

You must understand the changed behavior, tests, files, commands, data sent,
service used, and likely cost. Passing output without this explanation is not a
pass.

## Finish And Continue

Commit only the reviewed fixture and evidence. The final AI-track capstone
reviews this reasoning; the agent cannot approve its own work.
