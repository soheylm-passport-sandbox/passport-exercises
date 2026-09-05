# Mission: Create A Reproducible Python Environment

## Outcome

Python is a programming language. Create a separate interpreter and package
set for one practice project, recreate it from a small definition file, and
keep computer-specific setup files out of shared Git history.

## Concept

Python is a programming language, and a Python interpreter is the program that runs Python files. Projects often require different package versions, so each project needs an isolated environment containing its own interpreter and packages.

Conda creates and manages such environments. Miniforge is the small Conda distribution used by this guide. Conda's shared `base` environment is not used for project packages. This mission stores the project environment in `.venv`; `.gitignore` tells Git not to record that local folder, while `environment.yml` records the reproducible definition.

## Worked Example

Python runs from the project .venv and Git reports that .venv is ignored.

Check these points:

- **Should .venv be committed?** No. It is reproducible local state and must remain ignored.
- **What proves the environment is active?** The reported interpreter path is inside the project .venv.

## Common Trap

Creating the environment in Git-tracked files or installing into an unrelated global interpreter.

## Your Action

Install or verify Miniforge, create the project environment from environment.yml, and prove that Git ignores .venv.

**Follow these steps in order.** Do not install packages into Conda's shared base environment or into the Python installation used by the operating system. Keep an existing .venv folder until you have identified what it contains.

**New to text commands?** A command is a line of text that tells a
computer to do one task. A terminal is the text application in which a
shell reads that command. Open PowerShell on Windows or the application
named Terminal on macOS or Linux. The application starts the correct
shell automatically; do not install a separate Bash or zsh application. Read
[Terminal and command basics](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/core/command-line-basics.md)
before continuing if these words are new.

### 1. Know what the Python environment contains

**Where:** This web page in your browser

Python is run by a program called an interpreter. Packages add reusable code. A project environment keeps one interpreter and package set separate from other projects. Conda manages environments, and Miniforge provides Conda. Conda's base environment is the shared default and is not used for project packages. environment.yml records what to recreate. .venv is the local project environment folder. .gitignore tells Git not to record named local files or folders.

- [Open the Python setup reference](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/onboarding_IT_guides/python_setup.md)

**Expected:** You can distinguish the versioned environment.yml definition from the local .venv installation.

**Continue when:** Prepare the Python practice folder.

**If not:** Do not install packages globally or into base until the terms are clear.

### 2. Prepare the Python practice folder

**Where:** The laptop or desktop in front of you

Press Prepare practice folder in this step and run the displayed enter-folder command. The repository root is the top-level project folder that contains files such as environment.yml and .gitignore. Keep all following commands there unless a step says otherwise.

**Expected:** The practice repository and practice branch are active.

**Continue when:** Check whether Conda is already available.

**If not:** Do not create another clone; run gh passport doctor.

### 3. Check Conda

**Where:** The laptop or desktop in front of you

Run the version check. If it succeeds, keep the existing working installation and skip installation.

**Open PowerShell on your Windows computer, then run:**

```powershell
conda --version
conda info --base
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
conda --version
conda info --base
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
conda --version
conda info --base
```

**Expected:** Conda prints a version and the base path of the installation that will manage this project environment.

**Continue when:** Skip installation and read the environment definition.

**If not:** Check for an existing installation in the next step. Do not install a second copy yet.

### 4. Recover an existing Conda installation

**Where:** The laptop or desktop in front of you

Run this only when conda was not recognized. The check looks only in common personal installation folders and does not delete anything. If it finds exactly one installation, it runs conda init for this operating system; that change becomes available only in a newly opened terminal. On Windows, also search the Start menu for Miniforge Prompt, Miniconda Prompt, or Anaconda Prompt. If one exists but this check found nothing, open that prompt, run conda info --base, and request help without including private information rather than installing another copy.

**Open PowerShell on your Windows computer, then run:**

```powershell
& {
  $Candidates = @(
    (Join-Path $env:USERPROFILE "miniforge3\Scripts\conda.exe"),
    (Join-Path $env:USERPROFILE "mambaforge\Scripts\conda.exe"),
    (Join-Path $env:USERPROFILE "miniconda3\Scripts\conda.exe"),
    (Join-Path $env:USERPROFILE "anaconda3\Scripts\conda.exe"),
    (Join-Path $env:LOCALAPPDATA "miniforge3\Scripts\conda.exe"),
    (Join-Path $env:ProgramData "miniforge3\Scripts\conda.exe")
  )
  $Found = @($Candidates | Where-Object { Test-Path -LiteralPath $_ } | Select-Object -Unique)
  $Found | ForEach-Object { Write-Host "found: $_" }
  if ($Found.Count -gt 1) { throw "STOP: multiple Conda installations found; choose one with setup help" }
  if ($Found.Count -eq 1) {
    $CondaExe = $Found[0]
    & $CondaExe --version
    & $CondaExe init powershell
    if ($LASTEXITCODE -ne 0) { throw "STOP: Conda initialization failed" }
    Write-Host "existing-conda-initialized"
  } else {
    Write-Host "no-common-conda-installation"
  }
}
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
(
found=''; count=0
for candidate in "$HOME/miniforge3/bin/conda" "$HOME/mambaforge/bin/conda" "$HOME/miniconda3/bin/conda" "$HOME/anaconda3/bin/conda"; do
  if [ -x "$candidate" ]; then found="$candidate"; count=$((count + 1)); printf 'found: %s\n' "$candidate"; fi
done
if [ "$count" -gt 1 ]; then printf 'STOP: multiple Conda installations found; choose one with setup help\n' >&2; exit 1; fi
if [ "$count" -eq 1 ]; then
  "$found" --version
  "$found" init zsh || { printf 'STOP: Conda initialization failed\n' >&2; exit 1; }
  printf 'existing-conda-initialized\n'
else
  printf 'no-common-conda-installation\n'
fi
)
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
(
found=''; count=0
for candidate in "$HOME/miniforge3/bin/conda" "$HOME/mambaforge/bin/conda" "$HOME/miniconda3/bin/conda" "$HOME/anaconda3/bin/conda"; do
  if [ -x "$candidate" ]; then found="$candidate"; count=$((count + 1)); printf 'found: %s\n' "$candidate"; fi
done
if [ "$count" -gt 1 ]; then printf 'STOP: multiple Conda installations found; choose one with setup help\n' >&2; exit 1; fi
if [ "$count" -eq 1 ]; then
  "$found" --version
  "$found" init bash || { printf 'STOP: Conda initialization failed\n' >&2; exit 1; }
  printf 'existing-conda-initialized\n'
else
  printf 'no-common-conda-installation\n'
fi
)
```

**Expected:** The final line is existing-conda-initialized or no-common-conda-installation.

**Continue when:** After existing-conda-initialized, skip installation and continue at Reopen and recheck Conda. After no-common-conda-installation, run only the installation step for this operating system.

**If not:** If more than one installation is listed, or a Start-menu Conda prompt exists at another path, stop and request help without including private information. Do not uninstall, rename, or overwrite any installation.

### 5. Install Miniforge on Windows only if needed

**Where:** The laptop or desktop in front of you

Run this step only after the recovery check printed no-common-conda-installation and no Conda prompt exists in the Start menu. Download the Windows x86-64 installer from the official page, run it for Just Me, keep the default personal installation folder and Start Menu shortcut, and leave Add Miniforge to PATH disabled. Open Miniforge Prompt from the Start menu, run conda --version, then run conda init powershell once. Close only that Miniforge Prompt, keep the terminal running the Passport open, and open a new PowerShell window.

- [Open official Miniforge installers](https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Windows-x86_64.exe)

**Expected:** conda --version works in Miniforge Prompt without replacing another Conda installation.

**Continue when:** Continue at Reopen and recheck Conda.

**If not:** Stop if an existing installation or destination is reported; diagnose it instead of overwriting it.

### 6. Install Miniforge on macOS only if needed

**Where:** The laptop or desktop in front of you

Run this step only after the recovery check printed no-common-conda-installation. The block downloads the official installer and its published SHA-256 checksum, a fingerprint used to detect a changed or damaged download. It checks that fingerprint before starting the interactive installer. Answer yes when asked to initialize zsh.

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

<!-- passport-snippet:miniforge-macos-installer -->
```zsh
(
set -eu
temporary="$(mktemp -d "${TMPDIR:-/tmp}/ideal-passport-miniforge.XXXXXX")"
installer="$temporary/Miniforge3.sh"
checksum="$temporary/Miniforge3.sh.sha256"
cleanup() { rm -f -- "$installer" "$checksum"; rmdir -- "$temporary" 2>/dev/null || true; }
trap cleanup EXIT HUP INT TERM
asset="Miniforge3-MacOSX-$(uname -m).sh"
printf 'Operating system: '; uname -s
printf 'Architecture: '; uname -m
command -v curl >/dev/null || { printf 'STOP: curl is unavailable; use the official installer link.\n' >&2; exit 1; }
curl -fL --output "$installer" "https://github.com/conda-forge/miniforge/releases/latest/download/$asset"
curl -fL --output "$checksum" "https://github.com/conda-forge/miniforge/releases/latest/download/$asset.sha256"
expected="$(awk '{print $1}' "$checksum")"
actual="$(shasum -a 256 "$installer" | awk '{print $1}')"
[ "$actual" = "$expected" ] || { printf 'STOP: checksum mismatch. Do not run the installer.\n' >&2; exit 1; }
printf 'checksum-ok\n'
bash "$installer"
)
```
<!-- /passport-snippet:miniforge-macos-installer -->

- [Open official Miniforge releases](https://github.com/conda-forge/miniforge/releases/latest)

**Expected:** The operating system is Darwin, the checksum matches, and installation finishes without replacing another Conda installation.

**Continue when:** Close this command terminal after the installer finishes, open a new Terminal window, and continue at Reopen and recheck Conda.

**If not:** If curl is unavailable, use the official release link and choose the MacOSX installer for this Mac's architecture. Stop if the architecture or destination is unclear; do not overwrite an existing Conda installation.

### 7. Install Miniforge on Linux only if needed

**Where:** The laptop or desktop in front of you

Run this step only after the recovery check printed no-common-conda-installation. The block downloads the official installer and its published SHA-256 checksum, a fingerprint used to detect a changed or damaged download. It checks that fingerprint before starting the interactive installer. Answer yes when asked to initialize Bash. Do not use sudo.

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

<!-- passport-snippet:miniforge-linux-installer -->
```bash
(
set -eu
temporary="$(mktemp -d "${TMPDIR:-/tmp}/ideal-passport-miniforge.XXXXXX")"
installer="$temporary/Miniforge3.sh"
checksum="$temporary/Miniforge3.sh.sha256"
cleanup() { rm -f -- "$installer" "$checksum"; rmdir -- "$temporary" 2>/dev/null || true; }
trap cleanup EXIT HUP INT TERM
asset="Miniforge3-$(uname -s)-$(uname -m).sh"
printf 'Operating system: '; uname -s
printf 'Architecture: '; uname -m
command -v curl >/dev/null || { printf 'STOP: curl is unavailable; use the official installer link.\n' >&2; exit 1; }
curl -fL --output "$installer" "https://github.com/conda-forge/miniforge/releases/latest/download/$asset"
curl -fL --output "$checksum" "https://github.com/conda-forge/miniforge/releases/latest/download/$asset.sha256"
expected="$(awk '{print $1}' "$checksum")"
actual="$(sha256sum "$installer" | awk '{print $1}')"
[ "$actual" = "$expected" ] || { printf 'STOP: checksum mismatch. Do not run the installer.\n' >&2; exit 1; }
printf 'checksum-ok\n'
bash "$installer"
)
```
<!-- /passport-snippet:miniforge-linux-installer -->

- [Open official Miniforge releases](https://github.com/conda-forge/miniforge/releases/latest)

**Expected:** The operating system is Linux, the checksum matches, and installation finishes without replacing another Conda installation.

**Continue when:** Close this command terminal after the installer finishes, open a new Terminal window, which normally starts Bash, and continue at Reopen and recheck Conda.

**If not:** If curl is unavailable, use the official release link and choose the Linux installer for this computer's architecture. Stop if the architecture or destination is unclear; do not use sudo or overwrite another Conda installation.

### 8. Reopen and recheck Conda

**Where:** The laptop or desktop in front of you

If Conda already worked in the first check, keep this terminal. If you initialized or installed Conda, close only the terminal used for the setup commands, leave the terminal running the Passport open, and open a new PowerShell window on Windows or Terminal window on macOS or Linux. On Linux, Terminal normally starts Bash. Run the enter-folder command shown in Prepare the Python practice folder, then run both checks below.

**Open PowerShell on your Windows computer, then run:**

```powershell
conda --version
conda info --base
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
conda --version
conda info --base
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
conda --version
conda info --base
```

**Expected:** Conda prints a version and one base installation path without a command-not-found error.

**Continue when:** Keep this terminal open and continue to the environment definition.

**If not:** Do not install another copy. On Windows, try Miniforge Prompt and run conda info --base. On any platform, request help with the command-not-found message and the base path already found; do not include your username or full home path.

### 9. Read the environment definition

**Where:** The laptop or desktop in front of you

Open environment.yml at the practice repository root. This versioned file selects conda-forge, uses nodefaults so personal Conda settings cannot add another package channel, and pins Python 3.11. Do not edit it in this exercise.

**Open PowerShell on your Windows computer, then run:**

```powershell
Get-Content -LiteralPath environment.yml
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
cat environment.yml
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
cat environment.yml
```

**Expected:** The file names conda-forge, nodefaults, and Python 3.11, and it contains no machine-specific path.

**Continue when:** Inspect the .venv target before creating it.

**If not:** Return to Prepare practice folder if environment.yml is missing or changed; do not invent a replacement.

### 10. Inspect the environment path

**Where:** The laptop or desktop in front of you

Check whether .venv already exists before creating anything. A symbolic link is a path that redirects to another file or folder; this recipe will not follow one. A normal project folder using Python 3.11 is kept. A link, incomplete environment, or different Python version stops the recipe; nothing is deleted.

**Open PowerShell on your Windows computer, then run:**

```powershell
& {
  if (Test-Path -LiteralPath .venv) {
    $Target = Get-Item -Force -LiteralPath .venv
    if (($Target.Attributes -band [IO.FileAttributes]::ReparsePoint) -ne 0) { throw "STOP: .venv is a link or reparse point; nothing was changed" }
    if (-not $Target.PSIsContainer) { throw "STOP: .venv exists but is not a directory; nothing was changed" }
    conda list --prefix ./.venv | Out-Null
    if ($LASTEXITCODE -ne 0) { throw "STOP: .venv is not a readable Conda environment" }
    $Python = Join-Path $Target.FullName "python.exe"
    if (-not (Test-Path -LiteralPath $Python -PathType Leaf)) { throw "STOP: .venv has no Python interpreter" }
    & $Python -I -c "import sys; assert sys.version_info[:2] == (3, 11)"
    if ($LASTEXITCODE -ne 0) { throw "STOP: existing .venv does not use Python 3.11" }
    Write-Host "existing-conda-environment"
  } else {
    Write-Host "ready-to-create"
  }
}
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
(
if [ -L .venv ]; then
  printf 'STOP: .venv is a symbolic link; nothing was changed\n' >&2
  exit 1
elif [ -e .venv ]; then
  [ -d .venv ] && [ -x .venv/bin/python ] || { printf 'STOP: .venv is not a complete environment; nothing was changed\n' >&2; exit 1; }
  conda list --prefix ./.venv >/dev/null || { printf 'STOP: .venv is not a readable Conda environment\n' >&2; exit 1; }
  .venv/bin/python -I -c 'import sys; assert sys.version_info[:2] == (3, 11)' || { printf 'STOP: existing .venv does not use Python 3.11\n' >&2; exit 1; }
  printf 'existing-conda-environment\n'
else
  printf 'ready-to-create\n'
fi
)
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
(
if [ -L .venv ]; then
  printf 'STOP: .venv is a symbolic link; nothing was changed\n' >&2
  exit 1
elif [ -e .venv ]; then
  [ -d .venv ] && [ -x .venv/bin/python ] || { printf 'STOP: .venv is not a complete environment; nothing was changed\n' >&2; exit 1; }
  conda list --prefix ./.venv >/dev/null || { printf 'STOP: .venv is not a readable Conda environment\n' >&2; exit 1; }
  .venv/bin/python -I -c 'import sys; assert sys.version_info[:2] == (3, 11)' || { printf 'STOP: existing .venv does not use Python 3.11\n' >&2; exit 1; }
  printf 'existing-conda-environment\n'
else
  printf 'ready-to-create\n'
fi
)
```

**Expected:** The final line is ready-to-create or existing-conda-environment. An existing environment has been confirmed as a real directory using Python 3.11.

**Continue when:** Verify the Git ignore rule before creating or reusing the environment.

**If not:** Stop if the path is a link, incomplete, unreadable, or uses another Python version. Identify who created it before removing or replacing anything.

### 11. Verify the environment path is ignored

**Where:** The laptop or desktop in front of you

Ask Git whether the future .venv contents are excluded before creating anything there. --no-index makes the check work even when the path does not exist yet.

**Open PowerShell on your Windows computer, then run:**

```powershell
git check-ignore -v --no-index .venv/conda-meta/history
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
git check-ignore -v --no-index .venv/conda-meta/history
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
git check-ignore -v --no-index .venv/conda-meta/history
```

**Expected:** Git prints the .gitignore rule that covers .venv/.

**Continue when:** Create or reuse the environment.

**If not:** Stop and correct .gitignore before creating the environment or committing project files.

### 12. Create or reuse the project Conda environment

**Where:** The laptop or desktop in front of you

If the earlier path check printed existing-conda-environment, keep it and let this command report reused-conda-environment. Otherwise, create the project-local .venv from the committed environment.yml. Do not install packages into base and do not replace the definition with a manual package list.

**Open PowerShell on your Windows computer, then run:**

```powershell
& {
  if (Test-Path -LiteralPath .venv) {
    $Target = Get-Item -Force -LiteralPath .venv
    if (($Target.Attributes -band [IO.FileAttributes]::ReparsePoint) -ne 0 -or -not $Target.PSIsContainer) { throw "STOP: existing .venv is not a safe project directory" }
    conda list --prefix ./.venv | Out-Null
    if ($LASTEXITCODE -ne 0) { throw "STOP: existing .venv is not readable by Conda" }
    $Python = Join-Path $Target.FullName "python.exe"
    & $Python -I -c "import sys; assert sys.version_info[:2] == (3, 11)"
    if ($LASTEXITCODE -ne 0) { throw "STOP: existing .venv does not use Python 3.11" }
    Write-Host "reused-conda-environment"
  } else {
    conda env create --prefix ./.venv --file environment.yml -y
    if ($LASTEXITCODE -ne 0) { throw "STOP: Conda environment creation failed" }
  }
}
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
(
if [ -L .venv ]; then
  printf 'STOP: existing .venv is a symbolic link\n' >&2
  exit 1
elif [ -e .venv ]; then
  [ -d .venv ] && [ -x .venv/bin/python ] || { printf 'STOP: existing .venv is incomplete\n' >&2; exit 1; }
  conda list --prefix ./.venv >/dev/null || { printf 'STOP: existing .venv is not readable by Conda\n' >&2; exit 1; }
  .venv/bin/python -I -c 'import sys; assert sys.version_info[:2] == (3, 11)' || { printf 'STOP: existing .venv does not use Python 3.11\n' >&2; exit 1; }
  printf 'reused-conda-environment\n'
else
  conda env create --prefix ./.venv --file environment.yml -y
fi
)
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
(
if [ -L .venv ]; then
  printf 'STOP: existing .venv is a symbolic link\n' >&2
  exit 1
elif [ -e .venv ]; then
  [ -d .venv ] && [ -x .venv/bin/python ] || { printf 'STOP: existing .venv is incomplete\n' >&2; exit 1; }
  conda list --prefix ./.venv >/dev/null || { printf 'STOP: existing .venv is not readable by Conda\n' >&2; exit 1; }
  .venv/bin/python -I -c 'import sys; assert sys.version_info[:2] == (3, 11)' || { printf 'STOP: existing .venv does not use Python 3.11\n' >&2; exit 1; }
  printf 'reused-conda-environment\n'
else
  conda env create --prefix ./.venv --file environment.yml -y
fi
)
```

**Expected:** Conda creates .venv from environment.yml, or the final line is reused-conda-environment for the valid environment already present.

**Continue when:** Activate the environment.

**If not:** Read the first Conda or environment error. Do not rerun with administrator rights, follow a link target, or delete an unrelated environment.

### 13. Activate the project environment

**Where:** The laptop or desktop in front of you

Activate the environment by its local .venv folder path. Activation changes which Python this terminal uses; it does not change the project files.

**Open PowerShell on your Windows computer, then run:**

```powershell
conda activate ./.venv
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
conda activate ./.venv
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
conda activate ./.venv
```

**Expected:** The shell accepts the command without an activation error.

**Continue when:** Verify the interpreter path.

**If not:** Windows: open Miniforge Prompt and run conda init powershell. macOS: run conda init zsh. Linux Bash: run conda init bash. Run it once, close only that command terminal, keep the terminal running the Passport open, open a new command terminal, return to the practice root, and retry.

### 14. Verify the active interpreter

**Where:** The laptop or desktop in front of you

Print the executable path and Python version. The path, not only the prompt decoration, proves which environment is active.

**Open PowerShell on your Windows computer, then run:**

```powershell
python -c "import sys; print(sys.executable); print(sys.version)"
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
python -c "import sys; print(sys.executable); print(sys.version)"
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
python -c "import sys; print(sys.executable); print(sys.version)"
```

**Expected:** The executable path is inside the practice repository .venv directory and Python reports version 3.11.

**Continue when:** If you use an editor for Python, connect it to the same interpreter in the next step.

**If not:** Do not install packages until the interpreter path is correct.

### 15. Use the same interpreter in your editor

**Where:** The laptop or desktop in front of you

Terminal activation and editor selection are separate. If you use VS Code, open the practice repository, press Ctrl+Shift+P on Windows/Linux or Command+Shift+P on macOS, run Python: Select Interpreter, and choose the interpreter inside this repository's .venv folder. For another editor, use its Python interpreter setting and choose the same path printed in the previous step. If you run Python only from the terminal, no editor setting is required.

- [Read the VS Code Python environment instructions](https://code.visualstudio.com/docs/python/environments)

**Expected:** An editor in use names the repository .venv interpreter; terminal-only users keep the verified active terminal.

**Continue when:** Run Check my work.

**If not:** Keep using the verified terminal interpreter and correct the editor selection; do not install another Python or recreate the environment.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. This check runs on your computer and
checks only the practical work in this lesson. A score of 80% is required, and every
safety-critical question must be correct. Failed attempts provide targeted
feedback and can be retried without penalty.

## If Blocked

Do not repeatedly reinstall into `base`. Record `conda info --envs`, the Python
path, and the exact error without credentials. Use the
[reproducible Python lab](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/reproducible-python.md) or ask for
help before deleting an existing environment.

Useful references:

- [Python setup](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/onboarding_IT_guides/python_setup.md)
- [Reproducible Python](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/reproducible-python.md)

## Understand Before Accepting AI Output

An agent may suggest packages that are unnecessary, unmaintained, or fetched
from an unapproved source. Review dependency purpose and project declarations
before installation.

## Finish And Continue

When **Check my work** passes, use **Submit lesson** once. The launcher
publishes only this lesson's generated submission after private information is excluded. Continue when the
progress page shows the automatic GitHub result as passed; a check on your computer alone is not a pass.
