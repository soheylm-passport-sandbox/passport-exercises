# Mission: Design Safe Shared Data Collaboration

## Outcome

Decide how two fictional collaborators work without overwriting shared inputs.
This is a design exercise; grant or repair no real permissions.

## Concept

Code and data are shared differently. Each editor has a separate Git clone.
Its Git working tree holds that person's branch, staged and uncommitted changes.
Shared data instead has a named information owner and approved location.

Mira analyses beam measurements; Leo reviews her report.

| Area | Mira | Leo | Boundary |
| --- | --- | --- | --- |
| Main input | Read | Read only if approved for review | Neither replaces it |
| Mira's run output | Write | Read the agreed report | Separate outputs for concurrent runs |
| Code | Own clone | Own clone if editing | Reviewed changes through GitHub |

Permissions state who may read or change files. An access-control list (ACL)
expresses detailed permissions. A readable folder is not automatically writable.

## Learning Challenge

Leo cannot edit the main input. Is that a defect if his task is to review the
report? Decide the necessary boundary before opening the explanation.

## Worked Example

<details>
<summary>Why read and write roles differ</summary>

The reviewer needs the agreed report and provenance, not permission to replace
measurements. Diagnose owner, group, ACL and intended boundary before a narrow
authorized repair. Preserve conflicting outputs for the owner to resolve;
never use shared credentials or make everything writable.

</details>

## Common Trap

Keep separate Git working trees. Diagnose a failed permission before asking
for a narrow owner-approved repair.

## Your Action

Reason about the fictional collaborators and answer six decisions. Change no real access or shared folder.

**Follow these steps in order.** Use only Mira and Leo's fictional collaboration. Decide the required boundaries; do not apply real permissions or share credentials.

### 1. Name the dataset owner

**Where:** This web page in your browser

The fictional owner approves access and retention. Mira analyses the input; Leo reviews the report. Neither needs permission to replace the main input simply to do those tasks.

**Expected:** One accountable information owner is named.

**Continue when:** List the collaborators' actual tasks.

**If not:** Do not grant access until ownership is clear.

### 2. Grant only needed access

**Where:** This web page in your browser

Decide the read/write access each role needs. An access-control list expresses permissions, not authorization to broaden them. Change no actual permissions.

**Expected:** No collaborator receives broader access than needed.

**Continue when:** Define the write boundary.

**If not:** Reduce the proposed permission or obtain owner approval.

### 3. Define where writes occur

**Where:** This web page in your browser

Keep the main input read-only to analysts and reviewers. Each analysis writes its own run output. A write boundary names exactly which folders each person/program may change.

**Expected:** Concurrent work cannot silently overwrite the main approved inputs.

**Continue when:** Separate code collaboration from data sharing.

**If not:** Make source files read-only or use clearly versioned copies before collaboration starts.

### 4. Use separate Git clones

**Where:** This web page in your browser

Each editor uses their own Git working tree: a checkout with its own branch, staged and uncommitted changes. Reviewed changes travel through GitHub; shared data does not require a shared writable checkout.

**Expected:** Git ownership and file permissions cannot collide inside one shared checkout.

**Continue when:** Define names and record where generated data came from and how it was produced.

**If not:** Move the repository out of the shared writable data directory.

### 5. Define conflict and recovery rules

**Where:** This web page in your browser

If reports conflict, preserve both copies and identifiers, then ask the owner which is authoritative. Do not overwrite one merely because its timestamp is newer.

**Expected:** A collaborator can recover without guessing which copy is the main approved one.

**Continue when:** Complete the structured questions.

**If not:** Do not start shared writes until the main approved copy is named.

### 6. Complete the collaboration plan

**Where:** This web page in your browser

Answer six scenario decisions. A private plan may support discussion, but this assessment submits choices and creates no access.

**Expected:** The plan uses minimum access and separate code clones.

**Continue when:** Run Check my work.

**If not:** Use the feedback to correct the unsafe decision.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. This check runs on your computer and
checks only the practical work in this lesson. A score of 80% is required, and every
safety-critical question must be correct. Failed attempts provide targeted
feedback and can be retried without penalty.

## If Blocked

Do not guess numeric group IDs or apply broad recursive commands. Ask the
storage owner to inspect the smallest affected directory. Use
[Euler storage](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/euler/storage.md) for the maintained
setgid/default ACL procedure when Euler is the approved system.

Useful references:

- [Data Placement](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/labs/data-placement.md)
- [Euler storage](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/euler/storage.md)
- [NAS guide](https://github.com/IDEALLab/onboarding-IT/blob/main/onboarding_IT_guides/nas_ideal.md)

## Understand Before Accepting AI Output

An agent must not apply recursive permission changes based only on a pasted
path. Verify system, owner, group, inheritance, existing contents, and rollback
before any real change.

## Finish And Continue

When **Check my work** passes, use **Submit lesson** once. The launcher
publishes only this lesson's generated submission after private information is excluded. Continue when the
progress page shows the automatic GitHub result as passed; a check on your computer alone is not a pass.
