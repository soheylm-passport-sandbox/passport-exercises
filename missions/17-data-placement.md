# Mission: Place Research Data Intentionally

## Outcome

Decide where fictional project data belongs: who owns it, who may see it,
where it must survive and where it will be used. Move no real data.

## Concept

Research data includes measurements, derived results and records explaining
them. The main approved copy is the version the owner treats as correct.
Sensitivity describes disclosure/access restrictions; durability describes
survival; retention states how long a copy must be kept.

| Fictional beam item | Recovery need | Decision |
| --- | --- | --- |
| Measurements | Cannot be reconstructed | Owner approves classification and durable main copy |
| Derived report | Useful result with provenance | Collaborators need an approved recoverable copy |
| Mesh cache | Can be rebuilt from recorded inputs | Compute location and safe cleanup condition |

A checksum is a calculated fingerprint comparing contents. It establishes
neither permission nor durability. Keep code separate from data and results.

## Learning Challenge

A copy is readable and its checksum matches. Which placement decisions remain?
Try the decisions before opening the explanation.

## Worked Example

<details>
<summary>Separate a verified copy from an approved main copy</summary>

Verify contents, then confirm the owner's approved service, access,
backup/recovery and retention. Temporary work does not replace the durable main
copy. Stage high-I/O inputs to approved compute storage; verify needed output
back before owner-approved cleanup.

</details>

## Common Trap

Choose storage by ownership, access, recovery and lifetime; a filename does
not establish those properties.

## Your Action

Use the fictional beam project to answer six placement decisions. No real files, location map or permissions are submitted.

**Follow these steps in order.** Use the fictional beam project. Decide approval, durability, computation and retention before choosing a location. Move or delete no real data.

### 1. Classify sensitivity

**Where:** This web page in your browser

Use the fictional measurements, report and replaceable mesh above. Classification comes from the information owner and context, not a file extension. Do not use real project details here.

**Expected:** The classification is explicit and justified.

**Continue when:** Name an information owner.

**If not:** Stop placement until the project owner resolves the classification.

### 2. Name the owner

**Where:** This web page in your browser

The fictional project owner decides access and retention. Holding a downloaded copy does not make the analyst the information owner.

**Expected:** One accountable owner is named.

**Continue when:** Decide durability and collaboration needs.

**If not:** Ask the supervisor; do not self-authorize access.

### 3. Decide how long it must survive

**Where:** This web page in your browser

The measurements cannot be reconstructed; the mesh can. Compare recovery needs before assigning a location. A checksum verifies equal contents, not backup or authorization.

**Expected:** Irreplaceable material is assigned to approved durable storage.

**Continue when:** Decide where collaborators and compute need it.

**If not:** Do not leave the only copy in scratch, Blade D:, or a laptop.

### 4. Match collaboration and compute locality

**Where:** This web page in your browser

Keep code in a separate Git clone. Choose approved shared storage for measurements/report and approved compute storage for high-I/O working copies. Do not put data or checkpoints in Git.

**Expected:** The location supports the actual collaborators and workload.

**Continue when:** Define retention and cleanup.

**If not:** Do not run high-I/O Euler work directly against external NAS.

### 5. Record retention and cleanup

**Where:** This web page in your browser

Cleanup is safe only after required outputs reach verified durable storage and the owner-approved retention rule permits removal. No actual deletion is performed.

**Expected:** Every temporary copy has an end condition.

**Continue when:** Complete the fictional placements.

**If not:** Keep the file or result unchanged until the person responsible for retention has decided what must happen.

### 6. Complete each placement

**Where:** This web page in your browser

Answer the six fictional decisions. This assessment checks choices; any extra location map is optional private practice, not a public upload.

**Expected:** No sensitive or durable file or result is assigned to unapproved temporary storage.

**Continue when:** Run Check my work.

**If not:** Correct the first placement with an unresolved owner or durability rule.

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

1. A report copied into temporary storage has the same checksum as its source. Is its placement safe for handover?

   - Yes; matching checksums prove durable storage.
   - Not yet; equality is verified, but approval, durability and retention must be checked.
   - Yes, if its filename contains final.

<details class="learning-explanation">
<summary>See an explanation</summary>

Checksums compare contents. They do not establish approval, backup, access or retention. Verify the needed result in owner-approved durable storage before removing other copies.

</details>

## If Blocked

Do not create another ad hoc copy. Record the unresolved owner, classification,
or storage decision and ask the supervisor. Use the
[NAS guide](https://github.com/IDEALLab/onboarding-IT/blob/main/onboarding_IT_guides/nas_ideal.md) only after the assigned
supervisor folder is known.

Useful references:

- [Data Placement](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/labs/data-placement.md)
- [Data Steward](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/tracks/data-steward.md)
- [NAS guide](https://github.com/IDEALLab/onboarding-IT/blob/main/onboarding_IT_guides/nas_ideal.md)
- [Data and AI policy](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/policy/data-and-ai.md)

## Understand Before Accepting AI Output

An agent cannot decide ownership, classification, retention, or approved
services. It must not scan or reorganize real project data to complete this
exercise.

## Finish And Continue

When **Check my work** passes, use **Submit lesson** once. The launcher
publishes only this lesson's generated submission after private information is excluded. Continue when the
progress page shows the automatic GitHub result as passed; a check on your computer alone is not a pass.
