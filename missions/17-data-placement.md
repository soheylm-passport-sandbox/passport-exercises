# Mission: Place Research Data Intentionally

## Outcome

You can map source, authoritative, working, temporary, output, archive, and
disposal locations with explicit owners, access, recovery, and retention.

## Why This Matters

A file can be accessible without being durable, approved, backed up, or safe to
share. Multiple undocumented copies create ambiguity about which one is
authoritative and which rules apply.

## Before You Start

Identify the project information owner and supervisor. Read the
[data placement lab](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/data-placement.md) and current
[data and AI policy](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/policy/data-and-ai.md). Do not move real
project data during this planning mission.

## Machine And Shell

**Your computer - web browser or text editor.** Use sanitized logical paths,
not broad directory listings.

## Steps

For every important dataset or result category, record:

1. Source and provenance.
2. Information owner and classification.
3. Authoritative durable location.
4. Working and temporary copies.
5. People or groups allowed to access it.
6. Backup or snapshot expectation.
7. Retention, purge, and disposal decision.
8. Next owner at project handover.

For NAS work, the normal durable project location is the assigned supervisor
folder followed by your ETH-username folder. Git stores code and small text;
it is not the shared data store.

## Expected Result

Every important asset has exactly one declared authoritative copy, and every
temporary copy is disposable or synchronized back deliberately. Access and
retention decisions have named owners.

## Independent Verification

Test three failures on paper: laptop loss, temporary-storage purge, and project
member departure. The project must still know where the authoritative copy is
and who can restore or hand it over.

## Evidence To Submit

Complete `evidence/data/placement.md`. Use categories rather than protected
filenames. Do not include personal data, credentials, unpublished file content,
or secret storage URLs.

## If Blocked

Do not create another ad hoc copy. Record the unresolved owner, classification,
or storage decision and ask the supervisor. Use the
[NAS guide](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/onboarding_IT_guides/nas_ideal.md) only after the assigned
supervisor folder is known.

## Understand Before Accepting AI Output

An agent cannot decide ownership, classification, retention, or approved
services. It must not scan or reorganize real project data to complete this
exercise.

## Finish And Continue

Commit the lifecycle map for the final data-track review. The next mission
designs safe collaboration without shared Git working trees or world-writable
permissions.
