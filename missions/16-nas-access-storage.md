# Mission: Verify Your Approved NAS Workspace

## Outcome

Connect to the IDEAL Lab NAS, the durable shared network drive for approved project data. Enter only your authorized username folder and verify one harmless test file.

## Concept

NAS means network-attached storage: the IDEAL Lab's durable shared project drive, reached over the ETH network rather than stored inside your laptop. It holds approved project datasets, checkpoints, results, and deliverables that a team must keep and share.

The NAS is organized by supervisor and project permissions. Use only the approved supervisor folder and your ETH-username subfolder. It is not a replacement for GitHub source control and should not be used directly for high-I/O Euler computation.

## Worked Example

One harmless write/read/delete test succeeds inside the approved username
folder; the raw path is never submitted publicly.

Check these points:

- **Where may you create project data on the NAS?** Inside the approved supervisor project folder and your ETH-username subfolder.
- **Should the NAS hold one shared Git working tree?** No; keep separate clones and use GitHub for code collaboration.

## Common Trap

Using the NAS as a shared Git working tree, testing at the share root, exposing the real path publicly, or leaving the probe file behind.

## Your Action

Connect to the approved NAS project folder, verify your username boundary, and let the Passport perform one harmless write-read-delete probe.

**Follow these steps in order.** You need the supervisor's first name and explicit permission first. Never test access at the NAS root or in another person's folder.

### 1. Know what the NAS is

**Where:** This browser

NAS means network-attached storage. It is the lab's durable shared project drive reached over the ETH network. It is not inside your laptop, not a general folder open to everyone, and not the place to run high-I/O Euler jobs directly.

- [Open the NAS reference](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/onboarding_IT_guides/nas_ideal.md)

**Expected:** You can distinguish durable NAS project data from local, GitHub, and temporary storage.

**Continue when:** Ask for the exact approved project folder.

**If not:** Do not mount or probe a guessed folder.

### 2. Confirm the approved folder

**Where:** This browser

Ask your supervisor for the exact supervisor project folder and confirm that your ETH-username subfolder may be created or used there.

**Expected:** You know the supervisor first name, your short ETH username, and who owns the project data.

**Continue when:** Connect to ETH network or VPN.

**If not:** Stop. Do not browse or create folders by guessing.

### 3. Connect to the ETH network

**Where:** Your computer

Use the campus network or ETH VPN before mounting the share.

- [Open the ETH VPN instructions](https://unlimited.ethz.ch/en/help/network/vpn)

**Expected:** The ETH file service is reachable.

**Continue when:** Mount the supervisor project folder.

**If not:** Fix VPN or network access before changing credentials or paths.

### 4. Map the NAS folder in Windows

**Where:** Your computer

Press Win+E, right-click This PC, choose Map network drive, select an unused drive letter, and enter \\d.ethz.ch\groups\mavt\ide\Projects\<SupervisorFirstName>. Replace only the placeholder. Select Use a different account if needed and sign in as d\<eth-username> with your own ETH password.

- [Open the illustrated NAS guide](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/onboarding_IT_guides/nas_ideal.md)

**Expected:** The approved supervisor folder appears under This PC.

**Continue when:** Open or create only your ETH-username subfolder.

**If not:** Check VPN, the supervisor-name spelling, and the d\username account format; do not use another person's saved credentials.

### 5. Connect to the NAS folder in macOS

**Where:** Your computer

Open Finder, press Command+K, and enter smb://d.ethz.ch/groups/mavt/ide/Projects/<SupervisorFirstName>. Replace only the placeholder, choose Connect, and sign in as d\<eth-username> with your own ETH password.

- [Open the illustrated NAS guide](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/onboarding_IT_guides/nas_ideal.md)

**Expected:** The approved supervisor folder appears under Finder Locations.

**Continue when:** Open or create only your ETH-username subfolder.

**If not:** Check VPN, the supervisor-name spelling, and the d\username account format; do not save another person's credentials.

### 6. Connect to the NAS folder in Linux

**Where:** Your computer

Open your file manager, choose Other Locations or Connect to Server, and enter smb://d.ethz.ch/groups/mavt/ide/Projects/<SupervisorFirstName>. Replace only the placeholder and sign in as d\<eth-username> with your own ETH password. Do not use sudo, edit /etc/fstab, or install a system-wide SMB service for onboarding.

- [Open the complete NAS guide](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/onboarding_IT_guides/nas_ideal.md)

**Expected:** The approved supervisor folder opens in the file manager.

**Continue when:** Open or create only your ETH-username subfolder.

**If not:** Check VPN and the exact URL; ask for the approved Linux method instead of changing system settings.

### 7. Enter your username folder

**Where:** Your computer

Inside the mounted supervisor folder, open the folder whose name is exactly your short ETH username. If it is absent and your supervisor authorized you to create it, use New Folder once and give it that exact name. Do not select or test the supervisor root.

**Expected:** The final folder name exactly matches your ETH username.

**Continue when:** Find its local mounted path in the next step.

**If not:** Message your supervisor through your usual private ETH or lab channel: ask them to confirm or create your NAS username folder. Do not put the real path in a public issue.

### 8. Copy the mounted folder path

**Where:** Your computer

Open a local terminal. Type cd followed by one space, drag the authorized ETH-username folder from File Explorer, Finder, or your Linux file manager into the terminal, and press Enter. Then run the displayed command. If dragging does not insert a path, use the file manager's address bar or path-copy action. Copy the printed local path into the Passport field; do not enter the smb:// address.

**Run on Windows - PowerShell:**

```powershell
(Get-Location).Path
```

**Run on macOS - zsh:**

```zsh
pwd
```

**Run on Linux - Bash:**

```bash
pwd
```

**Expected:** The printed local path ends with your short ETH username and opens the same authorized folder in the file manager.

**Continue when:** Use that exact path for the access probe.

**If not:** Do not guess a hidden mount path. Ask for the approved mount method if the file manager cannot expose a local path.

### 9. Run the access probe

**Where:** Your computer

Enter your ETH username and the mounted username-folder path in the local confirmation fields. Check my work creates a random test file, reads it, and removes it inside that boundary.

**Expected:** The local verifier reports username boundary, write, read, and removed as passed.

**Continue when:** Confirm the storage rules.

**If not:** Do not broaden permissions or use chmod 777. For folder ownership or access, message your supervisor through your usual private ETH or lab channel. If the folder works but the Passport verifier fails, use the public help form with only your operating system, this mission title, and the failed step; omit the path and username.

### 10. Use NAS for durable shared data

**Where:** This browser

Keep datasets, checkpoints, and deliverables in the approved project hierarchy. Keep source code in separate Git clones, and stage high-I/O Euler work to approved Euler storage.

**Expected:** NAS holds durable shared data, not a shared Git working tree or active high-I/O Euler workload.

**Continue when:** Submit the sanitized receipt once.

**If not:** Move code collaboration to GitHub and identify the authoritative durable data copy.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work**. The verifier must confirm the boundary, create and read
its random probe, remove the probe, and find no residual file. Every safety
question must be correct.

## If Blocked

Stop if the approved supervisor folder is unknown, another person's folder is
shown, the path is read-only when write access is expected, or the cleanup
fails. Keep the exact path private. For folder ownership or access, message your
supervisor through the private ETH or lab channel you normally use. If the
folder works but the Passport verifier fails, open one
[public Passport help request](https://github.com/soheylm-passport-sandbox/passport-exercises/issues/new?template=passport-help.yml)
with only your operating system, this mission title, and the failed step. Do
not include the path or username. Do not change broad permissions or test at
the share root.

Useful references:

- [NAS guide](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/onboarding_IT_guides/nas_ideal.md)
- [Laptop, NAS, Blade, and Euler](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/core/environments-overview.md)

## Understand Before Accepting AI Output

An agent must not choose a project root, widen permissions, publish the real
path, or claim that the probe was removed without local verification.

## Finish And Continue

Submit only the generated sanitized receipt. The controller verifies its shape
and challenge digest; it never receives the NAS path. Continue when the trusted
GitHub result passes.
