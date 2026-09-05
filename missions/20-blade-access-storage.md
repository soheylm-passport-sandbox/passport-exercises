# Mission: Use Blade For GUI Work Without Losing Data

## Outcome

Connect to Blade, use the correct storage drives, and verify a
temporary-to-durable file copy.

## Concept

Blade is a shared Windows engineering workstation, not an HPC cluster or
permanent personal drive. Data left only on local `C:` or temporary `D:` can be
lost, while heavy computation can degrade every interactive user.

## Worked Example

The durable copy remains on P:, D: is clean, C: was not used, and no heavy unattended compute was started.

Check these points:

- **Where does durable Blade project work belong?** In the approved P: supervisor and username folder.
- **What is Blade primarily for?** Interactive Windows GUI software and light prototyping.

## Common Trap

Keeping the only copy on C: or D:, treating Blade as a general ML server, or exposing the real mapped path in the public submission.

## Your Action

Connect to Blade by RDP, verify the host, and complete a safe temporary-to-durable file round trip.

**Follow these steps in order.** Blade is a shared Windows GUI workstation. Use P: for durable project data, D: for temporary work, and never C: or user folders for project storage.

### 1. Confirm Blade is the right system

**Where:** This browser

Use Blade for interactive licensed Windows software, CAD, pre/post-processing, and light prototypes. Use Euler or another approved compute system for long or unattended heavy workloads.

**Expected:** Your task requires the shared Windows GUI environment.

**Continue when:** Connect to the ETH network.

**If not:** Choose the appropriate compute or storage system instead.

### 2. Connect to ETH network or VPN

**Where:** Your computer

Use the campus network or connect ETH VPN before opening RDP.

- [Open the ETH VPN instructions](https://unlimited.ethz.ch/en/help/network/vpn)

**Expected:** The Blade hostname is reachable from your computer.

**Continue when:** Open an RDP client.

**If not:** Fix network access before changing saved credentials.

### 3. Connect from Windows

**Where:** Your computer

Open Start, search for Remote Desktop Connection, and open it. Enter mavt-ide-s100w.d.ethz.ch as the computer. At the credential prompt choose More choices and Use a different account if needed, then sign in as d\<eth-username> with your own ETH password.

- [Open the complete Blade guide](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/onboarding_IT_guides/remote.md)

- [Microsoft: use Remote Desktop on Windows](https://support.microsoft.com/en-us/windows/experience/connectivity-networking/how-to-use-remote-desktop)

**Expected:** A Windows desktop opens for your personal ETH account.

**Continue when:** Verify the remote hostname.

**If not:** Check VPN, the exact hostname, and d\username; remove a wrong saved account instead of using it.

### 4. Connect from macOS

**Where:** Your computer

Install Microsoft Windows App from the Mac App Store if it is absent. Open Windows App, select Devices, select +, choose Add PC, enter mavt-ide-s100w.d.ethz.ch in PC Name, and select Add. Double-click the new PC. At the credential prompt sign in as d\<eth-username> with your own ETH password; do not reuse another person's saved account.

- [Open the complete Blade guide](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/onboarding_IT_guides/remote.md)

- [Microsoft: connect to a remote PC from macOS](https://learn.microsoft.com/en-us/windows-app/get-started-connect-devices-desktops-apps)

**Expected:** A Windows desktop opens for your personal ETH account.

**Continue when:** Verify the remote hostname.

**If not:** Check VPN, the exact hostname, and d\username before changing any remote setting.

### 5. Connect from Linux

**Where:** Your computer

Search your applications for Remmina. If it is installed, open it, choose RDP, enter mavt-ide-s100w.d.ethz.ch as the server, and sign in as d\<eth-username> with your own ETH password. If Remmina is absent on a personal Linux computer, use your distribution's Software application or the official Remmina installation guide; install the RDP client and plugin only. On an ETH-managed computer, request software installation instead. Do not install a remote-desktop server, change a firewall, or alter Blade security settings.

- [Open the complete Blade guide](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/onboarding_IT_guides/remote.md)

- [Official Remmina installation guide](https://remmina.org/how-to-install-remmina/)

**Expected:** A Windows desktop opens for your personal ETH account.

**Continue when:** Verify the remote hostname.

**If not:** Check VPN, protocol RDP, the exact hostname, and d\username. If the client or RDP plugin cannot be installed through the approved software source, use the sanitized Passport help form; do not install remote services.

### 6. Verify the remote computer

**Where:** Blade server

Open PowerShell inside the remote Blade desktop and run the block below. The hostname check is required. The GPU line is informational and may say that the query is unavailable.

**Run on Blade - PowerShell:**

```powershell
& {
  $HostName = $env:COMPUTERNAME
  $HostName
  if ($HostName -ne 'mavt-ide-s100w') { throw "STOP: this is not the assigned Blade server" }
  if (Get-Command nvidia-smi -ErrorAction SilentlyContinue) {
      nvidia-smi --query-gpu=name,memory.total --format=csv,noheader
  } else {
      'GPU query unavailable; hostname is correct.'
  }
}
```

**Expected:** The first line is mavt-ide-s100w. A GPU line may follow, but it is not required to prove the Blade connection.

**Continue when:** Locate the approved P: project folder.

**If not:** Disconnect if the hostname is not the assigned Blade server.

### 7. Confirm P: and D: paths

**Where:** Blade server

Obtain the supervisor first name and approval to use that project folder. Open P:\SupervisorFirstName and create one folder named exactly with your short ETH username if it is absent. The temporary folder is D:\eth-username. Do not use C:, Desktop, Documents, Downloads, or other mapped drives.

**Expected:** The approved P: username folder exists and the D: username folder is clearly temporary.

**Continue when:** Run the harmless file round trip.

**If not:** Ask the supervisor or lab IT for the correct P: folder before creating project data.

### 8. Copy, verify, and clean one test file

**Where:** Blade server

Run this PowerShell block on Blade. It first refuses files, shortcuts, and junctions at either target. It then creates a random non-sensitive file on D:, copies it to the approved P: folder, verifies equal hashes, and removes both probe files.

**Run on Blade - PowerShell:**

```powershell
& {
  $Supervisor = (Read-Host "Supervisor first name").Trim()
  $EthUser = $env:USERNAME
  if ([string]::IsNullOrWhiteSpace($Supervisor) -or $Supervisor -in @('.', '..') -or $Supervisor -match '[\\/:*?"<>|]') { throw "STOP: invalid supervisor folder name" }
  if ($EthUser -notmatch '^[A-Za-z0-9._-]+$') { throw "STOP: invalid ETH username" }
  if (-not (Test-Path -LiteralPath 'P:\' -PathType Container)) { throw "STOP: P: is not available" }
  if (-not (Test-Path -LiteralPath 'D:\' -PathType Container)) { throw "STOP: D: is not available" }
  $Durable = Join-Path "P:\$Supervisor" $EthUser
  $Temporary = Join-Path "D:\" $EthUser
  if (-not (Test-Path -LiteralPath $Durable -PathType Container)) { throw "STOP: approved P: username folder not found" }
  $DurableItem = Get-Item -Force -LiteralPath $Durable
  if (-not $DurableItem.PSIsContainer -or ($DurableItem.Attributes -band [IO.FileAttributes]::ReparsePoint) -ne 0) { throw "STOP: approved P: path is not a real directory" }
  if (Test-Path -LiteralPath $Temporary) {
    $TemporaryItem = Get-Item -Force -LiteralPath $Temporary
    if (-not $TemporaryItem.PSIsContainer -or ($TemporaryItem.Attributes -band [IO.FileAttributes]::ReparsePoint) -ne 0) { throw "STOP: D: username path is not a real directory" }
  } else {
    New-Item -ItemType Directory -Path $Temporary -ErrorAction Stop | Out-Null
    $TemporaryItem = Get-Item -Force -LiteralPath $Temporary
    if (-not $TemporaryItem.PSIsContainer -or ($TemporaryItem.Attributes -band [IO.FileAttributes]::ReparsePoint) -ne 0) { throw "STOP: new D: username path is not a real directory" }
  }
  $Name = "passport-$([guid]::NewGuid().ToString('N')).txt"
  $TempFile = Join-Path $Temporary $Name
  $DurableFile = Join-Path $Durable $Name
  $CopyVerified = $false
  try {
    Set-Content -LiteralPath $TempFile -Value "IDEAL Passport synthetic Blade storage check" -ErrorAction Stop
    Copy-Item -LiteralPath $TempFile -Destination $DurableFile -ErrorAction Stop
    $CopyVerified = (Get-FileHash -LiteralPath $TempFile -ErrorAction Stop).Hash -eq (Get-FileHash -LiteralPath $DurableFile -ErrorAction Stop).Hash
  } finally {
    Remove-Item -LiteralPath $TempFile -Force -ErrorAction SilentlyContinue
    Remove-Item -LiteralPath $DurableFile -Force -ErrorAction SilentlyContinue
  }
  $TemporaryRemoved = -not (Test-Path -LiteralPath $TempFile)
  $ProbeRemoved = -not (Test-Path -LiteralPath $DurableFile)
  "copy_verified=$CopyVerified temporary_removed=$TemporaryRemoved probe_removed=$ProbeRemoved"
  if (-not ($CopyVerified -and $TemporaryRemoved -and $ProbeRemoved)) { throw "STOP: copy verification or probe cleanup failed" }
}
```

**Expected:** The final line says copy_verified=True, temporary_removed=True, and probe_removed=True.

**Continue when:** Confirm the successful copy in the Passport; no probe file remains.

**If not:** Read the first error. The finally block attempts to remove both random probe files even after a failure. If either remains, remove only the two displayed passport probe paths; do not broaden folder permissions or delete the username folder.

### 9. Leave heavy work off Blade

**Where:** Blade server

Do not start overnight training, broad sweeps, or unscheduled heavy computation. Do not install a WSL distribution or enable Windows features without approval.

**Expected:** Only the interactive GUI or light prototype remains on Blade.

**Continue when:** Return to the local Passport.

**If not:** Stop the workload safely and move it to an approved scheduled compute system.

### 10. Record the sanitized result

**Where:** Your computer

Enter only the hostname and yes/no storage confirmations in the local Passport. Do not publish the supervisor name, mapped path, credentials, or screenshot.

**Expected:** The receipt confirms correct host, durable copy, D: cleanup, and no C: usage.

**Continue when:** Run Check my work and submit once.

**If not:** Reconnect and verify the exact missing condition before attesting.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. The local verifier checks only the
mission activity above. A score of 100% is required, and every
safety-critical question must be correct. Failed attempts provide targeted
feedback and can be retried without penalty.

## If Blocked

Check VPN, exact hostname, account format, and assigned supervisor folder. Do
not use another person's saved credentials, install remote services, or select
another mapped drive. Use the
[remote access guide](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/onboarding_IT_guides/remote.md).

Useful references:

- [Blade remote access](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/onboarding_IT_guides/remote.md)
- [NAS guide](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/onboarding_IT_guides/nas_ideal.md)

## Understand Before Accepting AI Output

An agent must not install system features, choose another drive, or run a heavy
local workload because Euler access is inconvenient. Verify host, storage, and
shared-resource impact.

## Finish And Continue

When **Check my work** passes, use **Submit mission** once. The launcher
publishes only this mission's generated, sanitized submission. Continue when the
dashboard shows the trusted result; a local check alone is not a pass.
