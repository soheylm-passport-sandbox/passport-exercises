# Mission: Establish Safe Euler SSH Access

## Outcome

Password access is proven first, a dedicated passphrase-protected key is
created without overwriting existing keys, only its `.pub` file is installed,
key-only authentication succeeds, and a validated `euler` alias preserves
unrelated SSH configuration.

## Why This Matters

Generating keys cannot repair missing Euler entitlement or a wrong username.
Testing password access first separates account problems from key problems.
Dedicated filenames and backups prevent accidental damage to other SSH hosts.

## Before You Start

Confirm that your supervisor assigned the Euler CPU responsibility. Connect to
ETH VPN when required. Never paste an ETH password, private key, or public-key
contents into evidence or chat.

## Machine And Shell

Use only the block matching your local computer. A prompt beginning with an
Euler hostname uses Bash and must not receive PowerShell commands.

## Steps

First prove ordinary access.

**Windows computer - PowerShell**

```powershell
$EulerUser = Read-Host "ETH username"
ssh "$EulerUser@euler.ethz.ch" "hostname"
```

**macOS/Linux computer - zsh or bash**

```bash
printf 'ETH username: '
read -r euler_user
ssh "$euler_user@euler.ethz.ch" hostname
```

Enter the ETH password only into the local SSH prompt. If this fails, stop; a
new key cannot fix account access.

Create a dedicated key without overwriting files.

**Windows computer - PowerShell**

```powershell
$SshDir = Join-Path $env:USERPROFILE ".ssh"
$KeyPath = Join-Path $SshDir "id_ed25519_euler"
New-Item -ItemType Directory -Force $SshDir | Out-Null
if ((Test-Path $KeyPath) -or (Test-Path "$KeyPath.pub")) {
    Write-Host "STOP: an Euler key file already exists. Nothing was overwritten."
} else {
    ssh-keygen -t ed25519 -f $KeyPath -C "$env:USERNAME@euler"
}
```

**macOS/Linux computer - zsh or bash**

```bash
(
  set -eu
  key="$HOME/.ssh/id_ed25519_euler"
  mkdir -p "$HOME/.ssh"
  chmod 700 "$HOME/.ssh"
  if [ -e "$key" ] || [ -e "$key.pub" ]; then
    printf 'STOP: an Euler key file already exists. Nothing was overwritten.\n'
  else
    ssh-keygen -t ed25519 -f "$key" -C "$USER@euler"
  fi
)
```

Set a passphrase. Install only the `.pub` file and perform the key-only proof
using the exact platform block in
[Euler access and SSH](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/euler/access-and-ssh.md#3-install-only-the-public-key-on-euler).
The required proof disables password and keyboard-interactive fallback and must
print `key-ok`.

Finally run the guide's safe `euler` alias block. It validates and backs up an
existing config, uses `~/.ssh/config.d/euler.conf`, sets `ForwardAgent no`, and
does not replace unrelated hosts.

## Expected Result

The key-only test prints `key-ok`. Then:

```bash
ssh euler "echo config-ok"
```

prints `config-ok` after at most the key passphrase prompt. It must not ask for
the ETH password.

## Independent Verification

Run `ssh -G euler` locally and inspect `hostname`, `user`, `identityfile`, and
`identitiesonly`. The identity file must not end in `.pub`.

## Evidence To Submit

Complete `evidence/euler/access-ssh.md` with sanitized host and configuration
fields. Never include usernames if unnecessary, key contents, private paths,
passwords, verbose authentication logs, or `authorized_keys` contents.

## If Blocked

Stop at the first failed gate. Do not regenerate repeatedly, overwrite keys,
replace the whole SSH config, or loosen permissions broadly. Use
[Euler SSH troubleshooting](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/euler/troubleshooting.md)
and share only the exact error plus sanitized `ssh -G` fields.

## Understand Before Accepting AI Output

Inspect every path and backup before accepting an SSH repair. A `.pub` file in
`IdentityFile`, concatenated host blocks, or PowerShell pasted into Euler Bash
are configuration errors, not reasons to delete all SSH state.

## Finish And Continue

Do not configure `euler-tunnel` yet. Continue to a tiny batch CPU job so login
and compute-node behavior are understood first.
