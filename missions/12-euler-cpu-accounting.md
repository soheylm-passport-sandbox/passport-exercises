# Mission: Measure And Right-Size An Euler Job

## Outcome

Use Slurm accounting commands to compare the CPU and memory reserved for one completed Euler job with what it actually used, then choose the next request from evidence.

## Concept

A Slurm request reserves CPU, memory, and time for an Euler job. Requested resources and resources actually used are different. `sacct` reports exact accounting fields for a recorded job, while `seff` summarizes CPU and memory efficiency.

Large “just in case” requests can wait longer and reduce capacity for others without making a serial or I/O-bound program faster. Measure a representative run before changing the next request.

## Worked Example

The proposed request follows measured utilization and does not enlarge resources merely to hide an error.

Check these points:

- **Which value helps estimate memory actually used?** MaxRSS, interpreted with the job steps and units.
- **A job exits immediately with a Python import error. What should you optimize first?** Fix and test the software environment before changing resources.
- **A representative serial job requested 4 CPUs, 16 GiB per CPU, and 2 hours. It completed in 20 minutes with 22% CPU efficiency and 9 GiB MaxRSS. Which next test is justified?** Test 1 CPU, 16 GiB total memory, and 45 minutes on a representative input.

## Common Trap

Treating requested memory as measured memory, or increasing every resource after a software failure.

## Your Action

Connect to Euler, read sacct and seff for the completed training job, then choose the next request from measured use.

**Follow these steps in order.** Connect to Euler and reuse the job ID from the first-job mission. This mission does not submit another job.

### 1. Distinguish requested and used resources

**Where:** This browser

A Slurm request reserves CPUs, memory, and time before a job runs. sacct provides exact recorded fields; seff summarizes CPU and memory efficiency. Read both for the existing job before deciding what a future run should request.

- [Open the Slurm accounting reference](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/euler/slurm.md)

**Expected:** You can distinguish allocated resources from measured use.

**Continue when:** Connect and recover the existing job ID.

**If not:** Return to the first-job mission; do not submit another job for this exercise.

### 2. Connect to Euler

**Where:** Your computer

From the local terminal, connect with the tested euler alias. Run every later command in the Euler shell that opens.

**Run on Windows - PowerShell:**

```powershell
ssh euler
```

**Run on macOS - zsh:**

```zsh
ssh euler
```

**Run on Linux - Bash:**

```bash
ssh euler
```

**Expected:** The prompt changes to an Euler login node.

**Continue when:** Recover the existing training job ID on Euler.

**If not:** Return to the SSH access mission; do not run Euler commands in the local shell.

### 3. Use the existing job ID

**Where:** Euler login node

Read the job ID saved by the previous mission. If the file is missing, list recent accounting records and identify the single passport-cpu job instead of submitting another job.

**Run on Euler - Bash:**

```bash
id_file="$HOME/passport-euler/first-job.id"
if [ -s "$id_file" ]; then printf 'Stored job ID: '; cat "$id_file"; else sacct -X -u "$USER" --starttime today --format=JobID,JobName,State,Elapsed; fi
```

**Expected:** You identify the existing passport-cpu job ID.

**Continue when:** Inspect its detailed accounting.

**If not:** Stop if you cannot identify one unambiguous training job.

### 4. Read the accounting fields

**Where:** Euler login node

Load the stored ID. If it was missing, enter the passport-cpu ID you identified and save it. Then query state, exit code, elapsed time, allocated CPUs, requested memory, and maximum resident memory. Continue only after the main job is COMPLETED with exit code 0:0.

**Run on Euler - Bash:**

```bash
(
set -eu
id_file="$HOME/passport-euler/first-job.id"
if [ -e "$id_file" ] && [ ! -s "$id_file" ]; then printf 'STOP: %s exists but is empty. Ask for help before changing it.\n' "$id_file" >&2; exit 1; fi
if [ -s "$id_file" ]; then job_id="$(cat "$id_file")"; else read -r -p 'Existing passport-cpu job ID: ' job_id; fi
case "$job_id" in ''|*[!0-9]*) printf 'STOP: job ID must contain digits only.\n' >&2; exit 1;; esac
if [ ! -e "$id_file" ]; then mkdir -p "$(dirname "$id_file")"; printf '%s\n' "$job_id" > "$id_file"; chmod 600 "$id_file"; fi
sacct -j "$job_id" --format=JobID,JobName,State,ExitCode,Elapsed,AllocCPUS,ReqMem,MaxRSS
state="$(sacct -X -n -j "$job_id" --format=State | awk 'NF {print $1; exit}' | cut -d+ -f1)"
exit_code="$(sacct -X -n -j "$job_id" --format=ExitCode | awk 'NF {print $1; exit}')"
[ "$state" = COMPLETED ] && [ "$exit_code" = 0:0 ] || { printf 'STOP: wait for COMPLETED 0:0 or inspect the failed job; do not resubmit. Current result: %s %s\n' "${state:-unavailable}" "${exit_code:-unavailable}" >&2; exit 1; }
printf 'accounting-ready\n'
)
```

**Expected:** sacct shows the main job and its steps, the main job is COMPLETED with exit code 0:0, MaxRSS is read from the relevant step when available, and the final line is accounting-ready.

**Continue when:** Read the efficiency summary.

**If not:** Wait for accounting to appear or verify the job ID; do not resubmit.

### 5. Read seff

**Where:** Euler login node

Use seff for a concise CPU and memory efficiency summary, while keeping sacct as the source for exact fields.

**Run on Euler - Bash:**

```bash
(
job_id="$(cat "$HOME/passport-euler/first-job.id")"
case "$job_id" in ''|*[!0-9]*) printf 'STOP: stored job ID is invalid.\n' >&2; exit 1;; esac
seff "$job_id"
)
```

**Expected:** seff reports the same job's CPU and memory efficiency.

**Continue when:** Decide what evidence is representative.

**If not:** Use sacct and application logs if seff is unavailable.

### 6. Interpret before changing resources

**Where:** Euler login node

Separate requested resources from actual use. A very short smoke test proves the workflow but may be too short to size a production run.

**Expected:** You can explain AllocCPUS, ReqMem, MaxRSS, Elapsed, State, and ExitCode.

**Continue when:** Choose a justified next request.

**If not:** Return to the field definitions; do not increase resources by guesswork.

### 7. Choose the next measured request

**Where:** Euler login node

Keep or reduce unused resources, leave sensible headroom for representative variation, and increase a resource only after identifying that bottleneck.

**Expected:** The proposed CPU, memory, and time values cite measured evidence.

**Continue when:** Complete the questions and local confirmation.

**If not:** Measure a representative input before claiming a production allocation.

### 8. Submit accounting evidence

**Where:** Your computer

Enter the existing job ID and confirm that you personally inspected sacct and seff. Do not paste logs into the public record.

**Expected:** The local receipt records only the sanitized inspection facts.

**Continue when:** Run Check my work and submit once.

**If not:** Return to Euler and inspect the named command before attesting.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. The local verifier checks only the
mission activity above. A score of 80% is required, and every
safety-critical question must be correct. Failed attempts provide targeted
feedback and can be retried without penalty.

## If Blocked

Do not increase resources when fields are unclear. Use
[Euler resource optimization](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/euler-resource-optimization.md)
and ask for help for MPI/multiprocess workloads, highly variable inputs, or
disagreeing metrics.

Useful references:

- [Euler resource optimization](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/euler-resource-optimization.md)
- [Slurm reference](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/euler/slurm.md)

## Understand Before Accepting AI Output

Verify arithmetic, per-CPU versus total memory, representativeness, and the
parallelism claim. An agent cannot infer scaling merely from CPU availability.

## Finish And Continue

When **Check my work** passes, use **Submit mission** once. The launcher
publishes only this mission's generated, sanitized submission. Continue when the
dashboard shows the trusted result; a local check alone is not a pass.
