# IDEAL Lab IT Passport Exercises

This public repository contains fictional exercises and empty evidence files
for the IDEAL Lab IT and Research Computing Passport `1.2.0`.
It contains no student records, research data, credentials, or privileged
workflow.

## Start Or Resume

Do not clone this repository manually. Install the public GitHub CLI extension,
then let it create or reuse your personal fork, assessment branch, and draft
pull request:

```text
gh extension install soheylm-passport-sandbox/gh-passport --force --pin v0.2.0
gh passport start
```

After setup, run this command from your local `passport-exercises` folder:

```text
gh passport open
```

The browser remembers only local navigation. Your commits and the permanent
draft pull request are the submitted record. The private IDEAL Lab controller
publishes automatic checks on that pull request. A final reviewer is requested
only after all deterministic checks pass.

If no automatic check appears after 30 minutes, submit one
[public, non-secret passport help request](https://github.com/soheylm-passport-sandbox/passport-exercises/issues/new?template=passport-help.yml)
and return later. Do not create an empty commit to wake the controller.

## Public Content Rule

Pull requests in this repository are public. Your GitHub username is
necessarily visible through the fork and PR. Use only the fictional values
requested by each exercise. Never submit passwords, tokens, private keys,
recovery codes, ETH usernames or email addresses, student numbers, other
private identifiers, real logs, unpublished research data, screenshots
containing private information, or confidential project details.

If a real incident or possible secret appears, stop. Revoke the credential if
needed and use the lab's private incident channel instead of the pull request.

## Repository Boundaries

- `missions/` contains generated fallback instructions and is not editable.
- `evidence/` contains the short answers checked by the controller.
- `workspace/` contains bounded fictional files used by practical exercises.
- `passport-curriculum.json` is the launcher-readable route catalogue.
- `passport.example.json` documents the format; `gh passport start` creates
  your actual `passport.json` only on your assessment branch.

The canonical curriculum and handbook live in
[`IDEALLab/onboarding-IT`](https://github.com/IDEALLab/onboarding-IT).
