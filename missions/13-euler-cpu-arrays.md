# Mission: Cap And Calculate Euler Job Arrays

## Outcome

Review the local fictional array file, limit simultaneous tasks and make its
log names traceable. This exercise never submits an array.

## Concept

An array runs similar tasks from one script. The range sets total tasks; the
number after % is the concurrency cap, or maximum allowed to run together.
Each running task reserves its own resources. The cap limits simultaneous
demand, not the amount of work and not your other jobs. A distinct log name
keeps each task's output separate, so it can be traced and does not overwrite another.

## Learning Challenge

The unsafe file allows 100 tasks without a cap. Before opening the supplied
repair, identify the unbounded setting and predict what a cap of one changes.
This guided assessment requires exactly --array=0-9%1 and the shown log form.
Do not paste file directives into a terminal or run sbatch.

## Worked Example

<details>
<summary>Check the separate concurrency calculation</summary>

With cap three, two CPUs and 4 GiB per CPU, at most three tasks reserve
3 x 2 = 6 CPUs and 3 x 2 x 4 = 24 GiB together. Add other running jobs before
any future approved submission. %A labels the parent array and %a its task
index; %j is also a distinct running job ID, but does not directly label both.

</details>

## Common Trap

Confusing total tasks with running tasks, or omitting other arrays and jobs.
A fixed shared filename can collide; %j does not inherently cause a collision.

## Your Action

Correct the fictional Slurm array practice file, add a concurrency cap, and make every task log name unique.

**Follow these steps in order.** The supplied file is deliberately unsafe. Edit it locally and never submit it to Euler.

**New to text commands?** A command is a line of text that tells a
computer to do one task. A terminal is the text application in which a
shell reads that command. Open PowerShell on Windows or the application
named Terminal on macOS or Linux. The application starts the correct
shell automatically; do not install a separate Bash or zsh application. Read
[Terminal and command basics](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/core/command-line-basics.md)
before continuing if these words are new.

### 1. Understand an array and its concurrency cap

**Where:** This web page in your browser

Use the range and cap distinction above when reading the fictional file. Before opening a repair, predict the total task count and how many could run together.

- [Open the job-array lab](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/labs/euler-job-arrays.md)

**Expected:** You can distinguish total task count from the maximum running at once.

**Continue when:** Open the deliberately unsafe local practice file.

**If not:** Do not submit a real array until you can calculate its simultaneous resource total.

### 2. Prepare the array practice file

**Where:** The laptop or desktop in front of you

Press Prepare practice folder, enter it, and open workspace/slurm/array_job.slurm.txt.

**Expected:** The unsafe practice file is open in the separate practice repository.

**Continue when:** Inspect it without submitting.

**If not:** Do not create your own replacement script or use Euler for this exercise.

### 3. Inspect the cap and log names

**Where:** The laptop or desktop in front of you

Read the array and two log directives in the unsafe local file. Which setting bounds simultaneous demand? Which filename placeholders identify the parent and index? Compare your reasoning with the repair steps afterwards; do not submit this file.

**Expected:** You can explain the missing concurrency cap and why parent/index labels make array logs easier to trace.

**Continue when:** Edit only the required directives.

**If not:** Review the array and log-name explanation before editing.

### 4. Add a small concurrency cap

**Where:** The laptop or desktop in front of you

Replace the unsafe array directive with the exact line below. It creates ten tasks, numbered 0 through 9, and allows at most one to run at a time.

<details>
<summary>Show the required cap-one repair</summary>

**Put this in the named Bash file:**

```bash
#SBATCH --array=0-9%1
```

</details>

**Expected:** The directive is exactly --array=0-9%1.

**Continue when:** Make the logs unique.

**If not:** Do not use an uncapped range or a zero cap.

### 5. Use parent and task IDs in logs

**Where:** The laptop or desktop in front of you

Replace both log directives with the two exact lines below. %A is the parent job ID and %a is the array task index.

<details>
<summary>Show the required parent/index log lines</summary>

**Put this in the named Bash file:**

```bash
#SBATCH --output=logs/%x_%A_%a.out
#SBATCH --error=logs/%x_%A_%a.err
```

</details>

**Expected:** Each array task has a distinct output and error path.

**Continue when:** Inspect the local diff.

**If not:** Correct both settings before pressing Check my work.

### 6. Calculate the concurrent resource total

**Where:** The laptop or desktop in front of you

The practice repair uses ten tasks with cap one. For the separate question, first calculate the simultaneous demand of cap three with two CPUs and 4 GiB per CPU, then compare with the model above. Add other active jobs: this cap limits only this array. No real array is submitted.

**Expected:** You can calculate the maximum simultaneous tasks, CPUs, system memory, and GPUs before submission.

**Continue when:** Review the edited practice file.

**If not:** Keep the cap at one until the per-task and combined totals are known.

### 7. Review the edited file

**Where:** The laptop or desktop in front of you

Confirm that only the fictional practice file changed and that no command submitted it.

**Open PowerShell on your Windows computer, then run:**

```powershell
git diff -- workspace/slurm/array_job.slurm.txt
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
git diff -- workspace/slurm/array_job.slurm.txt
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
git diff -- workspace/slurm/array_job.slurm.txt
```

**Expected:** The diff changes only the array cap and the two log names.

**Continue when:** Run Check my work.

**If not:** Remove every unrelated change before continuing.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. This check runs on your computer and
checks only the practical work in this lesson. A score of 100% is required, and every
safety-critical question must be correct. Failed attempts provide targeted
feedback and can be retried without penalty.

## Learning Check

### Practise

Try an answer before opening the explanation. These questions are for
practice; they do not affect your progress.

1. Another job already uses two CPUs and 6 GiB. An array has eight tasks, cap two, and each task requests one CPU and 3 GiB. What maximum combined reservation should you review?

   - Eight CPUs and 24 GiB, ignoring the already-running job.
   - Four CPUs and 12 GiB: two array tasks plus the existing job.
   - Two CPUs and 6 GiB, because the cap covers every job.

<details class="learning-explanation">
<summary>See an explanation</summary>

Two running array tasks reserve 2 CPUs and 6 GiB. Add the existing 2 CPUs and 6 GiB: 4 CPUs and 12 GiB total. The eight tasks determine total work, not simultaneous demand; the cap does not constrain other jobs.

</details>

## If Blocked

Reduce the cap to `%1` and validate a representative input. If many tasks fail
identically, cancel the array and debug one task. Use the
[job arrays lab](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/labs/euler-job-arrays.md) for dependent or
heterogeneous workloads.

Useful references:

- [Euler job arrays](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/labs/euler-job-arrays.md)
- [Slurm reference](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/euler/slurm.md)

## Understand Before Accepting AI Output

Calculate concurrency yourself and include other submissions. A personal or
lab limit is a ceiling, not a target for an agent to consume.

## Finish And Continue

When **Check my work** passes, use **Submit lesson** once. The launcher
publishes only this lesson's generated submission after private information is excluded. Continue when the
progress page shows the automatic GitHub result as passed; a check on your computer alone is not a pass.
