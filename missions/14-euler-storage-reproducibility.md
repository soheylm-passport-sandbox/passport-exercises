# Mission: Place Euler Data And Freeze Run Inputs

## Outcome

Choose how a fictional beam run preserves exact inputs and useful results.
The current assessment checks decisions, not a real recoverable run record.

## Concept

Names beginning with $ are shell variables that resolve to paths. Follow one
fictional project through its run; locations must still be owner-approved.

| Stage | Fictional item | Decision |
| --- | --- | --- |
| Before submission | Reviewed code, measurements and configuration | Identify the commit, environment and unchanged input snapshot |
| During computation | Rebuildable mesh and intermediate files | Use $SCRATCH or job-local $TMPDIR, never the only important copy |
| After computation | Result, useful logs and run metadata | Verify the copy in approved durable project storage before cleanup |

$HOME is small private storage; /cluster/work/fuge is approved shared working
storage. Neither a temporary directory nor a Slurm script replaces a run record.
A reproducible run records code, environment, inputs, configuration and command
so someone can identify what produced its result.

## Learning Challenge

The job is pending while a collaborator edits its input. What must be stable
before it starts? Make that decision before reading the explanation.

## Worked Example

<details>
<summary>Why the pending job needs unchanged referenced files</summary>

The submitted batch script is captured, but external code/configuration/input
files can still change. Use an immutable reviewed run snapshot and retain its
identifiers. Copy useful results and metadata back to approved durable storage
and verify them. A matching checksum establishes copy equality, not permission,
backup or retention. The optional GitHub code-sync guide is extra practice after
this lesson; it introduces no completion requirement.

</details>

## Common Trap

Keeping the only result in temporary storage, or assuming that a commit ID
freezes every file in a live working directory.

## Your Action

Apply the fictional beam-run lifecycle to the six placement and reproducibility decisions. No real run record or project data is submitted.

**Follow these steps in order.** Names such as $HOME and $SCRATCH are shell variables: short names that resolve to paths on Euler. High input/output (high-I/O) work repeatedly reads or writes a large amount of data. Use the fictional scenario. Choose locations by ownership and durability, not convenience.

### 1. Know the Euler storage areas

**Where:** This web page in your browser

Follow the fictional beam run in the table above. $HOME holds small private code/configuration; approved shared work storage holds the main inputs and outputs. Temporary copies need a rebuild or copy-back rule.

- [Open the Euler storage reference](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/euler/storage.md)

**Expected:** You can identify which locations survive, which are shared, and which are temporary.

**Continue when:** Record the code revision for the fictional run.

**If not:** Do not place the only copy of a result in scratch or TMPDIR.

### 2. Record the code revision

**Where:** This web page in your browser

For this fictional run, choose the reviewed commit before submission. Its identifier records a version; a separate clean, immutable run snapshot prevents later working-tree edits from changing what the job reads.

**Expected:** The run plan names one exact commit and a clean or explicitly described source state.

**Continue when:** Choose the exact input location for this run.

**If not:** Do not call an uncommitted changing checkout reproducible.

### 3. Freeze input identity

**Where:** This web page in your browser

The approved beam measurements have a known version/checksum. Decide whether a job may point to a file still edited by a collaborator. A checksum detects a changed file; it does not approve its contents or freeze it.

**Expected:** The inputs used by the job can be identified later.

**Continue when:** Choose temporary working storage.

**If not:** Stop if a pending job points to files that collaborators may overwrite.

### 4. Use scratch only for replaceable work

**Where:** This web page in your browser

Use Euler scratch for high-throughput temporary files that can be rebuilt. Do not leave the only checkpoint or result there.

**Expected:** Every scratch item has a rebuild or copy-back rule.

**Continue when:** Choose the durable output destination.

**If not:** Copy and verify irreplaceable output in approved durable storage.

### 5. Name durable outputs and ownership

**Where:** This web page in your browser

After computation, verify the result in the owner-approved durable location and retain its metadata. Only then follow the approved cleanup/retention rule. No actual copy or deletion is required in this lesson.

**Expected:** The main durable result location and its owner are stated explicitly.

**Continue when:** Record the software environment.

**If not:** Ask the project owner before inventing a durable location.

### 6. Record the environment

**Where:** This web page in your browser

Record modules, environment definition, application version, configuration, and the exact command or script used.

**Expected:** Another authorized user can reconstruct the software context.

**Continue when:** Keep run-specific logs with the run record.

**If not:** Do not rely on an undocumented interactive shell history.

### 7. Keep identifiable logs

**Where:** This web page in your browser

Use run-specific log names containing the job ID and retain the useful logs with the run metadata.

**Expected:** Each log maps to one submitted job and configuration.

**Continue when:** Complete the placement questions.

**If not:** Correct colliding or ambiguous log paths first.

### 8. Complete the run plan

**Where:** This web page in your browser

Answer the six fictional decisions. Use the table as a lookup; this assessment does not create or check a free-form run plan. Optional code synchronization after completion is separate from progress.

**Expected:** Git, durable storage, scratch, environment metadata, and logs have distinct roles.

**Continue when:** Run Check my work.

**If not:** Return to the first file or result whose owner or durability is unclear.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. This check runs on your computer and
checks only the practical work in this lesson. A score of 80% is required, and every
safety-critical question must be correct. Failed attempts provide targeted
feedback and can be retried without penalty.

## Learning Check

### Practise

Try an answer before opening the explanation. These questions are for
practice; they do not affect your progress.

1. A job is pending. Its batch script names a configuration file that a collaborator replaces. Has the submitted script frozen that configuration?

   - No. Preserve a run-specific configuration snapshot and leave referenced files unchanged.
   - Yes. Submitting the script freezes every named file automatically.
   - Yes, if the new file keeps the same name.

<details class="learning-explanation">
<summary>See an explanation</summary>

Slurm captures the submitted script, not every external file it references. A run-specific unchanged snapshot and its identifiers keep the intended configuration identifiable. A filename alone cannot do that.

</details>

## If Blocked

Do not invent permissions or recursively change a shared folder. Ask the data
owner which approved location holds the main durable copy, and use
[Euler storage](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/euler/storage.md) for lifecycle and
collaboration recovery.

Useful references:

- [Euler storage](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/euler/storage.md)
- [Slurm reference](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/euler/slurm.md)
- [Data Placement](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/labs/data-placement.md)

## Understand Before Accepting AI Output

Inspect every source and destination before copying or deleting. An agent must
not assume a temporary path is backed up or that a successful transfer is a
backup.

## Finish And Continue

When **Check my work** passes, use **Submit lesson** once. The launcher
publishes only this lesson's generated submission after private information is excluded. Continue when the
progress page shows the automatic GitHub result as passed; a check on your computer alone is not a pass.
