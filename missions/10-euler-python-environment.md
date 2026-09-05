# Mission: Create A Small Python Environment On Euler

## Outcome

Create or safely reuse a small Python environment on Euler and know how to
activate it inside a Slurm script.

## Concept

A Python environment contains operating-system-specific executables and paths.
The environment on your laptop cannot be copied to Euler. Recreate it on Euler
from a reviewed project definition, and make each batch script establish its
own software context.

## Worked Example

The training environment uses the documented Euler Python module, lives in the
dedicated training folder under `$HOME`, and prints `euler-python-env-ok` after
its path and version are verified.

Check these points:

- **Can a laptop `.venv` be copied to Euler?** No; recreate it on Euler.
- **Where does activation happen for a job?** Inside the Slurm script.

## Common Trap

Copying `.venv` from another machine, installing into a shared base
environment, or activating Python only in the login shell and assuming the job
will reproduce that setup.

## Your Action

Create or safely reuse one small Euler-native Python virtual environment and verify how a Slurm job activates it.

**Follow these steps in order.** Your laptop environment and Euler environment are separate. Run these steps on Euler after the SSH mission prints config-ok. This exercise creates no Slurm job and installs no project package.

### 1. Connect to Euler

**Where:** Your computer

From the local terminal, connect with the verified euler alias. Run every later command in the Euler Bash shell that opens.

**Run on Windows - PowerShell:**

```powershell
ssh euler
```

**Run on macOS - zsh:**

```zsh
ssh euler
```

**Run on Linux - Bash:**

```bash
ssh euler
```

**Expected:** The prompt changes to an Euler login node.

**Continue when:** Check the documented Python module.

**If not:** Return to the SSH mission. Do not run Euler commands in the local shell.

### 2. Check the Euler Python module

**Where:** Euler login node

Load the dated Euler software stack used by this training release and verify the interpreter before creating anything. This affects only the current shell.

**Run on Euler - Bash:**

```bash
(
set -eu
module purge
module load stack/2024-06 python/3.11.6
version="$(python --version 2>&1)"
printf '%s\n' "$version"
[ "$version" = "Python 3.11.6" ] || { printf 'STOP: expected Python 3.11.6, got %s\n' "$version" >&2; exit 1; }
printf 'module-python-ok\n'
)
```

- [Euler Python environment reference](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/euler/python-environments.md)

**Expected:** The final two lines are Python 3.11.6 and module-python-ok.

**Continue when:** Inspect the dedicated environment path.

**If not:** Run module spider python and use the help path with its non-secret output. Do not guess a replacement module.

### 3. Inspect before creating

**Where:** Euler login node

Check the exact training path without changing it. A valid existing environment is kept. A symbolic link, incomplete directory, or different Python version stops the recipe instead of being replaced.

**Run on Euler - Bash:**

```bash
(
set -eu
venv="$HOME/passport-euler/venvs/passport-python"
if [ -L "$venv" ]; then
  printf 'STOP: %s is a symbolic link; nothing was changed.\n' "$venv" >&2
  exit 1
elif [ ! -e "$venv" ]; then
  printf 'environment-target-available\n'
elif [ -d "$venv" ] && [ -x "$venv/bin/python" ]; then
  version="$("$venv/bin/python" -c 'import platform; print(platform.python_version())')"
  [ "$version" = "3.11.6" ] || { printf 'STOP: existing environment uses Python %s; nothing was changed.\n' "$version" >&2; exit 1; }
  printf 'existing-environment-ok\n'
else
  printf 'STOP: %s exists but is not a complete environment; nothing was changed.\n' "$venv" >&2
  exit 1
fi
)
```

**Expected:** The final line is environment-target-available or existing-environment-ok.

**Continue when:** Create only when absent, otherwise reuse it.

**If not:** Do not delete or rename the existing path. Use the help route to identify its owner and purpose.

### 4. Create or reuse the environment

**Where:** Euler login node

Run this after the inspection passes. The command creates into a private temporary directory and moves it into place only after Python and pip work. If the valid target already exists, it is reused without modification.

**Run on Euler - Bash:**

```bash
(
set -eu
umask 077
module purge
module load stack/2024-06 python/3.11.6
root="$HOME/passport-euler"
base="$root/venvs"
venv="$base/passport-python"
[ ! -L "$root" ] && [ ! -L "$base" ] || { printf 'STOP: a training parent path is a symbolic link.\n' >&2; exit 1; }
mkdir -p "$base"
if [ -L "$venv" ]; then
  printf 'STOP: environment target is a symbolic link.\n' >&2
  exit 1
elif [ -e "$venv" ]; then
  [ -d "$venv" ] && [ -x "$venv/bin/python" ] || { printf 'STOP: existing target is incomplete.\n' >&2; exit 1; }
  version="$("$venv/bin/python" -c 'import platform; print(platform.python_version())')"
  [ "$version" = "3.11.6" ] || { printf 'STOP: existing environment uses Python %s.\n' "$version" >&2; exit 1; }
  printf 'existing-environment-kept\n'
else
  tmp="$(mktemp -d "$base/.passport-python.XXXXXX")"
  cleanup() { if [ -n "${tmp:-}" ] && [ -d "$tmp" ]; then rm -r -- "$tmp"; fi; }
  trap cleanup EXIT HUP INT TERM
  python -m venv "$tmp"
  "$tmp/bin/python" -m pip --version
  mv "$tmp" "$venv"
  tmp=''
  printf 'created-environment-ok\n'
fi
)
```

**Expected:** The command prints existing-environment-kept or created-environment-ok and does not overwrite an existing path.

**Continue when:** Activate and verify the exact interpreter.

**If not:** Keep the first error. Do not rerun with sudo, remove the target, or install packages into base.

### 5. Verify the active interpreter

**Where:** Euler login node

Activate the training environment, verify its exact path and Python version, then deactivate it. The marker is safe to enter in the Passport; do not paste the full private path into a submission.

**Run on Euler - Bash:**

```bash
(
set -eu
module purge
module load stack/2024-06 python/3.11.6
venv="$HOME/passport-euler/venvs/passport-python"
[ -d "$venv" ] && [ ! -L "$venv" ] && [ -x "$venv/bin/python" ] || { printf 'STOP: training environment is missing or unsafe.\n' >&2; exit 1; }
. "$venv/bin/activate"
python -c 'import pathlib, platform, sys; expected = pathlib.Path.home() / "passport-euler" / "venvs" / "passport-python"; assert pathlib.Path(sys.prefix) == expected; assert platform.python_version() == "3.11.6"; print("python_environment=passport-python"); print("euler-python-env-ok")'
python -m pip --version
deactivate
)
```

**Expected:** The output includes python_environment=passport-python, euler-python-env-ok, and pip from the same environment.

**Continue when:** Learn where these lines belong in a job.

**If not:** Stop and inspect the reported interpreter. Do not repair it by copying your laptop environment.

### 6. Put setup inside the Slurm script

**Where:** Euler login node

Read this batch-script fragment. Do not run a workload on the login node. Every Python job must load its module and activate its environment inside the submitted script before the Python command.

**Put this in the named Bash file:**

```bash
module purge
module load stack/2024-06 python/3.11.6
. "$HOME/passport-euler/venvs/passport-python/bin/activate"
python your_script.py
```

**Expected:** You can identify the three environment lines that must precede the program in a Slurm script.

**Continue when:** Complete the questions and confirmation.

**If not:** Do not rely on a login-shell activation to define an unattended job.

### 7. Confirm the safe marker

**Where:** Your computer

Return to the local Passport, enter only euler-python-env-ok, complete the questions, and run Check my work.

**Expected:** The local check accepts the exact environment marker and all three safety decisions.

**Continue when:** Submit once and continue to the first CPU job.

**If not:** Repeat only the verification step on Euler; do not recreate a working environment.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. The local verifier checks the exact
safe marker printed by the Euler environment command. A score of 100% is
required, and every safety-critical question must be correct.

## If Blocked

Keep the first non-secret error. Use `module spider python` if the dated module
cannot be loaded. Do not use `sudo`, delete an existing environment, copy a
laptop environment, or install into `base`. See the
[Euler Python environment reference](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/euler/python-environments.md).

## Understand Before Accepting AI Output

Personally verify the Python version, environment path, and the activation
lines in the batch script. An agent must not choose a different module, delete
an environment, or install packages without your review.

## Finish And Continue

When **Check my work** passes, use **Submit mission** once. Continue when the
dashboard shows the trusted result; a local check alone is not a pass.
