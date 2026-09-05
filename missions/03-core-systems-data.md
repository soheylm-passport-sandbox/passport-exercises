# Mission: Map Systems And Research Data

## Outcome

Learn what GitHub, the NAS, Blade, Euler, and temporary storage are, then choose the correct place for code, durable data, Windows GUI work, and scheduled computation.

## Concept

A lab project normally uses several systems, each for a different purpose:

- GitHub stores reviewed source code and small text files.
- The IDEAL Lab NAS is durable shared storage for approved project data.
- Blade is a shared remote Windows computer for licensed graphical software.
- Euler is ETH Zurich's shared cluster for CPU and GPU programs submitted through the Slurm scheduler.
- Scratch and temporary folders hold replaceable working files, not the only copy of a result.

Choose a location from its purpose, owner, and retention rules, not from free disk space.

## Worked Example

The map separates source control, durable storage, temporary storage, GUI access, and scheduled computation.

Check these points:

- **Where does maintained source code belong?** In an approved GitHub repository.
- **Where should a heavy batch computation run?** In a Slurm allocation with explicit CPU, memory, and time limits on Euler or another approved compute system.
- **Where should an approved collaborative dataset remain authoritative?** In the supervisor-approved durable project location on NAS or another named project store.
- **What may be placed in scratch storage?** Temporary high-throughput files that can be recreated from recorded inputs.
- **Where should you use an approved Windows-only engineering GUI?** On Blade for interactive GUI work, while heavy batch computation uses an approved compute system.
- **What project context may you send to an AI service during onboarding?** Only the fictional fixture provided by the mission, unless the real data owner approved the exact service and content.

## Common Trap

Choosing a location without checking ownership, backup, lifetime, and where the
data will be processed.

## Your Action

Map code, durable data, temporary files, Windows GUI work, and scheduled compute to the correct lab systems.

**Follow these steps in order.** For each item, decide who owns it, how long it must survive, and where the work actually runs.

### 1. Read the system map before placing files

**Where:** This browser

Identify the role of each location: GitHub for reviewed source code, NAS for durable shared project data, Blade for licensed Windows GUI work, Euler for scheduled computation, and scratch or temporary folders for replaceable working files.

- [Open the complete system decision table](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/core/environments-overview.md)

**Expected:** Each system has one clear purpose and temporary storage is not treated as durable.

**Continue when:** Place source code first.

**If not:** Do not answer from familiarity or free disk space; reread the decision table.

### 2. Place source code

**Where:** This browser

Keep source code and reviewable text in GitHub. Each contributor uses a separate clone and collaborates through branches and pull requests.

**Expected:** Code has version history and no shared writable working tree.

**Continue when:** Continue to durable project data.

**If not:** Move code collaboration out of a shared NAS checkout before continuing.

### 3. Place durable project data

**Where:** This browser

Use the supervisor-approved NAS project folder or another explicitly approved durable project store for datasets, checkpoints, and deliverables.

**Expected:** The durable copy has a named owner and approved access.

**Continue when:** Continue to temporary data.

**If not:** Ask the supervisor for the authoritative project location; do not invent one.

### 4. Identify temporary storage

**Where:** This browser

Use scratch, Blade D:, or another named temporary area only for replaceable working copies. Record how needed results return to durable storage.

**Expected:** No irreplaceable file exists only in temporary storage.

**Continue when:** Continue to interactive GUI work.

**If not:** Copy and verify the required data in durable storage before proceeding.

### 5. Place Windows GUI work

**Where:** This browser

Use Blade for approved interactive Windows software such as CAD or pre/post-processing. Keep durable files on P: and move heavy computation elsewhere.

**Expected:** Blade is used interactively and does not hold the only durable copy.

**Continue when:** Continue to scheduled computation.

**If not:** Stop an unattended heavy workload and choose an approved compute system.

### 6. Place scheduled computation

**Where:** This browser

Use Euler compute nodes through Slurm for CPU or GPU computation. Login nodes are for access, file management, editing, and job control.

**Expected:** The Slurm job requests explicit CPU, memory, and time limits.

**Continue when:** Continue to the classification questions.

**If not:** Do not run the workload directly on an Euler login node.

### 7. Complete the placement map

**Where:** This browser

Classify every fictional item below. Use the named systems and durability rules, not the amount of free disk space.

**Expected:** Every item has one justified location.

**Continue when:** Run Check my work.

**If not:** Return to the relevant system rule and correct the placement.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. The local verifier checks only the
mission activity above. A score of 80% is required, and every
safety-critical question must be correct. Failed attempts provide targeted
feedback and can be retried without penalty.

## If Blocked

Do not guess a storage path or AI approval. Record the unresolved decision and
ask the project information owner or supervisor. The
[data and AI policy](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/policy/data-and-ai.md) defines the escalation
boundary.

Useful references:

- [Environments Overview](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/core/environments-overview.md)
- [Data And Ai Safety](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/core/data-and-ai-safety.md)
- [Data and AI policy](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/policy/data-and-ai.md)

## Understand Before Accepting AI Output

Zero-data-retention marketing does not decide whether project material may be
uploaded. The information owner, ETH policy, lab policy, account terms, and
data classification all still apply.

## Finish And Continue

When **Check my work** passes, use **Submit mission** once. The launcher
publishes only this mission's generated, sanitized submission. Continue when the
dashboard shows the trusted result; a local check alone is not a pass.
