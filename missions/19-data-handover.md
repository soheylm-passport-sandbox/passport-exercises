# Mission: Create A Recoverable Project Handover

## Outcome

Create a handover that another authorized researcher can use without your
personal account or computer.

## Concept

A project handover is the documented transfer of ownership, access, locations, and knowledge before a person leaves. It identifies the authoritative code and data, explains how to reproduce important results, confirms that successors can access them, and names what may be cleaned up.

A directory full of unexplained files is not a handover, even if the files still exist.

## Worked Example

Another authorized person could locate, verify, rerun, and safely retire the fictional project without hidden personal dependencies.

Check these points:

- **What is a successful handover?** An authorized successor can locate, verify, rerun, and maintain or retire the work.
- **How are credentials handled in a handover?** Rotate or provision access through approved channels; never place secrets in the document.

## Common Trap

Listing a folder without naming its owner, code revision, environment, access boundary, or retention decision.

## Your Action

Complete the synthetic handover file so another authorized person can locate, verify, rerun, and retire the project.

**Follow these steps in order.** Use fictional values only. Never enter a real private path, person, credential, unpublished detail, or participant information.

### 1. Prepare the handover fixture

**Where:** Your computer

Press Prepare practice folder, enter it, and open workspace/handover/project-handover.md.

**Expected:** The synthetic template is open in the practice repository.

**Continue when:** Replace every placeholder with fictional information.

**If not:** Do not use a real project document for this exercise.

### 2. Record current and successor ownership

**Where:** Your computer

Replace the two ownership placeholders with fictional role names. Use the example below so this public exercise contains no real person.

**Put this in the named Markdown file:**

```markdown
Current owner: Example Researcher

Authorized successor: Example Project Maintainer
```

**Expected:** Both ownership fields contain non-placeholder values.

**Continue when:** Record code and environment identity.

**If not:** Do not claim a handover without an authorized successor.

### 3. Record reproducible code

**Where:** Your computer

Replace the revision and environment placeholders with the fictional values below. A real handover would use the exact commit produced by git rev-parse HEAD and the committed environment file.

**Put this in the named Markdown file:**

```markdown
Revision: 0123456789abcdef0123456789abcdef01234567

Environment definition: environment.yml at the recorded revision
```

**Expected:** The revision has exactly 40 hexadecimal characters and the environment field is complete.

**Continue when:** Record authoritative and temporary data locations.

**If not:** Replace labels such as latest or current with an exact revision.

### 4. Record data locations and cleanup

**Where:** Your computer

Replace both data placeholders with the fictional paths below. They demonstrate a durable project location and a temporary copy without exposing a real lab path.

**Put this in the named Markdown file:**

```markdown
Authoritative location: P:\ExampleSupervisor\example-user\synthetic-project

Temporary locations to remove: D:\example-user\synthetic-project-cache
```

**Expected:** The durable and temporary roles are unambiguous.

**Continue when:** Add a verification command and expected result.

**If not:** Resolve which copy is authoritative before continuing.

### 5. Record how to verify the project

**Where:** Your computer

Replace the verification placeholders with the harmless fictional command and exact expected result below.

**Put this in the named Markdown file:**

```markdown
Verification command: python -m unittest discover -s tests -v

Expected result: All 12 synthetic tests pass.
```

**Expected:** The successor can tell success from failure.

**Continue when:** Assign access, retention, and deletion owners.

**If not:** Do not write works on my machine as verification.

### 6. Record access and retention actions

**Where:** Your computer

Use fictional role names for access and retention. Replace YYYY-MM-DD with a real future date for this exercise, such as a date 30 days from today. Then replace the Known Limitations placeholder with one fictional unresolved limitation.

**Put this in the named Markdown file:**

```markdown
Access owner: Example Project Maintainer

Retention owner: Example Data Steward

Temporary-copy deletion date: YYYY-MM-DD

Unresolved risk or limitation: Synthetic rerun has not been tested on a second operating system.
```

**Expected:** Both owners, a valid future date, and one fictional limitation replace all placeholders.

**Continue when:** Review the completed file.

**If not:** Do not delete or revoke anything without a named owner and date.

### 7. Check scope and placeholders

**Where:** Your computer

Confirm that only the synthetic handover file changed, every placeholder is gone, and no real information was inserted.

**Run on Windows - PowerShell:**

```powershell
git diff -- workspace/handover/project-handover.md
```

**Run on macOS - zsh:**

```zsh
git diff -- workspace/handover/project-handover.md
```

**Run on Linux - Bash:**

```bash
git diff -- workspace/handover/project-handover.md
```

**Expected:** The diff is complete, fictional, and limited to one file.

**Continue when:** Run Check my work.

**If not:** Remove real or extra information before submitting.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. The local verifier checks only the
mission activity above. A score of 80% is required, and every
safety-critical question must be correct. Failed attempts provide targeted
feedback and can be retried without penalty.

## If Blocked

Record missing ownership or retention decisions explicitly rather than
inventing them. Use the
[project handover lab](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/project-handover.md) and ask the
supervisor to assign the next owner.

Useful references:

- [Project Handover](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/project-handover.md)
- [Data Steward](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/tracks/data-steward.md)

## Understand Before Accepting AI Output

An agent may format an inventory but cannot certify that paths exist, access
works, results reproduce, or disposal is approved. A person verifies each item.

## Finish And Continue

When **Check my work** passes, use **Submit mission** once. The launcher
publishes only this mission's generated, sanitized submission. Continue when the
dashboard shows the trusted result; a local check alone is not a pass.
