# Mission: Verify Your Approved NAS Workspace

## Outcome

Connect to the NAS, the durable shared network drive. Mount the approved project
folder and verify one harmless write/read/delete
probe inside your authorized username boundary. Submit no private path.

## Concept

NAS means network-attached storage: the durable shared project drive over the
ETH network.
Mapping or mounting a share makes it appear as a drive or folder on your computer.
SMB (Server Message Block) supplies the connection. Permission remains an owner's
decision, even when the service is reachable.

| Address or path | Used for |
| --- | --- |
| Network share address (smb:// on macOS/Linux) | Connecting in the file manager |
| Mounted local filesystem path | The local Passport probe |
| Your ETH-username subfolder | The only authorized probe boundary |

Keep code in separate Git clones. High input/output (high-I/O) work repeatedly
reads/writes large amounts of data; stage it to approved Euler storage rather
than running it directly against the NAS.

## Learning Challenge

A folder is readable. What else must be approved and verified before you write?
Confirm the owner and boundary before the probe, rather than testing at the root.

## Worked Example

<details>
<summary>What the probe establishes</summary>

The launcher creates one random non-sensitive file, reads it and removes it in
your authorized username folder. Success establishes that small round trip;
it does not audit backups, all project permissions or retention. The mounted
path stays local. A cleanup failure is a stop requiring the exact probe's repair.

</details>

## Common Trap

Use the mounted local path, keep the authorized boundary and confirm probe
cleanup. Stop for owner help when any check fails.

## Your Action

Connect to the approved NAS project folder, verify your username boundary, and let the Passport perform one harmless write-read-delete probe.

**Follow these steps in order.** First obtain the supervisor folder and approval. Mount it using only your computer's instructions, then enter your exact ETH-username folder. Never probe the share root or someone else's folder. Never use chmod 777 or broaden permissions to repair access.

**New to text commands?** A command is a line of text that tells a
computer to do one task. A terminal is the text application in which a
shell reads that command. Open PowerShell on Windows or the application
named Terminal on macOS or Linux. The application starts the correct
shell automatically; do not install a separate Bash or zsh application. Read
[Terminal and command basics](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/core/command-line-basics.md)
before continuing if these words are new.

### 1. Know what the NAS is

**Where:** This web page in your browser

NAS means network-attached storage: approved durable shared project storage over the ETH network. Mapping or mounting makes a remote share visible locally. SMB (Server Message Block) is its file-sharing method. Use the address/path distinction above; high-I/O Euler work belongs on approved compute storage.

- [Open the NAS reference](https://github.com/IDEALLab/onboarding-IT/blob/main/onboarding_IT_guides/nas_ideal.md)

**Expected:** You can distinguish durable NAS project data from local, GitHub, and temporary storage.

**Continue when:** Ask for the exact approved project folder.

**If not:** Do not mount or probe a guessed folder.

### 2. Confirm the approved folder

**Where:** This web page in your browser

Ask your supervisor for the exact supervisor project folder and confirm that your ETH-username subfolder may be created or used there.

**Expected:** You know the supervisor first name, your short ETH username, and who owns the project data.

**Continue when:** Connect to ETH network or VPN.

**If not:** Stop. Do not browse or create folders by guessing.

### 3. Connect to the ETH network

**Where:** The laptop or desktop in front of you

Use the campus network or ETH VPN before connecting the network drive. VPN means Virtual Private Network: the official secure connection used to reach ETH-only services from outside the campus network. Connecting a network drive is also called mapping or mounting the share.

- [Open the ETH VPN instructions](https://unlimited.ethz.ch/en/help/network/vpn)

**Expected:** The ETH file service is reachable.

**Continue when:** Mount the supervisor project folder.

**If not:** Fix VPN or network access before changing credentials or paths.

### 4. Map the NAS folder in Windows

**Where:** The laptop or desktop in front of you

Press Win+E, right-click This PC, choose Map network drive, select an unused drive letter, and enter \\d.ethz.ch\groups\mavt\ide\Projects\<SupervisorFirstName>. Replace only the placeholder. Select Use a different account if needed and sign in as d\<eth-username> with your own ETH password.

- [Open the illustrated NAS guide](https://github.com/IDEALLab/onboarding-IT/blob/main/onboarding_IT_guides/nas_ideal.md)

**Expected:** The approved supervisor folder appears under This PC.

**Continue when:** Open or create only your ETH-username subfolder.

**If not:** Check VPN, the supervisor-name spelling, and the d\username account format; do not use another person's saved credentials.

### 5. Connect to the NAS folder in macOS

**Where:** The laptop or desktop in front of you

Open Finder, press Command+K, and enter smb://d.ethz.ch/groups/mavt/ide/Projects/<SupervisorFirstName>. Replace only the placeholder, choose Connect, and sign in as d\<eth-username> with your own ETH password.

- [Open the illustrated NAS guide](https://github.com/IDEALLab/onboarding-IT/blob/main/onboarding_IT_guides/nas_ideal.md)

**Expected:** The approved supervisor folder appears under Finder Locations.

**Continue when:** Open or create only your ETH-username subfolder.

**If not:** Check VPN, the supervisor-name spelling, and the d\username account format; do not save another person's credentials.

### 6. Connect to the NAS folder in Linux

**Where:** The laptop or desktop in front of you

Open your file manager, choose Other Locations or Connect to Server, and enter smb://d.ethz.ch/groups/mavt/ide/Projects/<SupervisorFirstName>. Replace only the placeholder and sign in as d\<eth-username> with your own ETH password. Do not use sudo, edit /etc/fstab, or install a system-wide network file-sharing service for onboarding.

- [Open the complete NAS guide](https://github.com/IDEALLab/onboarding-IT/blob/main/onboarding_IT_guides/nas_ideal.md)

**Expected:** The approved supervisor folder opens in the file manager.

**Continue when:** Open or create only your ETH-username subfolder.

**If not:** Check VPN and the exact URL; ask for the approved Linux method instead of changing system settings.

### 7. Enter your username folder

**Where:** The laptop or desktop in front of you

Inside the mounted supervisor folder, open the folder whose name is exactly your short ETH username. If it is absent and your supervisor authorized you to create it, use New Folder once and give it that exact name. Do not select or test the supervisor root.

**Expected:** The final folder name exactly matches your ETH username.

**Continue when:** Find its local mounted path in the next step.

**If not:** Message your supervisor through your usual private ETH or lab channel: ask them to confirm or create your NAS username folder. Do not put the real path in a public issue.

### 8. Copy the mounted folder path

**Where:** The laptop or desktop in front of you

Open a local terminal. Type cd followed by one space, drag the authorized ETH-username folder from File Explorer, Finder, or your Linux file manager into the terminal, and press Enter. Then run the displayed command. If dragging does not insert a path, use the file manager's address bar or path-copy action. Copy the printed local path into the Passport field; do not enter the smb:// address. Paths with spaces must stay quoted as inserted by the file manager. An SMB network address is not the mounted filesystem path.

**Open PowerShell on your Windows computer, then run:**

```powershell
(Get-Location).Path
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
pwd
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
pwd
```

**Expected:** The printed local path ends with your short ETH username and opens the same authorized folder in the file manager.

**Continue when:** Use that exact path for the access probe.

**If not:** Do not guess a hidden mount path. Ask for the approved mount method if the file manager cannot expose a local path.

### 9. Run the access probe

**Where:** The laptop or desktop in front of you

Enter your ETH username and the mounted username-folder path in the local confirmation fields. Check my work creates a random test file, reads it, and removes it inside that boundary.

**Expected:** Check my work reports that the username boundary, write, read, and removal checks passed.

**Continue when:** Confirm the storage rules.

**If not:** Stop and inspect the named failure. If cleanup failed, request private support for the affected username folder and exact check; do not broaden permissions, test the root or delete other files.

### 10. Use NAS for durable shared data

**Where:** This web page in your browser

Keep datasets, checkpoints, and deliverables in the approved project hierarchy. Keep source code in separate Git clones, and stage high-I/O Euler work to approved Euler storage.

**Expected:** NAS holds durable shared data, not a shared Git working tree or active high-I/O Euler workload.

**Continue when:** Submit the generated result once; it excludes the private NAS path and username.

**If not:** Move code collaboration to GitHub and identify the location that holds the main durable data copy.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work**. The automatic check must confirm the boundary, create and
read its random test file, remove that file, and find no remaining test file. Every safety
question must be correct.

## Learning Check

### Practise

Try an answer before opening the explanation. These questions are for
practice; they do not affect your progress.

1. You can read the supervisor folder, but your username folder is not writable. What does this show?

   - The whole share should be made writable.
   - Reading the share does not prove write permission in the approved boundary; ask its owner before changing access.
   - Test inside another person's writable folder.

<details class="learning-explanation">
<summary>See an explanation</summary>

Read and write access are separate. Confirm the intended username boundary with its owner; a readable share is not authorization to broaden permissions or test elsewhere.

</details>

## If Blocked

Stop if the approved supervisor folder is unknown, another person's folder is
shown, the path is read-only when write access is expected, or the cleanup
fails. Keep the exact path private. For folder ownership or access, message your
supervisor through the private ETH or lab channel you normally use. If the
folder works but **Check my work** fails, open one
[public Passport help request](https://github.com/soheylm-passport-sandbox/passport-exercises/issues/new?template=passport-help.yml)
with only your operating system, this mission title, and the failed step. Do
not include the path or username. Do not change broad permissions or test at
the share root.

Useful references:

- [NAS guide](https://github.com/IDEALLab/onboarding-IT/blob/main/onboarding_IT_guides/nas_ideal.md)
- [Laptop, NAS, Blade, and Euler](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/core/environments-overview.md)

## Understand Before Accepting AI Output

An agent must not choose a project root, widen permissions, publish the real
path, or claim that the probe was removed without local verification.

## Finish And Continue

Submit only the generated result, which excludes the NAS path and username.
The automatic GitHub check verifies it without receiving those private values.
Continue when the GitHub result passes.
