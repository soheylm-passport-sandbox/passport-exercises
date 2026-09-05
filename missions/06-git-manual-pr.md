# Mission: Complete A Manual Pull Request Loop

## Outcome

Use Git manually to edit and review one file, record a Conventional Commit, send the branch to GitHub, and open a draft pull request for review.

## Concept

A Git change moves through a visible sequence. The working tree contains the files you are editing. A branch keeps the work separate. Staging selects the reviewed changes for one commit; the commit records them with an author and message. Pushing sends that branch to GitHub. A pull request, or PR, asks others to review the branch before it is merged.

Complete this sequence manually once before delegating it to an IDE button or AI agent.

## Worked Example

The personal practice PR contains only the intended file, a Conventional Commit, and an honest verification record.

Check these points:

- **Which PR do you create manually in this mission?** The personal practice PR shown by the mission.
- **What must happen immediately before committing?** Inspect git diff --cached and confirm every staged change.

## Common Trap

Using the background transport PR as the exercise, or staging every file with git add . before reviewing status.

## Your Action

Make one small manual change, review both diffs, create a Conventional Commit, push it, and open a draft pull request.

**Follow these steps in order.** Do this mission without an AI agent. Use the exact practice folder and commands prepared by the Passport.

### 1. Learn the manual Git change path

**Where:** This browser

Edit a file in the working tree, inspect the diff, stage only the reviewed file, record it as a commit, push the branch to GitHub, then open a pull request for review. A draft pull request is visible but explicitly not ready to merge.

- [Read the beginner Git workflow](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/onboarding_IT_guides/git_workflow.md)

**Expected:** You can name the order: edit, diff, stage, commit, push, pull request.

**Continue when:** Open the prepared practice folder.

**If not:** Do not use an IDE button or agent to skip a step you cannot yet identify.

### 2. Open the practice folder

**Where:** Your computer

Press Prepare practice folder in this step. Run the displayed enter-folder command, then keep this terminal in that folder.

**Expected:** The terminal is at the root of the practice repository.

**Continue when:** Continue to the baseline inspection.

**If not:** Do not clone again; rerun the preparation or gh passport doctor.

### 3. Inspect before editing

**Where:** Your computer

Read workspace/manual_task/README.md and project-note.md. Confirm the branch is the practice branch and the working tree has no unexpected change.

**Run on Windows - PowerShell:**

```powershell
git status --short --branch
Get-Content -LiteralPath workspace/manual_task/README.md
Get-Content -LiteralPath workspace/manual_task/project-note.md
```

**Run on macOS - zsh:**

```zsh
git status --short --branch
sed -n '1,160p' workspace/manual_task/README.md
sed -n '1,160p' workspace/manual_task/project-note.md
```

**Run on Linux - Bash:**

```bash
git status --short --branch
sed -n '1,160p' workspace/manual_task/README.md
sed -n '1,160p' workspace/manual_task/project-note.md
```

**Expected:** The practice branch is shown with no unexpected file below it.

**Continue when:** Open the practice folder in a plain-text code editor.

**If not:** Stop and understand every existing change before touching a file.

### 4. Open the exact practice folder in an editor

**Where:** Your computer

Use a plain-text code editor you already trust. If you do not have one, install VS Code from the official link, open it, choose File > Open Folder, and select the exact practice-folder path shown by the Passport. Do not enable an AI agent for this mission.

- [Download VS Code](https://code.visualstudio.com/download)

**Expected:** The editor file tree contains workspace/manual_task/README.md and project-note.md from the practice folder.

**Continue when:** Open project-note.md and make the requested edit.

**If not:** Return to the folder path shown by Prepare practice folder; do not open the handbook or a research repository instead.

### 5. Make the requested edit

**Where:** Your computer

Open workspace/manual_task/project-note.md in the editor file tree. Add the exact block shown below at the end of the file, then save it. Do not edit another file.

**Put this in the named Markdown file:**

```markdown
## Verification

The staged diff must be reviewed before publishing.
```

**Expected:** Only project-note.md contains the intended text change.

**Continue when:** Inspect the unstaged diff.

**If not:** Undo only the mistaken lines in your editor; do not reset the repository.

### 6. Review the unstaged diff

**Where:** Your computer

Check the changed path and read every added or removed line before staging.

**Run on Windows - PowerShell:**

```powershell
git status --short
git diff -- workspace/manual_task/project-note.md
```

**Run on macOS - zsh:**

```zsh
git status --short
git diff -- workspace/manual_task/project-note.md
```

**Run on Linux - Bash:**

```bash
git status --short
git diff -- workspace/manual_task/project-note.md
```

**Expected:** The diff contains one intended file and no credential or private information.

**Continue when:** Stage that exact file.

**If not:** Correct the file before staging anything.

### 7. Stage one file

**Where:** Your computer

Add only the reviewed project note, then check whitespace and inspect the staged diff.

**Run on Windows - PowerShell:**

```powershell
git add -- workspace/manual_task/project-note.md
git diff --cached --check
git diff --cached
```

**Run on macOS - zsh:**

```zsh
git add -- workspace/manual_task/project-note.md
git diff --cached --check
git diff --cached
```

**Run on Linux - Bash:**

```bash
git add -- workspace/manual_task/project-note.md
git diff --cached --check
git diff --cached
```

**Expected:** The staged diff contains only the reviewed note and the whitespace check is silent.

**Continue when:** Create the commit.

**If not:** Use git restore --staged on the unintended path, correct it, and review again.

### 8. Create a Conventional Commit

**Where:** Your computer

Use the exact commit command prepared by the Passport. The form is type(scope): concise summary; the scope names the affected area.

**Run on Windows - PowerShell:**

```powershell
git commit -m "docs(practice): explain staged diff review"
```

**Run on macOS - zsh:**

```zsh
git commit -m "docs(practice): explain staged diff review"
```

**Run on Linux - Bash:**

```bash
git commit -m "docs(practice): explain staged diff review"
```

**Expected:** Git creates one commit with the shown subject.

**Continue when:** Push the current practice branch.

**If not:** Read the first Git error; do not use force or skip hooks.

### 9. Push and open a draft pull request

**Where:** Your computer

Run the exact push and gh pr create commands displayed by Prepare practice folder. Keep the pull request in draft and do not merge it.

**Expected:** GitHub shows one open draft pull request from your practice branch to main.

**Continue when:** Open the PR and inspect Files changed.

**If not:** Do not create a second PR; inspect the branch and existing PR with gh pr status.

### 10. Review what GitHub received

**Where:** Your computer

Open the current branch's draft PR, then confirm the author, source branch, target branch, commit subject, and single changed file. Leave the PR open as learning evidence.

**Run on Windows - PowerShell:**

```powershell
gh pr view --web
```

**Run on macOS - zsh:**

```zsh
gh pr view --web
```

**Run on Linux - Bash:**

```bash
gh pr view --web
```

**Expected:** The GitHub diff matches the staged diff you reviewed locally.

**Continue when:** Return to the Passport and run Check my work.

**If not:** Correct the same branch and push again; do not merge or delete evidence.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. The local verifier checks only the
mission activity above. A score of 80% is required, and every
safety-critical question must be correct. Failed attempts provide targeted
feedback and can be retried without penalty.

## If Blocked

Do not use `git reset --hard`, broad deletion, or force push as a first repair.
Preserve `git status`, the current branch, and the diff, then use the
[first safe PR lab](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/first-safe-pr.md) recovery section or ask
for help through the non-secret dashboard issue form.

Useful references:

- [First Safe Pr](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/first-safe-pr.md)
- [Git workflow](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/onboarding_IT_guides/git_workflow.md)

## Understand Before Accepting AI Output

This mission is deliberately manual. An agent may explain a Git concept but
must not perform the change, invent test output, or choose files to stage.

## Finish And Continue

When **Check my work** passes, use **Submit mission** once. The launcher
publishes only this mission's generated, sanitized submission. Continue when the
dashboard shows the trusted result; a local check alone is not a pass.
