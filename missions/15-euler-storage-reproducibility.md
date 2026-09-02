# Mission: Place Euler Data And Freeze Run Inputs

## Outcome

You can choose durable, working, scratch, and node-local locations, preserve
production run identity, and prevent mutable files from changing under queued
or running jobs.

## Why This Matters

`$SCRATCH` is not a backup and `$TMPDIR` disappears with the job. Slurm captures
the batch script, not every external code, configuration, model, or input file
it references.

## Before You Start

Know the project information owner and approved Euler project/work location.
Do not move real data for this planning mission.

## Machine And Shell

**Your computer or Euler login node - planning and read-only inspection.** On
Euler, `printf 'HOME=%s\nSCRATCH=%s\n' "$HOME" "$SCRATCH"` may be used to
identify paths without changing data.

## Steps

Create a storage map for:

1. Git-tracked source and small configuration.
2. Durable shared project data and final results.
3. Re-creatable short-term `$SCRATCH` data.
4. Job-specific `$TMPDIR` input/output.
5. Logs and checkpoints needed after a failure.

For a production run, record a clean source revision, declared environment,
run-specific configuration, immutable input identifier, resource request,
output directory, and checkpoint policy. Copy required `$TMPDIR` outputs to a
durable location before job exit.

## Expected Result

Important data has a durable authoritative copy and recovery owner. Scratch and
node-local data are explicitly disposable. Queued jobs reference an immutable
run snapshot rather than a collaborator's changing working directory.

## Independent Verification

For every location, answer: “What happens if this disappears now?” If the only
copy of important work is scratch, `$TMPDIR`, a laptop, or an uncommitted
working tree, the map fails.

## Evidence To Submit

Complete `evidence/euler/storage-reproducibility.md` using sanitized logical
paths. Do not publish private project names, protected filenames, or broad
directory listings.

## If Blocked

Do not invent permissions or recursively change a shared tree. Ask the data
owner about authoritative storage and use
[Euler storage](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/euler/storage.md) for lifecycle and
collaboration recovery.

## Understand Before Accepting AI Output

Inspect every source and destination before copying or deleting. An agent must
not assume a temporary path is backed up or that a successful transfer is a
backup.

## Finish And Continue

The Euler CPU endorsement now has evidence for access, job lifecycle,
accounting, concurrency, storage, and reproducibility. GPU users continue to a
static one-GPU review.
