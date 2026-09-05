# Mission: Use A Safe Agent Loop After The Manual Baseline

## Outcome

Use an AI coding agent on one fictional file, review every proposed action,
then verify the diff and result yourself.

## Concept

An agent can read files, edit code, execute commands, and publish changes. The
person who authorizes its actions remains responsible for them.

## Worked Example

The agent changes only the allowed file. The canary remains unchanged, the
verifier passes, and the learner reviews the result without submitting a chat
transcript.

Check these points:

- **What is a safe agent task?** One specific outcome with named files, constraints, and verification.
- **Who verifies the final diff and tests?** You do, even if the agent reports success.

## Common Trap

Granting a broad task, sharing protected data, or accepting a claimed test result without checking the diff and rerunning it.

## Your Action

Give an agent one small fictional task, review its plan and diff, then verify the result yourself.

**Follow these steps in order.** The agent may edit only storage-plan.md. The canary file, repository settings, dependencies, and real data are outside scope.

### 1. Prepare the agent fixture

**Where:** Your computer

Press Prepare practice folder in this step and run the displayed enter-folder command. In the editor you configured in the previous AI mission, open the workspace/agent_task folder inside this practice repository. Check the editor title or file tree before opening an agent chat.

**Expected:** README.md, storage-plan.md, and scope-canary.txt are visible.

**Continue when:** Read the task yourself before opening an agent session.

**If not:** Do not use a real project as a substitute.

### 2. Understand the task first

**Where:** Your computer

Read the fixture README and unsafe storage plan. Identify the four required corrections and the one file the agent may edit.

**Expected:** You can describe the intended P:, D:, C:, and heavy-compute rules.

**Continue when:** Start one new agent session.

**If not:** Return to the systems mission before delegating the task.

### 3. Ask for a plan without allowing changes

**Where:** Your computer

Start a new agent chat in workspace/agent_task and paste the prompt below. Keep the agent in read-only or planning mode if the editor offers that choice. Do not approve any edit or command yet.

**Paste this into the agent:**

```text
Read README.md, storage-plan.md, and scope-canary.txt in this folder. Explain the four errors in storage-plan.md and propose the smallest correction. Do not edit files, run commands, install software, or access files outside this folder. Your plan must edit only storage-plan.md and leave scope-canary.txt unchanged.
```

**Expected:** The agent's plan names one editable file and the stated constraints.

**Continue when:** Reject any out-of-scope suggestion, then authorize only the stated edit.

**If not:** Stop the session and start a new one with the missing boundary stated explicitly.

### 4. Authorize only the one-file edit

**Where:** Your computer

If the plan is correct, paste the authorization below. Do not enable auto-approval. Reject installs, permission changes, access to real files, destructive commands, and edits outside storage-plan.md.

**Paste this into the agent:**

```text
Apply the reviewed plan. Edit only storage-plan.md. Do not edit scope-canary.txt or README.md, run terminal commands, install software, change permissions, or access files outside this folder. Stop after the edit and summarize exactly what changed.
```

**Expected:** Only the intended file edit is authorized.

**Continue when:** Let the one-file edit finish.

**If not:** Stop the agent; inspect repository state before continuing.

### 5. Inspect the changed paths

**Where:** Your computer

Use Git independently of the agent to list changed files.

**Run on Windows - PowerShell:**

```powershell
git status --short -- workspace/agent_task
```

**Run on macOS - zsh:**

```zsh
git status --short -- workspace/agent_task
```

**Run on Linux - Bash:**

```bash
git status --short -- workspace/agent_task
```

**Expected:** Only workspace/agent_task/storage-plan.md is modified.

**Continue when:** Read the complete diff.

**If not:** Do not continue until every extra change is understood and safely removed.

### 6. Review the complete diff

**Where:** Your computer

Check that the plan makes P: durable, D: temporary, C: unsuitable for project data, and Euler or approved compute the place for heavy work.

**Run on Windows - PowerShell:**

```powershell
git diff -- workspace/agent_task
```

**Run on macOS - zsh:**

```zsh
git diff -- workspace/agent_task
```

**Run on Linux - Bash:**

```bash
git diff -- workspace/agent_task
```

**Expected:** The diff is limited to the four requested policy corrections.

**Continue when:** Run Check my work yourself.

**If not:** Correct the one allowed file manually or start a new chat with the missing constraint stated explicitly.

### 7. Run the Passport verifier

**Where:** This browser

Return to this page and press Check my work. The verifier checks the changed path, exact canary, and required storage statements.

**Expected:** The changed-path, canary, and storage-rule checks pass.

**Continue when:** Submit the mission once.

**If not:** Use the named failed check; do not submit an agent transcript or claim.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. The local verifier checks only the
mission activity above. A score of 80% is required, and every
safety-critical question must be correct. Failed attempts provide targeted
feedback and can be retried without penalty.

## If Blocked

Start a new agent thread for the same specific task if context has become inconsistent. Return to
the clean baseline when edits spread outside the fixture. Use the
[manual versus agent lab](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/manual-vs-agent.md) for recovery.

Useful references:

- [Manual Vs Agent](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/manual-vs-agent.md)
- [Agents And Interfaces](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/ai/agents-and-interfaces.md)
- [Data and AI policy](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/policy/data-and-ai.md)

## Understand Before Accepting AI Output

You must understand the changed behavior, tests, files, commands, data sent,
service used, and likely cost. Passing output without this explanation is not a
pass.

## Finish And Continue

When **Check my work** passes, use **Submit mission** once. The launcher
publishes only this mission's generated, sanitized submission. Continue when the
dashboard shows the trusted result; a local check alone is not a pass.
