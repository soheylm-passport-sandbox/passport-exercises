# Mission: Cap And Calculate Euler Job Arrays

## Outcome

Fix a Slurm job array, which runs many similar tasks from one script, so simultaneous tasks are capped and each task writes a distinct log.

## Concept

A Slurm job array submits many similar tasks from one script. The array range sets the total number of tasks; the value after `%` limits how many may run at the same time. This concurrency cap controls simultaneous demand, not total work.

Every task also needs a distinct log name, and the combined CPU, memory, and GPU request must be calculated before submission.

## Worked Example

The verifier accepts exactly ten tasks with at most one running at a time and
distinct logs for every task. No command submits the fixture to Euler.

Check these points:

- **What does %4 mean in --array=0-31%4?** At most four array tasks may run concurrently.
- **Which placeholders distinguish array logs?** %A for the parent job and %a for the task index.

## Common Trap

Submitting a large array before adding %N, or using %j so tasks overwrite or obscure one another.

## Your Action

Correct the synthetic Slurm array file, add a concurrency cap, and make every task log name unique.

**Follow these steps in order.** The supplied file is deliberately unsafe. Edit it locally and never submit it to Euler.

### 1. Understand an array and its concurrency cap

**Where:** This browser

A job array creates many similar Slurm tasks from one script. The range sets total tasks; %N limits simultaneous tasks. Each task still reserves its own CPU, memory, GPU, and time and needs a distinct log name.

- [Open the job-array lab](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/euler-job-arrays.md)

**Expected:** You can distinguish total task count from the maximum running at once.

**Continue when:** Open the deliberately unsafe local fixture.

**If not:** Do not submit a real array until you can calculate its simultaneous resource total.

### 2. Prepare the array fixture

**Where:** Your computer

Press Prepare practice folder, enter it, and open workspace/slurm/array_job.slurm.txt.

**Expected:** The unsafe fixture is open in the separate practice repository.

**Continue when:** Inspect it without submitting.

**If not:** Do not create your own replacement script or use Euler for this exercise.

### 3. Identify both defects

**Where:** Your computer

Read the array and log directives. The fixture allows 100 tasks without a concurrency cap and uses log names that do not identify each array task.

**Expected:** You can explain why uncapped tasks and colliding logs are unsafe.

**Continue when:** Edit only the required directives.

**If not:** Review the array and log-name explanation before editing.

### 4. Add a small concurrency cap

**Where:** Your computer

Replace the unsafe array directive with the exact line below. It creates ten tasks, numbered 0 through 9, and allows at most one to run at a time.

**Put this in the named Bash file:**

```bash
#SBATCH --array=0-9%1
```

**Expected:** The directive is exactly --array=0-9%1.

**Continue when:** Make the logs unique.

**If not:** Do not use an uncapped range or a zero cap.

### 5. Use parent and task IDs in logs

**Where:** Your computer

Replace both log directives with the two exact lines below. %A is the parent job ID and %a is the array task index.

**Put this in the named Bash file:**

```bash
#SBATCH --output=logs/%x_%A_%a.out
#SBATCH --error=logs/%x_%A_%a.err
```

**Expected:** Each array task has a distinct output and error path.

**Continue when:** Inspect the local diff.

**If not:** Correct both directives before running the verifier.

### 6. Calculate the concurrent resource total

**Where:** Your computer

Before using any array in a real project, multiply the cap by each task's CPU, memory, and GPU request. For --array=0-9%3 with 2 CPUs and 4 GiB per CPU, three tasks can run together: 3 x 2 = 6 CPUs and 3 x 2 x 4 GiB = 24 GiB. Then add your other active jobs and arrays; the cap applies only to this array.

**Expected:** You can calculate the maximum simultaneous tasks, CPUs, system memory, and GPUs before submission.

**Continue when:** Review the edited fixture.

**If not:** Keep the cap at one until the per-task and combined totals are known.

### 7. Review the edited file

**Where:** Your computer

Confirm that only the synthetic fixture changed and that no command submitted it.

**Run on Windows - PowerShell:**

```powershell
git diff -- workspace/slurm/array_job.slurm.txt
```

**Run on macOS - zsh:**

```zsh
git diff -- workspace/slurm/array_job.slurm.txt
```

**Run on Linux - Bash:**

```bash
git diff -- workspace/slurm/array_job.slurm.txt
```

**Expected:** The diff changes only the array cap and the two log names.

**Continue when:** Run Check my work.

**If not:** Remove every unrelated change before continuing.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. The local verifier checks only the
mission activity above. A score of 100% is required, and every
safety-critical question must be correct. Failed attempts provide targeted
feedback and can be retried without penalty.

## If Blocked

Reduce the cap to `%1` and validate a representative input. If many tasks fail
identically, cancel the array and debug one task. Use the
[job arrays lab](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/euler-job-arrays.md) for dependent or
heterogeneous workloads.

Useful references:

- [Euler job arrays](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/euler-job-arrays.md)
- [Slurm reference](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/euler/slurm.md)

## Understand Before Accepting AI Output

Calculate concurrency yourself and include other submissions. A personal or
lab limit is a ceiling, not a target for an agent to consume.

## Finish And Continue

When **Check my work** passes, use **Submit mission** once. The launcher
publishes only this mission's generated, sanitized submission. Continue when the
dashboard shows the trusted result; a local check alone is not a pass.
