# Mission: Submit And Control A Tiny Euler CPU Job

## Outcome

You can distinguish login from compute nodes, submit one tiny CPU job with
Slurm, inspect it, cancel it, and find its logs without computing on the login
node.

## Why This Matters

Euler login nodes are shared control points. Resource-intensive programs belong
in Slurm allocations, where CPU, memory, time, logs, and ownership are explicit.

## Before You Start

`ssh euler "echo config-ok"` must succeed. On Euler, run `my_share_info` and
confirm `es_fuge`; do not guess an account.

## Machine And Shell

**Euler login node - Bash.** First connect from your local terminal with
`ssh euler`. Stop if the hostname or prompt does not indicate Euler.

## Steps

Create the tiny script exactly as shown:

<!-- passport-snippet:euler-cpu-tiny-request -->
```bash
mkdir -p "$HOME/passport-euler/logs"
cd "$HOME/passport-euler"
cat > first-job.slurm <<'EOF'
#!/usr/bin/env bash
#SBATCH --job-name=passport-cpu
#SBATCH --account=es_fuge
#SBATCH --time=00:02:00
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1
#SBATCH --mem-per-cpu=1G
#SBATCH --output=logs/%x_%j.out
#SBATCH --error=logs/%x_%j.err

set -euo pipefail
echo "job_id=$SLURM_JOB_ID"
echo "host=$(hostname)"
echo "cpus=$SLURM_CPUS_PER_TASK"
for number in 1 2 3 4 5; do
  printf '%s squared is %s\n' "$number" "$((number * number))"
done
EOF
bash -n first-job.slurm
sed -n '1,80p' first-job.slurm
```
<!-- /passport-snippet:euler-cpu-tiny-request -->

Read it before submitting:

```bash
job_id="$(sbatch --parsable first-job.slurm)"
printf 'Submitted job: %s\n' "$job_id"
squeue -j "$job_id"
```

If the request or script is wrong, use `scancel "$job_id"`.

## Expected Result

The job leaves the queue, its output names a compute node, the error log is
empty, and the script requested exactly one CPU, 1 GiB per CPU, two minutes,
and no GPU.

## Independent Verification

After completion, run:

```bash
cat "logs/passport-cpu_${job_id}.out"
cat "logs/passport-cpu_${job_id}.err"
sacct -j "$job_id" --format=JobID,JobName%20,Account,State,ExitCode,Elapsed,AllocCPUS,ReqMem,MaxRSS
seff "$job_id"
```

Accounting may include `.batch` and `.extern` steps. The main state should be
`COMPLETED` with a successful exit code.

## Evidence To Submit

Complete `evidence/euler/first-job.md` with sanitized request, lifecycle, state,
exit, elapsed time, and compute hostname. Do not include unrelated job history,
private paths, credentials, or broad account output.

## If Blocked

For an invalid account, stop and check `my_share_info`. For a pending job,
inspect `myjobs -j "$job_id"` instead of submitting duplicates. Read the first
meaningful error before changing resources. Use the
[first Euler job lab](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/euler-first-job.md) for recovery.

## Understand Before Accepting AI Output

Personally read the script, record the real job ID, know how to cancel it, and
inspect output and accounting. An agent must not submit or enlarge the job.

## Finish And Continue

Keep the sanitized job ID available. The next mission interprets accounting
and proposes evidence-based requests rather than optimizing this toy workload.
