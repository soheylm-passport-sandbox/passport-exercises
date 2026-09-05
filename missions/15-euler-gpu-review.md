# Mission: Review A One-GPU Euler Plan

## Outcome

Review a Slurm script that reserves one GPU accelerator on Euler, then set an explicit model, CPU, memory, time, account, and log plan without submitting it.

## Concept

A GPU is an accelerator used only by software written to perform GPU operations. Requesting a GPU reserves it even when the program is waiting on CPU, data, or configuration. One Slurm GPU request normally allocates one accelerator on a shared compute node, not the whole physical node.

Start with one supported GPU and measured CPU, memory, and time. Use more GPUs only after a representative test proves that the program scales.

## Worked Example

The verifier accepts one named GPU, no forced partition, at most 16 CPUs, at
most 64 GiB total system memory, at most four hours, and distinct logs.

Check these points:

- **Which account provides the documented lab GPU access?** The approved es_fuge share.
- **What should a one-GPU starter request do?** Request one named GPU and explicit CPU, memory, and time limits.

## Common Trap

Assuming GPUs are on the public share, requesting all node CPUs for one GPU, or submitting the review fixture accidentally.

## Your Action

Repair the unsafe one-GPU Slurm fixture locally and apply the lab starter limits without submitting it.

**Follow these steps in order.** This is a review exercise. Do not run sbatch. Use one explicit GPU model and the es_fuge account.

### 1. Understand what a GPU request reserves

**Where:** This browser

A GPU accelerates only compatible code. A Slurm request such as rtx_4090:1 reserves one accelerator on a compute node; it does not prove that the program uses it efficiently and does not grant the whole node. CPU, memory, time, logs, and the project account are requested separately.

- [Open the Euler GPU policy](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/policy/euler-share.md)

**Expected:** You can explain why the starter plan requests one explicit GPU plus measured supporting resources.

**Continue when:** Review the synthetic GPU fixture.

**If not:** Do not request multiple GPUs from dataset size or assumption alone.

### 2. Prepare the GPU fixture

**Where:** Your computer

Press Prepare practice folder, enter it, and open workspace/slurm/gpu_job.slurm.txt.

**Expected:** The deliberately unsafe GPU script is open locally.

**Continue when:** Identify every unsafe directive.

**If not:** Do not copy the unsafe fixture into a real project.

### 3. Identify the unsafe request

**Where:** Your computer

Find the public account, forced partition, four-GPU request, 64 CPUs, 500 GiB memory, 48-hour time, and missing log directives.

**Expected:** You can explain why the script is not a one-GPU starter.

**Continue when:** Choose one supported model.

**If not:** Review the Euler GPU reference before editing.

### 4. Choose one GPU model

**Where:** Your computer

Use rtx_4090:1 by default. Use rtx_3090:1 when a 4090 is unavailable. Use pro_6000:1 only for a tested compatible workload that needs its capability.

**Expected:** Exactly one explicit GPU model and one GPU are requested.

**Continue when:** Set the companion resources.

**If not:** Do not submit duplicate jobs for several GPU models.

### 5. Set the lab starter profile

**Where:** Your computer

Remove the partition line and the old --mem line. Replace the account, GPU, CPU, memory-per-CPU, and time directives with the starter lines below. If you selected another supported GPU, replace only rtx_4090 with rtx_3090 or pro_6000.

**Put this in the named Bash file:**

<!-- passport-snippet:euler-gpu-4090-starter -->
```bash
#SBATCH --account=es_fuge
#SBATCH --gpus=rtx_4090:1
#SBATCH --cpus-per-task=16
#SBATCH --mem-per-cpu=3G
```
<!-- /passport-snippet:euler-gpu-4090-starter -->

**Expected:** The script uses es_fuge, one supported GPU, no partition, at most 16 CPUs, no more than 64 GiB total memory, and at most 04:00:00.

**Continue when:** Add unique output and error logs.

**If not:** Reduce the request or explain a measured reason before any live submission.

### 6. Add output and error logs

**Where:** Your computer

Add the time and log directives below. %x expands to the job name and %j to its job ID. Create the logs directory only when this script is later used in a real project; do not submit this exercise fixture.

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

**Where:** Your computer

Inspect only the synthetic GPU file. Confirm that no sbatch command was run.

**Run on Windows - PowerShell:**

```powershell
git diff -- workspace/slurm/gpu_job.slurm.txt
```

**Run on macOS - zsh:**

```zsh
git diff -- workspace/slurm/gpu_job.slurm.txt
```

**Run on Linux - Bash:**

```bash
git diff -- workspace/slurm/gpu_job.slurm.txt
```

**Expected:** The diff contains one explicit one-GPU starter profile and no unrelated change.

**Continue when:** Run Check my work.

**If not:** Correct the fixture locally; live testing is a separate deliberate action.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. The local verifier checks only the
mission activity above. A score of 100% is required, and every
safety-critical question must be correct. Failed attempts provide targeted
feedback and can be retried without penalty.

## If Blocked

Use the RTX 4090 review baseline. Do not submit duplicate jobs for multiple GPU
types or select RTX PRO 6000 merely to bypass a queue. Escalate distributed
training, unusual memory, or CUDA compatibility to the supervisor.

Useful references:

- [Euler GPU review](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/euler-gpu-review.md)
- [Euler GPU track](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/tracks/euler-gpu.md)
- [Slurm reference](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/euler/slurm.md)
- [IDEAL Lab Euler share policy](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/policy/euler-share.md)

## Understand Before Accepting AI Output

Verify that program operations, not only CUDA detection, use the GPU. You must
explain every requested resource and why adding GPUs may not help a CPU-bound
pipeline.

## Finish And Continue

When **Check my work** passes, use **Submit mission** once. The launcher
publishes only this mission's generated, sanitized submission. Continue when the
dashboard shows the trusted result; a local check alone is not a pass.
