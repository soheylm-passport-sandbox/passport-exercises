# Mission: Design Safe Shared Data Collaboration

## Outcome

You can separate code collaboration from shared datasets, design group
inheritance for approved data directories, and avoid destructive permission
workarounds.

## Why This Matters

A shared Git working tree mixes branches, indexes, uncommitted files, and file
ownership between users. Shared datasets, checkpoints, logs, and results need a
different permission and lifecycle design.

## Before You Start

Complete the data placement map and identify the service owner who controls the
shared group. This mission designs permissions; it does not alter real folders.

## Machine And Shell

**Your computer - text review only.** Do not run recursive `chmod`, `chown`,
`setfacl`, or deletion commands for this assessment.

## Steps

Design two separate workflows:

1. Each contributor keeps an individual Git clone, creates a branch, commits,
   pushes, and integrates through a pull request.
2. Approved large shared assets live outside Git under a project group, with
   group ownership, setgid inheritance for new directories, and default ACLs
   when the storage system supports them.

Define who owns permission changes, how new members receive access, how access
is removed, and how collaborators verify a harmless write only inside their
assigned area.

## Expected Result

No one shares a Git index or solves collaboration with world-writable access.
New shared data inherits the intended group behavior, while private and
unrelated paths remain unchanged.

## Independent Verification

Explain what happens when two people pull different branches in one shared Git
directory. Then explain why `chmod 777` grants more access than collaboration
requires and does not solve ownership, provenance, or recovery.

## Evidence To Submit

Complete `evidence/data/collaboration.md` with a proposed logical layout,
permission intent, access owner, and safe test. Do not include real membership
lists or protected directory output.

## If Blocked

Do not guess numeric group IDs or apply broad recursive commands. Ask the
storage owner to inspect the smallest affected directory. Use
[Euler storage](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/euler/storage.md) for the canonical
setgid/default ACL procedure when Euler is the approved system.

## Understand Before Accepting AI Output

An agent must not apply recursive permission changes based only on a pasted
path. Verify system, owner, group, inheritance, existing contents, and rollback
before any real change.

## Finish And Continue

Commit the collaboration design for the final data-track review. Continue to a
handover packet that another person can use without inheriting your laptop or
account.
