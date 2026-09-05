# Mission: Establish Safe Euler SSH Access

## Outcome

Connect your computer to Euler, ETH Zurich's shared computing cluster, through SSH. Reuse or create one dedicated key and configure a safe `euler` shortcut without replacing existing SSH files.

## Concept

Euler is ETH Zurich's shared high-performance computing cluster: many managed computers used through a central login service and the Slurm job scheduler. SSH, or Secure Shell, opens a protected terminal connection from your computer to Euler.

An SSH key pair has a private key that stays on your computer and a public `.pub` file that may be installed on Euler. The key passphrase unlocks the local private key; it is different from your ETH password. Test network, password login, key installation, and local configuration in that order, changing only the part that fails.

## Worked Example

Key-only SSH prints config-ok; IdentityFile names a private key, never a .pub file, and no existing key was overwritten.

Check these points:

- **Which file must IdentityFile reference?** The private key path without .pub.
- **What is the safe default when a target key or config already exists?** Stop, back it up, inspect it, and avoid overwriting.

## Common Trap

Running PowerShell at an Euler Bash prompt, concatenating Host blocks, or pointing IdentityFile at the public .pub key.

## Your Action

Test your direct Euler login, keep a working dedicated key or create one without overwriting anything, then configure and test the euler SSH alias.

**Follow these steps in order.** Euler is ETH Zurich's shared computing cluster, and SSH is the secure terminal connection from your computer. Run the 12 checks in order. A key passphrase prompt is normal; an ETH password prompt is not normal during a key-only test.

### 1. Check the network or VPN

**Where:** Your computer

Confirm that this computer has working internet access. Euler SSH normally connects directly to euler.ethz.ch. If that address times out on a restricted network, try the campus network or ETH VPN before changing any SSH file.

- [Open the ETH VPN instructions](https://unlimited.ethz.ch/en/help/network/vpn)

**Expected:** This computer has a working network path for the direct Euler login test.

**Continue when:** Continue to the password-login test.

**If not:** Try the campus network or ETH VPN; do not change SSH keys to solve a timeout.

### 2. Test password login

**Where:** Your computer

Enter the short ETH username, not an email address. On a first connection, compare the host fingerprint with ETH's published host keys before accepting it. This test ignores your user SSH config and disables public-key authentication so it really tests the ETH password.

**Run on Windows - PowerShell:**

```powershell
& {
  $EulerUser = Read-Host "Short ETH username"
  if ($EulerUser -notmatch "^[A-Za-z0-9._-]+$") { throw "STOP: invalid ETH username" }
  ssh -F none -o PubkeyAuthentication=no -o PasswordAuthentication=yes -o KbdInteractiveAuthentication=yes -o PreferredAuthentications=keyboard-interactive,password "$EulerUser@euler.ethz.ch" "echo password-login-ok"
}
```

**Run on macOS - zsh:**

```zsh
(
printf 'Short ETH username: '; read -r eth_user
case "$eth_user" in ''|*[!A-Za-z0-9._-]*) printf 'STOP: invalid ETH username\n' >&2; exit 1;; esac
ssh -F none -o PubkeyAuthentication=no -o PasswordAuthentication=yes -o KbdInteractiveAuthentication=yes -o PreferredAuthentications=keyboard-interactive,password "$eth_user@euler.ethz.ch" 'echo password-login-ok'
)
```

**Run on Linux - Bash:**

```bash
(
printf 'Short ETH username: '; read -r eth_user
case "$eth_user" in ''|*[!A-Za-z0-9._-]*) printf 'STOP: invalid ETH username\n' >&2; exit 1;; esac
ssh -F none -o PubkeyAuthentication=no -o PasswordAuthentication=yes -o KbdInteractiveAuthentication=yes -o PreferredAuthentications=keyboard-interactive,password "$eth_user@euler.ethz.ch" 'echo password-login-ok'
)
```

- [Check ETH Euler host keys](https://docs.hpc.ethz.ch/connections/host-keys/)

**Expected:** After the ETH password, Euler prints password-login-ok.

**Continue when:** Continue to read-only inspection.

**If not:** Stop and solve account, password, VPN, or host-key access first. Do not generate a key yet.

### 3. Inspect existing SSH files without changing them

**Where:** Your computer

List the local .ssh folder, print the numbered user config if it exists, and ask OpenSSH to parse the current euler alias. This step is read-only. Do not edit or delete anything.

**Run on Windows - PowerShell:**

```powershell
& {
  $SshDir = Join-Path $env:USERPROFILE ".ssh"
  Get-ChildItem -LiteralPath $SshDir -Force -ErrorAction SilentlyContinue
  $Config = Join-Path $SshDir "config"
  if (Test-Path -LiteralPath $Config) {
    $i = 0
    Get-Content -LiteralPath $Config | ForEach-Object { $i++; "{0,3}: {1}" -f $i, $_ }
    ssh -G euler | Out-Null
    if ($LASTEXITCODE -ne 0) { throw "STOP: OpenSSH cannot parse the current config; no file was changed" }
    Write-Host "existing-config-parses"
  } else {
    Write-Host "No user SSH config yet."
  }
}
```

**Run on macOS - zsh:**

```zsh
(
ssh_dir="$HOME/.ssh"
ls -la "$ssh_dir" 2>/dev/null || printf 'No .ssh directory yet.\n'
config="$ssh_dir/config"
if [ -f "$config" ]; then
  nl -ba "$config"
  ssh -G euler >/dev/null || {
    printf 'STOP: OpenSSH cannot parse the current config; no file was changed\n' >&2
    exit 1
  }
  printf 'existing-config-parses\n'
else
  printf 'No user SSH config yet.\n'
fi
)
```

**Run on Linux - Bash:**

```bash
(
ssh_dir="$HOME/.ssh"
ls -la "$ssh_dir" 2>/dev/null || printf 'No .ssh directory yet.\n'
config="$ssh_dir/config"
if [ -f "$config" ]; then
  nl -ba "$config"
  ssh -G euler >/dev/null || {
    printf 'STOP: OpenSSH cannot parse the current config; no file was changed\n' >&2
    exit 1
  }
  printf 'existing-config-parses\n'
else
  printf 'No user SSH config yet.\n'
fi
)
```

**Expected:** You know which SSH files exist. An existing config also prints existing-config-parses.

**Continue when:** Test existing key-only access.

**If not:** Stop if OpenSSH names a bad line. Use the SSH troubleshooting page to correct only that line; do not append another Host block or replace the file.

### 4. Keep working key-only access

**Where:** Your computer

First test an existing euler alias when it resolves to this Euler account. The command forces a direct connection to euler.ethz.ch on port 22 and ignores any ProxyCommand or ProxyJump. If that is not available, test the canonical id_ed25519_euler pair directly while ignoring user config. Every connection in this step disables ETH-password and keyboard-interactive fallback.

**Run on Windows - PowerShell:**

```powershell
& {
  $EulerUser = Read-Host "Short ETH username"
  if ($EulerUser -notmatch "^[A-Za-z0-9._-]+$") { throw "STOP: invalid ETH username" }

  $Resolved = @(ssh -G euler 2>$null)
  if ($LASTEXITCODE -ne 0) { throw "STOP: existing SSH config is invalid" }
  $ResolvedHostMatch = $Resolved | Select-String '^hostname\s+' | Select-Object -First 1
  $ResolvedUserMatch = $Resolved | Select-String '^user\s+' | Select-Object -First 1
  $ResolvedHost = if ($ResolvedHostMatch) { ($ResolvedHostMatch.Line -split '\s+', 2)[1] } else { "" }
  $ResolvedUser = if ($ResolvedUserMatch) { ($ResolvedUserMatch.Line -split '\s+', 2)[1] } else { "" }
  $PublicIdentity = @($Resolved | Select-String '^identityfile\s+.*\.pub\s*$')
  if ($ResolvedHost -eq "euler.ethz.ch" -and $ResolvedUser -eq $EulerUser) {
    if ($PublicIdentity.Count -gt 0) { throw "STOP: the existing euler alias points IdentityFile at a .pub file" }
    ssh -o Port=22 -o ProxyCommand=none -o ProxyJump=none -o ForwardAgent=no -o PreferredAuthentications=publickey -o PasswordAuthentication=no -o KbdInteractiveAuthentication=no euler "echo existing-alias-ok"
    if ($LASTEXITCODE -eq 0) { return }
  }

  $KeyPath = Join-Path $env:USERPROFILE ".ssh\id_ed25519_euler"
  $PrivateExists = Test-Path -LiteralPath $KeyPath
  $PublicExists = Test-Path -LiteralPath "$KeyPath.pub"
  if ($PrivateExists -xor $PublicExists) { throw "STOP: the canonical key pair is incomplete; do not overwrite either file" }
  if (-not $PrivateExists) { Write-Host "no-canonical-key"; return }
  ssh -F none -i $KeyPath -o IdentitiesOnly=yes -o PreferredAuthentications=publickey -o PasswordAuthentication=no -o KbdInteractiveAuthentication=no "$EulerUser@euler.ethz.ch" "echo canonical-key-ok"
}
```

**Run on macOS - zsh:**

```zsh
(
printf 'Short ETH username: '; read -r eth_user
case "$eth_user" in ''|*[!A-Za-z0-9._-]*) printf 'STOP: invalid ETH username\n' >&2; exit 1;; esac

resolved="$(ssh -G euler 2>/dev/null)" || {
  printf 'STOP: existing SSH config is invalid\n' >&2
  exit 1
}
resolved_host="$(printf '%s\n' "$resolved" | awk '$1 == "hostname" { print $2; exit }')"
resolved_user="$(printf '%s\n' "$resolved" | awk '$1 == "user" { print $2; exit }')"
if [ "$resolved_host" = "euler.ethz.ch" ] && [ "$resolved_user" = "$eth_user" ]; then
  if printf '%s\n' "$resolved" | awk '$1 == "identityfile" && $2 ~ /[.]pub$/ { found=1 } END { exit !found }'; then
    printf 'STOP: the existing euler alias points IdentityFile at a .pub file\n' >&2
    exit 1
  fi
  if ssh -o Port=22 -o ProxyCommand=none -o ProxyJump=none -o ForwardAgent=no -o PreferredAuthentications=publickey -o PasswordAuthentication=no -o KbdInteractiveAuthentication=no euler 'echo existing-alias-ok'; then
    exit 0
  fi
fi

key="$HOME/.ssh/id_ed25519_euler"
private_exists=0; public_exists=0
[ -f "$key" ] && private_exists=1
[ -f "$key.pub" ] && public_exists=1
if [ "$private_exists" -ne "$public_exists" ]; then
  printf 'STOP: the canonical key pair is incomplete; do not overwrite either file\n' >&2
  exit 1
fi
if [ "$private_exists" -eq 0 ]; then
  printf 'no-canonical-key\n'
  exit 0
fi
ssh -F none -i "$key" -o IdentitiesOnly=yes -o PreferredAuthentications=publickey -o PasswordAuthentication=no -o KbdInteractiveAuthentication=no "$eth_user@euler.ethz.ch" 'echo canonical-key-ok'
)
```

**Run on Linux - Bash:**

```bash
(
printf 'Short ETH username: '; read -r eth_user
case "$eth_user" in ''|*[!A-Za-z0-9._-]*) printf 'STOP: invalid ETH username\n' >&2; exit 1;; esac

resolved="$(ssh -G euler 2>/dev/null)" || {
  printf 'STOP: existing SSH config is invalid\n' >&2
  exit 1
}
resolved_host="$(printf '%s\n' "$resolved" | awk '$1 == "hostname" { print $2; exit }')"
resolved_user="$(printf '%s\n' "$resolved" | awk '$1 == "user" { print $2; exit }')"
if [ "$resolved_host" = "euler.ethz.ch" ] && [ "$resolved_user" = "$eth_user" ]; then
  if printf '%s\n' "$resolved" | awk '$1 == "identityfile" && $2 ~ /[.]pub$/ { found=1 } END { exit !found }'; then
    printf 'STOP: the existing euler alias points IdentityFile at a .pub file\n' >&2
    exit 1
  fi
  if ssh -o Port=22 -o ProxyCommand=none -o ProxyJump=none -o ForwardAgent=no -o PreferredAuthentications=publickey -o PasswordAuthentication=no -o KbdInteractiveAuthentication=no euler 'echo existing-alias-ok'; then
    exit 0
  fi
fi

key="$HOME/.ssh/id_ed25519_euler"
private_exists=0; public_exists=0
[ -f "$key" ] && private_exists=1
[ -f "$key.pub" ] && public_exists=1
if [ "$private_exists" -ne "$public_exists" ]; then
  printf 'STOP: the canonical key pair is incomplete; do not overwrite either file\n' >&2
  exit 1
fi
if [ "$private_exists" -eq 0 ]; then
  printf 'no-canonical-key\n'
  exit 0
fi
ssh -F none -i "$key" -o IdentitiesOnly=yes -o PreferredAuthentications=publickey -o PasswordAuthentication=no -o KbdInteractiveAuthentication=no "$eth_user@euler.ethz.ch" 'echo canonical-key-ok'
)
```

**Expected:** The final marker is existing-alias-ok, canonical-key-ok, or no-canonical-key.

**Continue when:** After existing-alias-ok, skip key generation and installation and continue at the alias step, which preserves the working identity. After canonical-key-ok, also skip to the alias step. After no-canonical-key, continue to key generation.

**If not:** If the canonical pair exists but neither key-only test succeeds, use the next diagnostic step. If OpenSSH reports a .pub IdentityFile, correct that config line first.

### 5. Diagnose an existing key pair without replacing it

**Where:** Your computer

Run this only when id_ed25519_euler exists but the canonical key-only test did not print canonical-key-ok. Compare the private- and public-key fingerprints. This reads the key pair but does not change it.

**Run on Windows - PowerShell:**

```powershell
& {
  $KeyPath = Join-Path $env:USERPROFILE ".ssh\id_ed25519_euler"
  $PrivateFingerprint = ssh-keygen -lf $KeyPath
  if ($LASTEXITCODE -ne 0) { throw "STOP: private key could not be inspected" }
  $PublicFingerprint = ssh-keygen -lf "$KeyPath.pub"
  if ($LASTEXITCODE -ne 0) { throw "STOP: public key could not be inspected" }
  $PrivateFingerprint
  $PublicFingerprint
  if (($PrivateFingerprint -split '\s+')[1] -ne ($PublicFingerprint -split '\s+')[1]) { throw "STOP: private and public keys do not match" }
  Write-Host "key-pair-matches"
}
```

**Run on macOS - zsh:**

```zsh
(
key="$HOME/.ssh/id_ed25519_euler"
private_fingerprint="$(ssh-keygen -lf "$key")" || { printf 'STOP: private key could not be inspected\n' >&2; exit 1; }
public_fingerprint="$(ssh-keygen -lf "$key.pub")" || { printf 'STOP: public key could not be inspected\n' >&2; exit 1; }
printf '%s\n%s\n' "$private_fingerprint" "$public_fingerprint"
[ "$(printf '%s\n' "$private_fingerprint" | awk '{print $2}')" = "$(printf '%s\n' "$public_fingerprint" | awk '{print $2}')" ] || { printf 'STOP: private and public keys do not match\n' >&2; exit 1; }
printf 'key-pair-matches\n'
)
```

**Run on Linux - Bash:**

```bash
(
key="$HOME/.ssh/id_ed25519_euler"
private_fingerprint="$(ssh-keygen -lf "$key")" || { printf 'STOP: private key could not be inspected\n' >&2; exit 1; }
public_fingerprint="$(ssh-keygen -lf "$key.pub")" || { printf 'STOP: public key could not be inspected\n' >&2; exit 1; }
printf '%s\n%s\n' "$private_fingerprint" "$public_fingerprint"
[ "$(printf '%s\n' "$private_fingerprint" | awk '{print $2}')" = "$(printf '%s\n' "$public_fingerprint" | awk '{print $2}')" ] || { printf 'STOP: private and public keys do not match\n' >&2; exit 1; }
printf 'key-pair-matches\n'
)
```

- [Open Euler SSH troubleshooting](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/euler/troubleshooting.md)

**Expected:** Both fingerprint lines contain the same SHA256 value and the final line is key-pair-matches.

**Continue when:** Keep this pair, skip key generation, and continue to Install only the public key.

**If not:** Stop and use the SSH help path. Never overwrite either key file or point IdentityFile at a .pub file.

### 6. Create the canonical key only when absent

**Where:** Your computer

Run this only after no-canonical-key. The guard stops if either half of the pair exists. Choose a passphrase when ssh-keygen asks.

**Run on Windows - PowerShell:**

```powershell
& {
  $SshDir = Join-Path $env:USERPROFILE ".ssh"
  $KeyPath = Join-Path $SshDir "id_ed25519_euler"
  New-Item -ItemType Directory -Force $SshDir | Out-Null
  if ((Test-Path -LiteralPath $KeyPath) -or (Test-Path -LiteralPath "$KeyPath.pub")) { throw "STOP: canonical key or public key already exists; nothing was overwritten" }
  ssh-keygen -t ed25519 -a 100 -f $KeyPath -C "$env:USERNAME@euler"
  if ($LASTEXITCODE -ne 0) { throw "STOP: ssh-keygen failed" }
  icacls $KeyPath /inheritance:r
  icacls $KeyPath /grant:r "${env:USERNAME}:(R)"
}
```

**Run on macOS - zsh:**

```zsh
(
key="$HOME/.ssh/id_ed25519_euler"
mkdir -p "$HOME/.ssh" && chmod 700 "$HOME/.ssh"
if [ -e "$key" ] || [ -e "$key.pub" ]; then printf 'STOP: canonical key or public key already exists; nothing was overwritten\n' >&2; exit 1; fi
ssh-keygen -t ed25519 -a 100 -f "$key" -C "$USER@euler"
)
```

**Run on Linux - Bash:**

```bash
(
key="$HOME/.ssh/id_ed25519_euler"
mkdir -p "$HOME/.ssh" && chmod 700 "$HOME/.ssh"
if [ -e "$key" ] || [ -e "$key.pub" ]; then printf 'STOP: canonical key or public key already exists; nothing was overwritten\n' >&2; exit 1; fi
ssh-keygen -t ed25519 -a 100 -f "$key" -C "$USER@euler"
)
```

**Expected:** Both id_ed25519_euler and id_ed25519_euler.pub are created; the private key has restricted permissions.

**Continue when:** Install only the .pub file.

**If not:** Stop at the first error and keep all pre-existing files unchanged.

### 7. Install only the public key

**Where:** Your computer

Send the contents of id_ed25519_euler.pub through the working password login. The remote command removes a possible Windows carriage return, preserves authorized_keys, and avoids adding a duplicate exact line.

**Run on Windows - PowerShell:**

```powershell
& {
  $EulerUser = Read-Host "Short ETH username used in the password test"
  if ($EulerUser -notmatch "^[A-Za-z0-9._-]+$") { throw "STOP: invalid ETH username" }
  $PublicKey = Join-Path $env:USERPROFILE ".ssh\id_ed25519_euler.pub"
  if (-not (Test-Path -LiteralPath $PublicKey)) { throw "STOP: public key is missing" }
  Get-Content -LiteralPath $PublicKey | ssh -F none -o PubkeyAuthentication=no -o PasswordAuthentication=yes -o KbdInteractiveAuthentication=yes -o PreferredAuthentications=keyboard-interactive,password "$EulerUser@euler.ethz.ch" 'umask 077; mkdir -p ~/.ssh; chmod 700 ~/.ssh; touch ~/.ssh/authorized_keys; chmod 600 ~/.ssh/authorized_keys; key="$(tr -d "\r")"; grep -Fqx "$key" ~/.ssh/authorized_keys || printf "%s\n" "$key" >> ~/.ssh/authorized_keys; printf "public-key-installed\n"'
}
```

**Run on macOS - zsh:**

```zsh
(
printf 'Short ETH username used in the password test: '; read -r eth_user
case "$eth_user" in ''|*[!A-Za-z0-9._-]*) printf 'STOP: invalid ETH username\n' >&2; exit 1;; esac
public_key="$HOME/.ssh/id_ed25519_euler.pub"
test -f "$public_key" || { printf 'STOP: public key is missing\n' >&2; exit 1; }
cat "$public_key" | ssh -F none -o PubkeyAuthentication=no -o PasswordAuthentication=yes -o KbdInteractiveAuthentication=yes -o PreferredAuthentications=keyboard-interactive,password "$eth_user@euler.ethz.ch" 'umask 077; mkdir -p ~/.ssh; chmod 700 ~/.ssh; touch ~/.ssh/authorized_keys; chmod 600 ~/.ssh/authorized_keys; key="$(tr -d "\r")"; grep -Fqx "$key" ~/.ssh/authorized_keys || printf "%s\n" "$key" >> ~/.ssh/authorized_keys; printf "public-key-installed\n"'
)
```

**Run on Linux - Bash:**

```bash
(
printf 'Short ETH username used in the password test: '; read -r eth_user
case "$eth_user" in ''|*[!A-Za-z0-9._-]*) printf 'STOP: invalid ETH username\n' >&2; exit 1;; esac
public_key="$HOME/.ssh/id_ed25519_euler.pub"
test -f "$public_key" || { printf 'STOP: public key is missing\n' >&2; exit 1; }
cat "$public_key" | ssh -F none -o PubkeyAuthentication=no -o PasswordAuthentication=yes -o KbdInteractiveAuthentication=yes -o PreferredAuthentications=keyboard-interactive,password "$eth_user@euler.ethz.ch" 'umask 077; mkdir -p ~/.ssh; chmod 700 ~/.ssh; touch ~/.ssh/authorized_keys; chmod 600 ~/.ssh/authorized_keys; key="$(tr -d "\r")"; grep -Fqx "$key" ~/.ssh/authorized_keys || printf "%s\n" "$key" >> ~/.ssh/authorized_keys; printf "public-key-installed\n"'
)
```

**Expected:** After the ETH password, Euler prints public-key-installed and no SSH or permission error.

**Continue when:** Run the direct key-only test.

**If not:** Do not edit authorized_keys manually; diagnose the reported login or permission error.

### 8. Prove direct key-only access

**Where:** Your computer

Run the direct test with password and keyboard-interactive authentication disabled. Enter only the local key passphrase if prompted.

**Run on Windows - PowerShell:**

```powershell
& {
  $EulerUser = Read-Host "Short ETH username"
  if ($EulerUser -notmatch "^[A-Za-z0-9._-]+$") { throw "STOP: invalid ETH username" }
  $KeyPath = Join-Path $env:USERPROFILE ".ssh\id_ed25519_euler"
  ssh -F none -i $KeyPath -o IdentitiesOnly=yes -o PreferredAuthentications=publickey -o PasswordAuthentication=no -o KbdInteractiveAuthentication=no "$EulerUser@euler.ethz.ch" "echo key-ok"
}
```

**Run on macOS - zsh:**

```zsh
(
printf 'Short ETH username: '; read -r eth_user
case "$eth_user" in ''|*[!A-Za-z0-9._-]*) printf 'STOP: invalid ETH username\n' >&2; exit 1;; esac
ssh -F none -i "$HOME/.ssh/id_ed25519_euler" -o IdentitiesOnly=yes -o PreferredAuthentications=publickey -o PasswordAuthentication=no -o KbdInteractiveAuthentication=no "$eth_user@euler.ethz.ch" 'echo key-ok'
)
```

**Run on Linux - Bash:**

```bash
(
printf 'Short ETH username: '; read -r eth_user
case "$eth_user" in ''|*[!A-Za-z0-9._-]*) printf 'STOP: invalid ETH username\n' >&2; exit 1;; esac
ssh -F none -i "$HOME/.ssh/id_ed25519_euler" -o IdentitiesOnly=yes -o PreferredAuthentications=publickey -o PasswordAuthentication=no -o KbdInteractiveAuthentication=no "$eth_user@euler.ethz.ch" 'echo key-ok'
)
```

**Expected:** Euler prints exactly key-ok without asking for the ETH password.

**Continue when:** Create the isolated euler alias.

**If not:** Stop. Do not continue to the alias or euler-tunnel until this exact test passes.

### 9. Create or update an isolated euler alias

**Where:** Your computer

Back up the existing config and validate it without connecting. If the current euler alias already passed the key-only test, preserve its resolved private-key selection; otherwise use the tested canonical key. Write the policy to passport.d/euler.conf and add one Include line. Backups go in passport-backups, which OpenSSH does not load.

**Run on Windows - PowerShell:**

```powershell
& {
  $EulerUser = Read-Host "Short ETH username"
  if ($EulerUser -notmatch "^[A-Za-z0-9._-]+$") { throw "STOP: invalid ETH username" }
  $SshDir = Join-Path $env:USERPROFILE ".ssh"; $Config = Join-Path $SshDir "config"; $IncludeDir = Join-Path $SshDir "passport.d"; $BackupDir = Join-Path $SshDir "passport-backups"; $EulerConfig = Join-Path $IncludeDir "euler.conf"; $KeyPath = Join-Path $SshDir "id_ed25519_euler"
  $ConfigExisted = Test-Path -LiteralPath $Config
  $EulerConfigExisted = Test-Path -LiteralPath $EulerConfig
  foreach ($Path in @($Config, $EulerConfig)) {
    if ((Test-Path -LiteralPath $Path) -and ((((Get-Item -LiteralPath $Path).Attributes) -band [IO.FileAttributes]::ReparsePoint) -ne 0)) {
      throw "STOP: $Path is a link or reparse point; no file was changed"
    }
  }

  $ResolvedBefore = @(ssh -G euler 2>$null)
  if ($LASTEXITCODE -ne 0) { throw "STOP: existing SSH config is invalid; no file was changed" }
  $ResolvedHostMatch = $ResolvedBefore | Select-String '^hostname\s+' | Select-Object -First 1
  $ResolvedUserMatch = $ResolvedBefore | Select-String '^user\s+' | Select-Object -First 1
  $ResolvedHost = if ($ResolvedHostMatch) { ($ResolvedHostMatch.Line -split '\s+', 2)[1] } else { "" }
  $ResolvedUser = if ($ResolvedUserMatch) { ($ResolvedUserMatch.Line -split '\s+', 2)[1] } else { "" }
  $ResolvedIdentity = @($ResolvedBefore | ForEach-Object { if ($_ -match '^identityfile\s+(.+)$') { $Matches[1] } })
  if (@($ResolvedIdentity | Where-Object { $_ -match '\.pub$' }).Count -gt 0) { throw "STOP: existing IdentityFile points at a .pub file" }

  $UseExisting = $false
  if ($ResolvedHost -eq "euler.ethz.ch" -and $ResolvedUser -eq $EulerUser) {
    ssh -o Port=22 -o ProxyCommand=none -o ProxyJump=none -o ForwardAgent=no -o PreferredAuthentications=publickey -o PasswordAuthentication=no -o KbdInteractiveAuthentication=no euler "exit 0"
    $UseExisting = $LASTEXITCODE -eq 0
  }

  $CanonicalWorks = $false
  $PrivateExists = Test-Path -LiteralPath $KeyPath
  $PublicExists = Test-Path -LiteralPath "$KeyPath.pub"
  if (-not $UseExisting -and ($PrivateExists -xor $PublicExists)) { throw "STOP: canonical key pair is incomplete" }
  if (-not $UseExisting -and $PrivateExists) {
    ssh -F none -i $KeyPath -o IdentitiesOnly=yes -o PreferredAuthentications=publickey -o PasswordAuthentication=no -o KbdInteractiveAuthentication=no "$EulerUser@euler.ethz.ch" "exit 0"
    $CanonicalWorks = $LASTEXITCODE -eq 0
  }
  if (-not $UseExisting -and -not $CanonicalWorks) { throw "STOP: no tested key-only identity is available" }

  New-Item -ItemType Directory -Force $IncludeDir, $BackupDir -ErrorAction Stop | Out-Null
  $Stamp = "$(Get-Date -Format yyyyMMdd-HHmmss-fffffff)-$PID"
  $ConfigBackup = Join-Path $BackupDir "config.$Stamp"
  $EulerConfigBackup = Join-Path $BackupDir "euler.conf.$Stamp"
  if ($ConfigExisted) { Copy-Item -LiteralPath $Config -Destination $ConfigBackup -ErrorAction Stop }
  if ($EulerConfigExisted) { Copy-Item -LiteralPath $EulerConfig -Destination $EulerConfigBackup -ErrorAction Stop }

  $Lines = @("Host euler", "  HostName euler.ethz.ch", "  User $EulerUser")
  if ($UseExisting) {
    if ($ResolvedIdentity.Count -eq 0) { throw "STOP: working alias has no inspectable identity selection" }
    foreach ($Identity in $ResolvedIdentity) {
      if ($Identity.Contains('"')) { throw "STOP: unsupported quote in resolved identity path" }
      $Lines += '  IdentityFile "' + $Identity + '"'
    }
    $ResolvedIdentitiesOnlyMatch = $ResolvedBefore | Select-String '^identitiesonly\s+' | Select-Object -First 1
    $ResolvedIdentitiesOnly = if ($ResolvedIdentitiesOnlyMatch) { ($ResolvedIdentitiesOnlyMatch.Line -split '\s+', 2)[1] } else { "" }
    if ($ResolvedIdentitiesOnly -notin @("yes", "no")) { throw "STOP: invalid resolved IdentitiesOnly value" }
    $Lines += "  IdentitiesOnly $ResolvedIdentitiesOnly"
  } else {
    $Lines += "  IdentityFile ~/.ssh/id_ed25519_euler"
    $Lines += "  IdentitiesOnly yes"
  }
  $Lines += @("  Port 22", "  ProxyCommand none", "  ProxyJump none", "  PreferredAuthentications publickey", "  PasswordAuthentication no", "  KbdInteractiveAuthentication no", "  ForwardAgent no")

  $EulerTemporary = "$EulerConfig.passport-new"
  $Lines | Set-Content -LiteralPath $EulerTemporary -Encoding ascii
  ssh -F $EulerTemporary -G euler | Out-Null
  if ($LASTEXITCODE -ne 0) { Remove-Item -LiteralPath $EulerTemporary -ErrorAction SilentlyContinue; throw "STOP: generated Euler block is invalid" }

  $Include = "Include ~/.ssh/passport.d/*.conf"; $NewLine = [Environment]::NewLine
  $Old = if (Test-Path -LiteralPath $Config) { [System.IO.File]::ReadAllText($Config) } else { "" }
  $Broad = '(?m)^[ \t]*Include[ \t]+(?:~/.ssh/)?passport\.d/\*(?:\.conf)?[ \t]*(?:\r?\n|$)'
  $Rest = [System.Text.RegularExpressions.Regex]::Replace($Old, $Broad, "").TrimStart([char[]]@([char]13, [char]10))
  $Updated = if ($Rest) { "$Include$NewLine$Rest" } else { "$Include$NewLine" }
  $ConfigTemporary = "$Config.passport-new"
  [System.IO.File]::WriteAllText($ConfigTemporary, $Updated, [System.Text.UTF8Encoding]::new($false))
  ssh -F $ConfigTemporary -G euler | Out-Null
  if ($LASTEXITCODE -ne 0) {
    Remove-Item -LiteralPath $EulerTemporary, $ConfigTemporary -ErrorAction SilentlyContinue
    throw "STOP: generated SSH config is invalid; the original files are unchanged"
  }

  try {
    Move-Item -Force -LiteralPath $EulerTemporary -Destination $EulerConfig -ErrorAction Stop
    Move-Item -Force -LiteralPath $ConfigTemporary -Destination $Config -ErrorAction Stop
    ssh -G euler | Out-Null
    if ($LASTEXITCODE -ne 0) { throw "final Euler alias validation failed" }
  } catch {
    $Failure = $_.Exception.Message
    $RestoreFailed = $false
    try {
      if ($ConfigExisted) { Copy-Item -Force -LiteralPath $ConfigBackup -Destination $Config -ErrorAction Stop }
      else { Remove-Item -Force -LiteralPath $Config -ErrorAction SilentlyContinue }
    } catch { $RestoreFailed = $true }
    try {
      if ($EulerConfigExisted) { Copy-Item -Force -LiteralPath $EulerConfigBackup -Destination $EulerConfig -ErrorAction Stop }
      else { Remove-Item -Force -LiteralPath $EulerConfig -ErrorAction SilentlyContinue }
    } catch { $RestoreFailed = $true }
    Remove-Item -Force -LiteralPath $EulerTemporary, $ConfigTemporary -ErrorAction SilentlyContinue
    if ($RestoreFailed) { throw "STOP: install failed and automatic restore was incomplete. Restore only config.$Stamp and euler.conf.$Stamp from $BackupDir. Cause: $Failure" }
    throw "STOP: install failed; the original SSH files were restored automatically. Cause: $Failure"
  }
}
```

**Run on macOS - zsh:**

```zsh
(
  set -eu
  printf 'Short ETH username: '; read -r eth_user
  case "$eth_user" in ''|*[!A-Za-z0-9._-]*) printf 'STOP: invalid ETH username\n' >&2; exit 1;; esac
  ssh_dir="$HOME/.ssh"; config="$ssh_dir/config"; include_dir="$ssh_dir/passport.d"; backup_dir="$ssh_dir/passport-backups"; euler_config="$include_dir/euler.conf"; key="$ssh_dir/id_ed25519_euler"
  [ ! -L "$config" ] || { printf "STOP: %s is a symbolic link; no file was changed\n" "$config" >&2; exit 1; }
  [ ! -L "$euler_config" ] || { printf "STOP: %s is a symbolic link; no file was changed\n" "$euler_config" >&2; exit 1; }
  config_existed=0; euler_config_existed=0
  if [ -e "$config" ]; then [ -f "$config" ] || { printf "STOP: %s is not a regular file\n" "$config" >&2; exit 1; }; config_existed=1; fi
  if [ -e "$euler_config" ]; then [ -f "$euler_config" ] || { printf "STOP: %s is not a regular file\n" "$euler_config" >&2; exit 1; }; euler_config_existed=1; fi

  resolved_before="$(ssh -G euler 2>/dev/null)" || {
    printf 'STOP: existing SSH config is invalid; no file was changed\n' >&2
    exit 1
  }
  resolved_host="$(printf '%s\n' "$resolved_before" | awk '$1 == "hostname" { print $2; exit }')"
  resolved_user="$(printf '%s\n' "$resolved_before" | awk '$1 == "user" { print $2; exit }')"
  if printf '%s\n' "$resolved_before" | awk '$1 == "identityfile" && $2 ~ /[.]pub$/ { found=1 } END { exit !found }'; then
    printf 'STOP: existing IdentityFile points at a .pub file\n' >&2
    exit 1
  fi

  use_existing=0
  if [ "$resolved_host" = "euler.ethz.ch" ] && [ "$resolved_user" = "$eth_user" ]; then
    if ssh -o Port=22 -o ProxyCommand=none -o ProxyJump=none -o ForwardAgent=no -o PreferredAuthentications=publickey -o PasswordAuthentication=no -o KbdInteractiveAuthentication=no euler 'exit 0'; then
      use_existing=1
    fi
  fi

  private_exists=0; public_exists=0
  [ -f "$key" ] && private_exists=1
  [ -f "$key.pub" ] && public_exists=1
  if [ "$use_existing" -eq 0 ] && [ "$private_exists" -ne "$public_exists" ]; then printf 'STOP: canonical key pair is incomplete\n' >&2; exit 1; fi
  canonical_works=0
  if [ "$use_existing" -eq 0 ] && [ "$private_exists" -eq 1 ]; then
    if ssh -F none -i "$key" -o IdentitiesOnly=yes -o PreferredAuthentications=publickey -o PasswordAuthentication=no -o KbdInteractiveAuthentication=no "$eth_user@euler.ethz.ch" 'exit 0'; then
      canonical_works=1
    fi
  fi
  if [ "$use_existing" -eq 0 ] && [ "$canonical_works" -eq 0 ]; then
    printf 'STOP: no tested key-only identity is available\n' >&2
    exit 1
  fi

  mkdir -p "$include_dir" "$backup_dir" && chmod 700 "$ssh_dir" "$include_dir" "$backup_dir"
  stamp="$(date +%Y%m%d-%H%M%S)-$$"
  config_backup="$backup_dir/config.$stamp"
  euler_config_backup="$backup_dir/euler.conf.$stamp"
  [ "$config_existed" -eq 0 ] || cp -p "$config" "$config_backup"
  [ "$euler_config_existed" -eq 0 ] || cp -p "$euler_config" "$euler_config_backup"

  restore_originals() {
    restore_status=0
    if [ "$config_existed" -eq 1 ]; then cp -p "$config_backup" "$config" || restore_status=1; else rm -f "$config" || restore_status=1; fi
    if [ "$euler_config_existed" -eq 1 ]; then cp -p "$euler_config_backup" "$euler_config" || restore_status=1; else rm -f "$euler_config" || restore_status=1; fi
    return "$restore_status"
  }

  euler_temporary="$euler_config.passport-new"
  {
    printf 'Host euler\n  HostName euler.ethz.ch\n  User %s\n' "$eth_user"
    if [ "$use_existing" -eq 1 ]; then
      identity_count=0
      while IFS= read -r identity; do
        [ -n "$identity" ] || continue
        case "$identity" in *'"'*) printf 'STOP: unsupported quote in resolved identity path\n' >&2; exit 1;; esac
        printf '  IdentityFile "%s"\n' "$identity"
        identity_count=$((identity_count + 1))
      done <<EOF
$(printf '%s\n' "$resolved_before" | awk '$1 == "identityfile" { $1=""; sub(/^[[:space:]]+/, ""); print }')
EOF
      [ "$identity_count" -gt 0 ] || { printf 'STOP: working alias has no inspectable identity selection\n' >&2; exit 1; }
      identities_only="$(printf '%s\n' "$resolved_before" | awk '$1 == "identitiesonly" { print $2; exit }')"
      case "$identities_only" in yes|no) ;; *) printf 'STOP: invalid resolved IdentitiesOnly value\n' >&2; exit 1;; esac
      printf '  IdentitiesOnly %s\n' "$identities_only"
    else
      printf '  IdentityFile ~/.ssh/id_ed25519_euler\n  IdentitiesOnly yes\n'
    fi
    printf '  Port 22\n  ProxyCommand none\n  ProxyJump none\n  PreferredAuthentications publickey\n  PasswordAuthentication no\n  KbdInteractiveAuthentication no\n  ForwardAgent no\n'
  } > "$euler_temporary"
  chmod 600 "$euler_temporary"
  ssh -F "$euler_temporary" -G euler >/dev/null || {
    rm -f "$euler_temporary"
    printf 'STOP: generated Euler block is invalid\n' >&2
    exit 1
  }

  include='Include ~/.ssh/passport.d/*.conf'; temporary="$config.passport-new"
  if [ -f "$config" ]; then
    awk -v include="$include" 'BEGIN { print include } /^[[:space:]]*Include[[:space:]]+(~\/[.]ssh\/)?passport[.]d\/[*]([.]conf)?[[:space:]]*$/ { next } { print }' "$config" > "$temporary"
  else
    printf '%s\n' "$include" > "$temporary"
  fi
  chmod 600 "$temporary"
  ssh -F "$temporary" -G euler >/dev/null || {
    rm -f "$euler_temporary" "$temporary"
    printf 'STOP: generated SSH config is invalid; the original files are unchanged\n' >&2
    exit 1
  }

  if ! mv "$euler_temporary" "$euler_config" || ! mv "$temporary" "$config" || ! ssh -G euler >/dev/null; then
    rm -f "$euler_temporary" "$temporary"
    if restore_originals; then
      printf 'STOP: install failed; the original SSH files were restored automatically\n' >&2
    else
      printf 'STOP: install failed and automatic restore was incomplete. Restore only config.%s and euler.conf.%s from %s\n' "$stamp" "$stamp" "$backup_dir" >&2
    fi
    exit 1
  fi
)
```

**Run on Linux - Bash:**

```bash
(
  set -eu
  printf 'Short ETH username: '; read -r eth_user
  case "$eth_user" in ''|*[!A-Za-z0-9._-]*) printf 'STOP: invalid ETH username\n' >&2; exit 1;; esac
  ssh_dir="$HOME/.ssh"; config="$ssh_dir/config"; include_dir="$ssh_dir/passport.d"; backup_dir="$ssh_dir/passport-backups"; euler_config="$include_dir/euler.conf"; key="$ssh_dir/id_ed25519_euler"
  [ ! -L "$config" ] || { printf "STOP: %s is a symbolic link; no file was changed\n" "$config" >&2; exit 1; }
  [ ! -L "$euler_config" ] || { printf "STOP: %s is a symbolic link; no file was changed\n" "$euler_config" >&2; exit 1; }
  config_existed=0; euler_config_existed=0
  if [ -e "$config" ]; then [ -f "$config" ] || { printf "STOP: %s is not a regular file\n" "$config" >&2; exit 1; }; config_existed=1; fi
  if [ -e "$euler_config" ]; then [ -f "$euler_config" ] || { printf "STOP: %s is not a regular file\n" "$euler_config" >&2; exit 1; }; euler_config_existed=1; fi

  resolved_before="$(ssh -G euler 2>/dev/null)" || {
    printf 'STOP: existing SSH config is invalid; no file was changed\n' >&2
    exit 1
  }
  resolved_host="$(printf '%s\n' "$resolved_before" | awk '$1 == "hostname" { print $2; exit }')"
  resolved_user="$(printf '%s\n' "$resolved_before" | awk '$1 == "user" { print $2; exit }')"
  if printf '%s\n' "$resolved_before" | awk '$1 == "identityfile" && $2 ~ /[.]pub$/ { found=1 } END { exit !found }'; then
    printf 'STOP: existing IdentityFile points at a .pub file\n' >&2
    exit 1
  fi

  use_existing=0
  if [ "$resolved_host" = "euler.ethz.ch" ] && [ "$resolved_user" = "$eth_user" ]; then
    if ssh -o Port=22 -o ProxyCommand=none -o ProxyJump=none -o ForwardAgent=no -o PreferredAuthentications=publickey -o PasswordAuthentication=no -o KbdInteractiveAuthentication=no euler 'exit 0'; then
      use_existing=1
    fi
  fi

  private_exists=0; public_exists=0
  [ -f "$key" ] && private_exists=1
  [ -f "$key.pub" ] && public_exists=1
  if [ "$use_existing" -eq 0 ] && [ "$private_exists" -ne "$public_exists" ]; then printf 'STOP: canonical key pair is incomplete\n' >&2; exit 1; fi
  canonical_works=0
  if [ "$use_existing" -eq 0 ] && [ "$private_exists" -eq 1 ]; then
    if ssh -F none -i "$key" -o IdentitiesOnly=yes -o PreferredAuthentications=publickey -o PasswordAuthentication=no -o KbdInteractiveAuthentication=no "$eth_user@euler.ethz.ch" 'exit 0'; then
      canonical_works=1
    fi
  fi
  if [ "$use_existing" -eq 0 ] && [ "$canonical_works" -eq 0 ]; then
    printf 'STOP: no tested key-only identity is available\n' >&2
    exit 1
  fi

  mkdir -p "$include_dir" "$backup_dir" && chmod 700 "$ssh_dir" "$include_dir" "$backup_dir"
  stamp="$(date +%Y%m%d-%H%M%S)-$$"
  config_backup="$backup_dir/config.$stamp"
  euler_config_backup="$backup_dir/euler.conf.$stamp"
  [ "$config_existed" -eq 0 ] || cp -p "$config" "$config_backup"
  [ "$euler_config_existed" -eq 0 ] || cp -p "$euler_config" "$euler_config_backup"

  restore_originals() {
    restore_status=0
    if [ "$config_existed" -eq 1 ]; then cp -p "$config_backup" "$config" || restore_status=1; else rm -f "$config" || restore_status=1; fi
    if [ "$euler_config_existed" -eq 1 ]; then cp -p "$euler_config_backup" "$euler_config" || restore_status=1; else rm -f "$euler_config" || restore_status=1; fi
    return "$restore_status"
  }

  euler_temporary="$euler_config.passport-new"
  {
    printf 'Host euler\n  HostName euler.ethz.ch\n  User %s\n' "$eth_user"
    if [ "$use_existing" -eq 1 ]; then
      identity_count=0
      while IFS= read -r identity; do
        [ -n "$identity" ] || continue
        case "$identity" in *'"'*) printf 'STOP: unsupported quote in resolved identity path\n' >&2; exit 1;; esac
        printf '  IdentityFile "%s"\n' "$identity"
        identity_count=$((identity_count + 1))
      done <<EOF
$(printf '%s\n' "$resolved_before" | awk '$1 == "identityfile" { $1=""; sub(/^[[:space:]]+/, ""); print }')
EOF
      [ "$identity_count" -gt 0 ] || { printf 'STOP: working alias has no inspectable identity selection\n' >&2; exit 1; }
      identities_only="$(printf '%s\n' "$resolved_before" | awk '$1 == "identitiesonly" { print $2; exit }')"
      case "$identities_only" in yes|no) ;; *) printf 'STOP: invalid resolved IdentitiesOnly value\n' >&2; exit 1;; esac
      printf '  IdentitiesOnly %s\n' "$identities_only"
    else
      printf '  IdentityFile ~/.ssh/id_ed25519_euler\n  IdentitiesOnly yes\n'
    fi
    printf '  Port 22\n  ProxyCommand none\n  ProxyJump none\n  PreferredAuthentications publickey\n  PasswordAuthentication no\n  KbdInteractiveAuthentication no\n  ForwardAgent no\n'
  } > "$euler_temporary"
  chmod 600 "$euler_temporary"
  ssh -F "$euler_temporary" -G euler >/dev/null || {
    rm -f "$euler_temporary"
    printf 'STOP: generated Euler block is invalid\n' >&2
    exit 1
  }

  include='Include ~/.ssh/passport.d/*.conf'; temporary="$config.passport-new"
  if [ -f "$config" ]; then
    awk -v include="$include" 'BEGIN { print include } /^[[:space:]]*Include[[:space:]]+(~\/[.]ssh\/)?passport[.]d\/[*]([.]conf)?[[:space:]]*$/ { next } { print }' "$config" > "$temporary"
  else
    printf '%s\n' "$include" > "$temporary"
  fi
  chmod 600 "$temporary"
  ssh -F "$temporary" -G euler >/dev/null || {
    rm -f "$euler_temporary" "$temporary"
    printf 'STOP: generated SSH config is invalid; the original files are unchanged\n' >&2
    exit 1
  }

  if ! mv "$euler_temporary" "$euler_config" || ! mv "$temporary" "$config" || ! ssh -G euler >/dev/null; then
    rm -f "$euler_temporary" "$temporary"
    if restore_originals; then
      printf 'STOP: install failed; the original SSH files were restored automatically\n' >&2
    else
      printf 'STOP: install failed and automatic restore was incomplete. Restore only config.%s and euler.conf.%s from %s\n' "$stamp" "$stamp" "$backup_dir" >&2
    fi
    exit 1
  fi
)
```

**Expected:** The command finishes without a config error. A working existing identity is retained, or the tested canonical private key is selected. Prior files have timestamped backups, and a failed final install restores them automatically.

**Continue when:** Display the resolved settings.

**If not:** Do not append another host block. The command restores the original files after an install failure. If it reports an incomplete restore, use only the two timestamped files it names; otherwise open the sanitized error through the Passport help link.

### 10. Verify the resolved SSH fields

**Where:** Your computer

Display the target, port, username, identity files, authentication methods, proxy state, and agent-forwarding setting that OpenSSH will actually use.

**Run on Windows - PowerShell:**

```powershell
ssh -G euler | Select-String '^(hostname|port|user|identityfile|identitiesonly|preferredauthentications|passwordauthentication|kbdinteractiveauthentication|proxycommand|proxyjump|forwardagent) '
```

**Run on macOS - zsh:**

```zsh
ssh -G euler | grep -E '^(hostname|port|user|identityfile|identitiesonly|preferredauthentications|passwordauthentication|kbdinteractiveauthentication|proxycommand|proxyjump|forwardagent) '
```

**Run on Linux - Bash:**

```bash
ssh -G euler | grep -E '^(hostname|port|user|identityfile|identitiesonly|preferredauthentications|passwordauthentication|kbdinteractiveauthentication|proxycommand|proxyjump|forwardagent) '
```

**Expected:** hostname is euler.ethz.ch; port is 22; user is the short ETH username; no identityfile ends in .pub; preferredauthentications is publickey; passwordauthentication and kbdinteractiveauthentication are no; forwardagent is no; no proxycommand or proxyjump line is present. A generated canonical setup also shows id_ed25519_euler and identitiesonly yes.

**Continue when:** Run the final alias test.

**If not:** Stop and correct only passport.d/euler.conf. Keep unrelated SSH hosts and backup files unchanged.

### 11. Prove the alias is key-only

**Where:** Your computer

Run the alias with ETH-password and keyboard-interactive fallback disabled. A prompt for the local key passphrase is allowed.

**Run on Windows - PowerShell:**

```powershell
ssh -o PreferredAuthentications=publickey -o PasswordAuthentication=no -o KbdInteractiveAuthentication=no euler "echo config-ok"
```

**Run on macOS - zsh:**

```zsh
ssh -o PreferredAuthentications=publickey -o PasswordAuthentication=no -o KbdInteractiveAuthentication=no euler "echo config-ok"
```

**Run on Linux - Bash:**

```bash
ssh -o PreferredAuthentications=publickey -o PasswordAuthentication=no -o KbdInteractiveAuthentication=no euler "echo config-ok"
```

**Expected:** Euler prints exactly config-ok without asking for the ETH password.

**Continue when:** Enter config-ok in the confirmation field and run Check my work.

**If not:** Stop. Use the resolved fields and direct key-only result to diagnose the alias.

### 12. Configure euler-tunnel only after config-ok

**Where:** Your computer

If you need VS Code on an allocated compute node, follow the separate euler-tunnel procedure now. It depends on the working euler alias.

- [Open the euler-tunnel procedure](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/euler/euler-tunnel.md)

**Expected:** The direct euler alias already prints config-ok.

**Continue when:** Proceed to euler-tunnel or finish this mission.

**If not:** Return to the failed SSH step; do not debug the tunnel first.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. The local verifier checks only the
mission activity above. A score of 100% is required, and every
safety-critical question must be correct. Failed attempts provide targeted
feedback and can be retried without penalty.

## If Blocked

Stop at the first failed gate. Do not regenerate repeatedly, overwrite keys,
replace the whole SSH config, or loosen permissions broadly. Use
[Euler SSH troubleshooting](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/euler/troubleshooting.md)
and share only the exact error plus sanitized `ssh -G` fields.

Useful references:

- [Access And Ssh](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/euler/access-and-ssh.md)
- [Euler troubleshooting](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/euler/troubleshooting.md)

## Understand Before Accepting AI Output

Inspect every path and backup before accepting an SSH repair. A `.pub` file in
`IdentityFile`, concatenated host blocks, or PowerShell pasted into Euler Bash
are configuration errors, not reasons to delete all SSH state.

## Finish And Continue

When **Check my work** passes, use **Submit mission** once. The launcher
publishes only this mission's generated, sanitized submission. Continue when the
dashboard shows the trusted result; a local check alone is not a pass.
