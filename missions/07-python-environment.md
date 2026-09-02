# Mission: Create A Reproducible Python Environment

## Outcome

The training project runs in a dedicated environment whose dependencies are
declared in Git while the environment directory itself remains untracked.

## Why This Matters

Installing packages globally or into `base` makes projects interfere with one
another and prevents collaborators from reproducing the environment.

## Before You Start

Complete the manual Git mission. Install Miniforge using the current
[Python setup guide](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/onboarding_IT_guides/python_setup.md) if `conda`
is unavailable.

## Machine And Shell

**Windows computer - Miniforge Prompt or PowerShell initialized for Conda.**

**macOS/Linux computer - zsh or bash initialized for Conda.**

## Steps

From the passport repository, create and activate the dedicated environment:

```bash
conda create -n ideal-passport python=3.11 -y
conda activate ideal-passport
python --version
python -c "import sys; print(sys.executable)"
```

Open `workspace/python_project`. Install only the dependencies declared by its
tracked project file, then select the `ideal-passport` interpreter in the
editor. Do not commit Conda directories, `.venv`, caches, or generated output.

## Expected Result

Python reports the intended environment, the fixture imports successfully, and
`git status --short` does not show an environment directory.

## Independent Verification

Deactivate and reactivate the environment, then run the documented fixture
test. Confirm that a clean clone could identify required dependencies from a
tracked file rather than your machine state.

## Evidence To Submit

Complete `evidence/python/environment.md`. Sanitize home-directory components
from interpreter paths and do not include environment exports containing
credentials or private package indexes.

## If Blocked

Do not repeatedly reinstall into `base`. Record `conda info --envs`, the Python
path, and the exact error without credentials. Use the
[reproducible Python lab](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/labs/reproducible-python.md) or ask for
help before deleting an existing environment.

## Understand Before Accepting AI Output

An agent may suggest packages that are unnecessary, unmaintained, or fetched
from an unapproved source. Review dependency purpose and project declarations
before installation.

## Finish And Continue

Keep `ideal-passport` active for the next bounded Python change and verification
mission.
