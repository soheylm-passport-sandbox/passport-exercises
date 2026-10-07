# Mission: Use A Safe Agent Loop After The Manual Baseline

## Outcome

Authorize one small fictional file edit, then verify its scope and policy
meaning independently. No agent transcript is uploaded.

## Concept

An AI coding agent can request actions that change files or services; an
ordinary chat window only supplies text unless separately given tools. The
person who authorizes an action remains responsible for its scope and result.
Verify the final diff and tests required by the task. This exercise checks the
plan and protected file, rather than running a program test suite. This practice folder contains
an unsafe storage plan and scope-canary.txt, a protected file that must not change.

## Learning Challenge

Read the unsafe plan first. What needs correcting, and what must stay untouched?
Ask for a plan, compare it with your own reasoning, then authorize only the
reviewed edit. Read the actual diff before accepting any claimed success.

## Worked Example

<details>
<summary>Review one proposed action</summary>

Check the file, intended correction, forbidden actions and independent
verification. A correct sentence does not excuse another file changing.
Keep each storage role/location together in a sentence or bullet and remove
contradictions. The shared local/remote rules accept documented phrasing variants,
not arbitrary contradictory plans. Check the canary and diff yourself.

</details>

## Common Trap

Approve only the bounded plan and inspect the actual changed files.

## Your Action

Give an agent one small fictional task, review its plan and diff, then verify the result yourself.

**Follow these steps in order.** Read the fictional plan manually, then review and authorize one file edit. Keep the protected file and unrelated folders unchanged.

**New to text commands?** A command is a line of text that tells a
computer to do one task. A terminal is the text application in which a
shell reads that command. Open PowerShell on Windows or the application
named Terminal on macOS or Linux. The application starts the correct
shell automatically; do not install a separate Bash or zsh application. Read
[Terminal and command basics](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/core/command-line-basics.md)
before continuing if these words are new.

### 1. Prepare the AI practice files

**Where:** The laptop or desktop in front of you

Press Prepare practice folder in this step and run the displayed enter-folder command. In the editor you configured in the previous AI mission, open the workspace/agent_task folder inside this practice repository. Check the editor title or file tree before opening an agent chat.

**Expected:** README.md, storage-plan.md, and scope-canary.txt are visible.

**Continue when:** Read the task yourself before opening an agent session.

**If not:** Do not use a real project as a substitute.

### 2. Understand the task first

**Where:** The laptop or desktop in front of you

Read the unsafe fictional plan before asking the agent. Identify the four corrections yourself and name the only editable file. scope-canary.txt is a protected file whose unchanged content checks that boundary.

**Expected:** You can describe the intended P:, D:, C:, and heavy-compute rules.

**Continue when:** Start one new agent session.

**If not:** Return to the systems mission before delegating the task.

### 3. Ask for a plan without allowing changes

**Where:** The laptop or desktop in front of you

Start a new agent chat in workspace/agent_task and paste the prompt below. Keep the agent in read-only or planning mode if the editor offers that choice. Do not approve any edit or command yet.

**Paste this into the agent:**

```text
Read README.md, storage-plan.md, and scope-canary.txt in this folder. Explain the four errors in storage-plan.md and propose the smallest correction. Do not edit files, run commands, install software, or access files outside this folder. Your plan must edit only storage-plan.md and leave scope-canary.txt unchanged.
```

**Expected:** The agent's plan names one editable file and the stated constraints.

**Continue when:** Reject any out-of-scope suggestion, then authorize only the stated edit.

**If not:** Stop the session and start a new one with the missing boundary stated explicitly.

### 4. Authorize only the one-file edit

**Where:** The laptop or desktop in front of you

Compare the proposed plan with your four corrections. Use the existing narrow authorization below only if it stays within the named file and permissions. Reject extra edits, installs, permission changes, destructive commands and real-file access. Do not enable auto-approval.

**Paste this into the agent:**

```text
Apply the reviewed plan. Edit only storage-plan.md. Do not edit scope-canary.txt or README.md, run terminal commands, install software, change permissions, or access files outside this folder. Stop after the edit and summarize exactly what changed.
```

**Expected:** Only the intended file edit is authorized.

**Continue when:** Let the one-file edit finish.

**If not:** Stop the agent; inspect repository state before continuing.

### 5. Inspect the changed paths

**Where:** The laptop or desktop in front of you

Use Git independently of the agent to list changed files.

**Open PowerShell on your Windows computer, then run:**

```powershell
git status --short -- workspace/agent_task
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
git status --short -- workspace/agent_task
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
git status --short -- workspace/agent_task
```

**Expected:** Only workspace/agent_task/storage-plan.md is modified.

**Continue when:** Read the complete diff.

**If not:** Do not continue until every extra change is understood and safely removed.

### 6. Review the complete diff

**Where:** The laptop or desktop in front of you

Check that the plan makes P: durable, D: temporary, C: unsuitable for project data, and Euler or approved compute the place for heavy work. Write each policy correction as its own sentence or bullet, connecting the location with its role. Keep the compute task and its destination together; their order does not matter. Remove contradictory claims left from the unsafe plan. Review the actual diff independently; an agent summary is not verification.

**Open PowerShell on your Windows computer, then run:**

```powershell
git diff -- workspace/agent_task
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
git diff -- workspace/agent_task
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
git diff -- workspace/agent_task
```

**Expected:** The diff is limited to the four requested policy corrections.

**Continue when:** Run Check my work yourself.

**If not:** Correct the one allowed file manually or start a new chat with the missing constraint stated explicitly.

### 7. Check the result

**Where:** This web page in your browser

Return to this page and press Check my work. The automatic check confirms the changed file, the unchanged protected file, and the required storage statements.

**Expected:** The changed-file, protected-file, and storage-rule checks pass.

**Continue when:** Submit the mission once.

**If not:** Read the named check and its recovery message. Review that statement and any contradictory claim in storage-plan.md, then check again. Keep your existing work; do not reset the Passport or submit an agent transcript.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. This check runs on your computer and
checks only the practical work in this lesson. A score of 80% is required, and every
safety-critical question must be correct. Failed attempts provide targeted
feedback and can be retried without penalty.

## If Blocked

Start a new agent thread for the same specific task if context has become inconsistent. Return to
the clean baseline when edits spread outside the practice files. Use the
[manual versus agent lab](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/labs/manual-vs-agent.md) for recovery.

Useful references:

- [Manual Vs Agent](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/labs/manual-vs-agent.md)
- [Agents And Interfaces](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/ai/agents-and-interfaces.md)
- [Data and AI policy](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/policy/data-and-ai.md)

## Understand Before Accepting AI Output

You must understand the changed behavior, tests, files, commands, data sent,
service used, and likely cost. Passing output without this explanation is not a
pass.

## Finish And Continue

When **Check my work** passes, use **Submit lesson** once. The launcher
publishes only this lesson's generated submission after private information is excluded. Continue when the
progress page shows the automatic GitHub result as passed; a check on your computer alone is not a pass.
