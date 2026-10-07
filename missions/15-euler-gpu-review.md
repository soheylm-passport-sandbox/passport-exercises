# Mission: Review A One-GPU Euler Plan

## Outcome

Correct a fictional graphics processor (GPU) request locally. No GPU allocation or live computation
is required; the file is public practice material only.

## Concept

A GPU is an accelerator for compatible operations, not every program.
A Slurm GPU request reserves that shared accelerator; it does not grant the
entire compute node.

| Resource | Meaning in this review |
| --- | --- |
| GPU count | One explicitly supported accelerator |
| CPU count | Supporting work; more CPUs do not establish faster GPU code |
| System RAM | CPU count times memory per CPU, distinct from GPU memory |
| GPU memory | Capacity on the accelerator; not Slurm system RAM |
| Time | Bounded reservation, later justified by representative measurements |

The account identifies the approved lab computing share, es_fuge. A partition is a group of
compute nodes; the teaching request leaves selection to Euler. Current dated
lab hardware policy remains in the reference.

## Learning Challenge

The unsafe file requests four GPUs without evidence of scaling. Spot one
unsupported reservation before opening the repair. The accepted teaching
profile is bounded, but its maximum values are ceilings, not targets.

## Worked Example

<details>
<summary>What the current script checker accepts</summary>

One supported named GPU, es_fuge, no forced partition, 1..16 CPUs, at most
64 GiB total system memory, positive time up to four hours and per-job logs.
The supplied profile is compatible with this review. Real workloads need their
own measured CPU, memory and time; passing this fixture proves neither runtime
compatibility nor efficient GPU use.

</details>

## Common Trap

Increasing GPUs because the dataset is large, or submitting the unsafe practice
file. Keep this exercise a local text review.

## Your Action

Repair the unsafe one-GPU Slurm practice file locally and apply the lab starter limits without submitting it.

**Follow these steps in order.** This is a review exercise. Do not run sbatch, the Slurm submission command. Use one explicit GPU model and the es_fuge lab computing share. A Slurm partition is a named group of compute nodes; this starter request lets Euler choose it instead of forcing one.

**New to text commands?** A command is a line of text that tells a
computer to do one task. A terminal is the text application in which a
shell reads that command. Open PowerShell on Windows or the application
named Terminal on macOS or Linux. The application starts the correct
shell automatically; do not install a separate Bash or zsh application. Read
[Terminal and command basics](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/core/command-line-basics.md)
before continuing if these words are new.

### 1. Understand what a GPU request reserves

**Where:** This web page in your browser

Compare the unsafe request with the resource distinctions above. A GPU request reserves an accelerator even when software waits for CPU or data; reservation does not prove useful GPU work.

- [Open the Euler GPU policy](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/policy/euler-share.md)

**Expected:** You can explain why the starter plan requests one explicit GPU plus measured supporting resources.

**Continue when:** Review the fictional GPU practice file.

**If not:** Do not request multiple GPUs from dataset size or assumption alone.

### 2. Prepare the GPU practice file

**Where:** The laptop or desktop in front of you

Press Prepare practice folder, enter it, and open workspace/slurm/gpu_job.slurm.txt.

**Expected:** The deliberately unsafe GPU script is open locally.

**Continue when:** Identify every unsafe directive.

**If not:** Do not copy the unsafe practice file into a real project.

### 3. Identify the unsafe request

**Where:** The laptop or desktop in front of you

Read the deliberately unsafe local file. Choose one request that is unsupported by a program needing one GPU, and explain why before opening the model. Do not submit it to Euler.

**Expected:** You can explain why the script is not a one-GPU starter.

**Continue when:** Choose one supported model.

**If not:** Review the Euler GPU reference before editing.

### 4. Choose one GPU model

**Where:** The laptop or desktop in front of you

Keep the existing documented teaching default rtx_4090:1. The supported fallback and special-purpose profile are in the optional GPU reference; do not choose hardware simply to bypass a queue. This lesson changes no current hardware or entitlement policy.

- [Only if needed: fallback and special-purpose GPU profile](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/euler/slurm.md#rtx-pro-6000-special-purpose-profile)

**Expected:** Exactly one explicit GPU model and one GPU are requested.

**Continue when:** Set the companion resources.

**If not:** Do not submit duplicate jobs for several GPU models.

### 5. Set the lab starter profile

**Where:** The laptop or desktop in front of you

Keep this a local text edit. Remove the forced partition and old --mem line. Predict the correction, then inspect the compatible teaching model. Its limits are an assessment profile, not optimized settings for an unknown research workload.

<details>
<summary>Show the compatible one-GPU teaching profile</summary>

**Put this in the named Bash file:**

<!-- passport-snippet:euler-gpu-4090-starter -->
```bash
#SBATCH --account=es_fuge
#SBATCH --gpus=rtx_4090:1
#SBATCH --cpus-per-task=16
#SBATCH --mem-per-cpu=3G
```
<!-- /passport-snippet:euler-gpu-4090-starter -->

</details>

**Expected:** The script uses es_fuge, one supported GPU, no partition, at most 16 CPUs, no more than 64 GiB total memory, and at most 04:00:00.

**Continue when:** Add unique output and error logs.

**If not:** Reduce the request or explain a measured reason before any live submission.

### 6. Add output and error logs

**Where:** The laptop or desktop in front of you

Add the time and log settings below. %x expands to the job name and %j to its job ID. Create the logs directory only when this script is later used in a real project; do not submit this exercise practice file.

**Put this in the named Bash file:**

```bash
#SBATCH --time=04:00:00
#SBATCH --output=logs/%x_%j.out
#SBATCH --error=logs/%x_%j.err
```

**Expected:** Both output and error directives are present and unique per job.

**Continue when:** Review the complete local diff.

**If not:** Do not rely on default Slurm output names for this starter.

### 7. Review without submitting

**Where:** The laptop or desktop in front of you

Inspect only the fictional GPU practice file. Confirm that no sbatch command was run.

**Open PowerShell on your Windows computer, then run:**

```powershell
git diff -- workspace/slurm/gpu_job.slurm.txt
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
git diff -- workspace/slurm/gpu_job.slurm.txt
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
git diff -- workspace/slurm/gpu_job.slurm.txt
```

**Expected:** The diff contains one explicit one-GPU starter profile and no unrelated change.

**Continue when:** Run Check my work.

**If not:** Correct the practice file locally; live testing is a separate deliberate action.

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

1. One GPU is reserved, but the program spends most time waiting for slow input reads. What is the next useful investigation?

   - Reserve a second GPU immediately.
   - Inspect data locality and the input pipeline before changing GPU count.
   - Request the whole node because a reservation guarantees utilization.

<details class="learning-explanation">
<summary>See an explanation</summary>

Waiting for data is not evidence of GPU scaling. Inspect where and how inputs are read, using the approved storage workflow. Cancel an unnecessary real allocation safely; do setup and log review without retaining an idle GPU.

</details>

## If Blocked

Use the RTX 4090 review baseline. Do not submit duplicate jobs for multiple GPU
types or select RTX PRO 6000 merely to bypass a queue. Escalate distributed
training, unusual memory, or CUDA compatibility to the supervisor.

Useful references:

- [Euler GPU review](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/labs/euler-gpu-review.md)
- [Euler GPU track](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/tracks/euler-gpu.md)
- [Slurm reference](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/euler/slurm.md)
- [IDEAL Lab Euler share policy](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/policy/euler-share.md)

## Understand Before Accepting AI Output

Verify that program operations, not only CUDA detection, use the GPU. You must
explain every requested resource and why adding GPUs may not help a CPU-bound
pipeline.

## Finish And Continue

When **Check my work** passes, use **Submit lesson** once. The launcher
publishes only this lesson's generated submission after private information is excluded. Continue when the
progress page shows the automatic GitHub result as passed; a check on your computer alone is not a pass.
