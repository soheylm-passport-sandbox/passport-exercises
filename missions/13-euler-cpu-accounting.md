# Mission: Measure And Right-Size An Euler Job

## Outcome

You can interpret `sacct` and `seff`, calculate requested resources, distinguish
successful from efficient, and adjust only the next request using representative
evidence.

## Why This Matters

Large “just in case” requests reduce availability and may wait longer without
improving a serial or I/O-bound program. A completed state alone does not prove
appropriate resource use.

## Before You Start

Have sanitized output from the tiny CPU job. Do not submit the intentionally
oversized scenario below.

## Machine And Shell

**Your computer or Euler login node - text review only.** Commands that inspect
your completed tiny job may run on Euler; scenario calculations run locally.

## Steps

Interpret this fictional serial job:

```text
Requested: 16 CPUs, 4 GiB per CPU, 4 hours
State: COMPLETED
Elapsed: 00:11:42
MaxRSS: 3.8 GiB
CPU efficiency: 6.4%
```

1. Calculate total requested memory.
2. Explain why low CPU efficiency matters.
3. Propose a smaller next experiment with justified headroom.
4. State what measurement would justify more CPUs.
5. Explain why one sample may not represent every input.

Then inspect your real tiny job with `sacct` and `seff`. The purpose is to read
the fields, not to optimize the toy calculation as a production workload.

Finally explain this queued-job boundary: Slurm captures the submitted batch
script, but external code, configuration, and input files can change while a
job is pending. Production runs need a clean reviewed source revision and
immutable run-specific configuration/input snapshot.

## Expected Result

The proposal reduces unsupported resources, retains reasonable headroom, and
does not infer parallel scaling from available CPUs. The input explanation
distinguishes captured script text from external mutable files.

## Independent Verification

Check memory arithmetic yourself and identify whether reported memory is per
CPU or per node. When `MaxRSS` is blank for the top-level job, inspect the
`.batch` step.

## Evidence To Submit

Complete `evidence/euler/accounting.md` with the fictional calculation and your
sanitized tiny-job interpretation. Do not include broad job history.

## If Blocked

Do not increase resources when fields are unclear. Use
[Euler resource optimization](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/euler-resource-optimization.md)
and ask for help for MPI/multiprocess workloads, highly variable inputs, or
disagreeing metrics.

## Understand Before Accepting AI Output

Verify arithmetic, per-CPU versus total memory, representativeness, and the
parallelism claim. An agent cannot infer scaling merely from CPU availability.

## Finish And Continue

Submit the measured interpretation and next-request reasoning. The next mission
applies aggregate-resource reasoning to arrays without submitting a large one.
