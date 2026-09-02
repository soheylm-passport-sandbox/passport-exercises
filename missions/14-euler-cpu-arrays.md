# Mission: Cap And Calculate Euler Job Arrays

## Outcome

You can add an explicit concurrency cap, validate one representative task,
calculate aggregate resources across overlapping submissions, and cancel failed
or duplicate arrays.

## Why This Matters

Array size is not concurrency. An uncapped array can make many tasks eligible
simultaneously, and several individually capped arrays can still exceed a safe
aggregate request.

## Before You Start

Complete one successful single-task job and accounting review. This mission
uses an explicitly labelled non-submit fixture; a live multi-task array is not
required.

## Machine And Shell

**Your computer - text editor.** Euler commands may be discussed, but do not
submit `workspace/slurm/array_job.slurm.txt`.

## Steps

Open the fixture and ensure it contains an explicit cap such as:

```bash
#SBATCH --array=0-9%1
```

Explain why `%1` is the first safe baseline. After one representative task is
measured, a small justified cap such as `%2` may be reviewed.

Calculate concurrent CPUs, memory, and GPUs for the cap. Include every active
ordinary job and array; two arrays capped at `%2` may make four tasks eligible.
Use `%A` for the parent array ID and `%a` for each task ID in log filenames.

## Expected Result

The fixture has an explicit `%` cap, distinct per-task logs, one-task
validation, aggregate arithmetic, and a cancellation plan. It remains a text
fixture and is not submitted.

## Independent Verification

Recalculate the aggregate from scratch and explain the difference between 100
total tasks and two concurrent tasks. State how to inspect your jobs and cancel
the parent job ID.

## Evidence To Submit

Complete `evidence/euler/arrays.md` and correct the `.slurm.txt` fixture. Do not
rename it to an executable Slurm script or submit it.

## If Blocked

Reduce the cap to `%1` and validate a representative input. If many tasks fail
identically, cancel the array and debug one task. Use the
[job arrays lab](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/euler-job-arrays.md) for dependent or
heterogeneous workloads.

## Understand Before Accepting AI Output

Calculate concurrency yourself and include other submissions. A personal or
lab limit is a ceiling, not a target for an agent to consume.

## Finish And Continue

Submit the corrected fixture and arithmetic. The next mission maps durable,
working, scratch, and node-local data and freezes production inputs.
