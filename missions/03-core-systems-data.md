# Mission: Map Systems And Research Data

## Outcome

You can place code, durable research data, temporary files, GUI work, and
compute intentionally instead of treating every available drive or service as
interchangeable.

## Why This Matters

Git is not a data archive, scratch is not a backup, a laptop is not a shared
compute node, and an AI provider is not automatically approved for unpublished
material. Correct placement prevents data loss, leakage, and blocked projects.

## Before You Start

Read [Environments overview](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/core/environments-overview.md) and
[Data and AI safety](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/core/data-and-ai-safety.md). Ask your
supervisor who owns the project's information decisions.

## Machine And Shell

**Your computer - web browser or text editor.** This is a planning mission; do
not move or delete project files while completing it.

## Steps

Create a map covering these categories:

| Category | Decision to record |
| --- | --- |
| Source code and small text | Authoritative repository and access level |
| Durable research data | Approved NAS or project storage and information owner |
| Temporary working data | Purge behavior and authoritative copy |
| CPU/GPU computation | Laptop, Blade, Euler, or another approved system |
| GUI-only software | Local computer or Blade |
| AI context | Classification, approved service, minimization, and account |

For each category, record where the authoritative copy lives, who approves
access, what is temporary, and how loss is recovered.

## Expected Result

Every important asset has an owner and authoritative location. Temporary
locations are labelled, and no system is selected merely because it is easy to
reach.

## Independent Verification

Ask: “If this laptop or temporary directory disappears today, can the project
recover?” Every important category must have a concrete answer.

## Evidence To Submit

Complete `evidence/core/systems-data.md` using fictional or project-level
descriptions. Do not list protected filenames, credentials, personal data, or
confidential content.

## If Blocked

Do not guess a storage path or AI approval. Record the unresolved decision and
ask the project information owner or supervisor. The
[data and AI policy](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/policy/data-and-ai.md) defines the escalation
boundary.

## Understand Before Accepting AI Output

Zero-data-retention marketing does not decide whether project material may be
uploaded. The information owner, ETH policy, lab policy, account terms, and
data classification all still apply.

## Finish And Continue

Commit the map and keep it available for the final core review and later data,
Blade, and Euler missions rather than creating contradictory maps.
