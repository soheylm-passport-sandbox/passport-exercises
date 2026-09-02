# Mission: Use Blade For GUI Work Without Losing Data

## Outcome

You can reach the shared Windows Blade server, use it for appropriate GUI and
prototype work, place durable data under the assigned project share, use `D:`
only temporarily, and avoid `C:` and personal profile folders.

## Why This Matters

Blade is a shared Windows engineering workstation, not an HPC cluster or
permanent personal drive. Data left only on local `C:` or temporary `D:` can be
lost, while heavy computation can degrade every interactive user.

## Before You Start

Obtain the assigned supervisor folder and confirm VPN requirements. Do not save
credentials in the remote desktop client on an untrusted/shared computer.

## Machine And Shell

**Windows computer - Remote Desktop Connection.**

**macOS computer - Windows App.**

**Linux computer - supervisor-approved RDP client.**

The target PC is `mavt-ide-s100w.d.ethz.ch`.

## Steps

1. Connect to ETH VPN when off-campus.
2. Connect to the target using your personal ETH account.
3. Confirm the Windows host is `mavt-ide-s100w`.
4. Use installed GUI engineering software for interactive design,
   pre/post-processing, and small prototypes.
5. Store durable project work under
   `P:\SupervisorFirstName\eth-username\` as assigned.
6. Use `D:\eth-username\` only for temporary high-speed work; copy required
   output back to `P:` and clean disposable files.
7. Do not store project data on `C:`, Desktop, Documents, or Downloads.
8. Do not install WSL distributions, Windows features, remote services, or
   system software without lab IT approval.

## Expected Result

The session reaches the correct shared host, work uses an appropriate installed
GUI tool, and no important output exists only on local or temporary storage.

## Independent Verification

Before disconnecting, verify: code is committed and pushed; important data is
on `P:`; `D:` content is copied back or disposable; nothing important remains
only under `C:` or the user profile.

## Evidence To Submit

Complete `evidence/blade/access-storage.md` with logical paths and decisions.
Do not include credentials, screenshots containing project data, mapped-drive
membership, or confidential filenames.

## If Blocked

Check VPN, exact hostname, account format, and assigned supervisor folder. Do
not use another person's saved credentials, install remote services, or select
another mapped drive. Use the
[remote access guide](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/onboarding_IT_guides/remote.md).

## Understand Before Accepting AI Output

An agent must not install system features, choose another drive, or run a heavy
local workload because Euler access is inconvenient. Verify host, storage, and
shared-resource impact.

## Finish And Continue

Submit the purpose and storage decision. A live RDP session may be confirmed by
the reviewer when access is available; no protected screenshot is required.
