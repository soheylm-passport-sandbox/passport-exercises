# Mission: Protect Accounts And Secrets

## Outcome

Decide which sign-in information must stay secret. Keep or set up the required
account protections, then answer fictional scenarios. Do not submit any secret.

## Concept

An account is your personal identity at a service. A credential proves access;
keep its secret part private. A password manager encrypts unique passwords and
recovery information.
Two-factor authentication (2FA) asks for another proof after a password.
Keep an approved setup that already works; the steps below explain missing setup.

| Item | Boundary |
| --- | --- |
| Password, token, recovery code | Approved private secret store; never a public record |
| SSH private key | Stays private on its computer |
| SSH public key (the .pub file) | May be given to the named service |
| Example settings file | Setting names and fictional values only |

A token authorizes service access. An SSH key pair separates the public key
from the private proof. A passphrase is a password protecting the private-key file;
it does not make the file safe to share. Git's ignore rule prevents recording
selected files; it is not encryption or permission to disclose their contents.

## Learning Challenge

A fictional token has entered a public commit. Would deleting that file stop
someone using the token? Decide the containment action before the explanation.

## Worked Example

<details>
<summary>Why deleting the file is insufficient</summary>

Copies and history can retain it. The service must disable or replace the
exposed credential. Preserve evidence with credentials and private details removed and use the private reporting
route. This is a fictional decision; do not disable a healthy account to practise.

</details>

## Common Trap

Keep private keys private even when protected by a passphrase. Use fictional
values in example files.

## Your Action

Set up the minimum account protections, learn what may never be submitted, then answer the credential scenarios.

**Follow these steps in order.** Keep working approved protections. Set up only missing safeguards, then answer fictional scenarios. Publish no credential or recovery code.

### 1. Prepare an approved password manager

**Where:** This web page in your browser

A password manager is an encrypted application for storing unique passwords and recovery information. Keep a working approved password manager if you already use one. Otherwise, on a personal computer follow ETH's KeePass guidance and use KeePassXC; on an ETH-managed device ask the responsible IT support before installing software. Do not store ETH passwords in an unapproved cloud-hosted vault.

- [Read the ETH KeePass guidance](https://unlimited.ethz.ch/help/security/passwort-manager-keepass)

**Expected:** You have an approved private place for unique passwords and recovery codes, or you have requested installation help for a managed device.

**Continue when:** Enable GitHub two-factor authentication.

**If not:** Do not create plain-text password notes or reuse a password while waiting for support.

### 2. Enable GitHub two-factor authentication

**Where:** This web page in your browser

Two-factor authentication (2FA) asks for a second proof after your password. Open your personal GitHub password and authentication settings, enable 2FA, configure the recovery methods offered by GitHub, and store the recovery codes in the approved private location from the previous step. Never upload a recovery code to the Passport.

- [Open GitHub authentication settings](https://github.com/settings/security)

- [Read GitHub recovery-method guidance](https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication-recovery-methods)

**Expected:** GitHub reports that two-factor authentication is enabled and the recovery-code view is closed after secure storage.

**Continue when:** Continue to file-based secrets.

**If not:** Complete GitHub account recovery privately; never submit a recovery code as evidence.

### 3. Keep secrets outside Git

**Where:** This web page in your browser

Use the secret/public boundary above. Ignored means Git is configured not to record a file, not that the file is safe to share. An example environment file names settings without their real values. Keep working protections; do not revoke a healthy credential for this exercise.

**Expected:** No secret value is inside any file that Git is asked to record or share.

**Continue when:** Continue to the exposure procedure.

**If not:** Remove the value from the project files and any staged Git change, then rotate it if it may have been exposed.

### 4. Know the first response to exposure

**Where:** This web page in your browser

For the fictional exposure, decide what stops further credential use. In a real exposure, follow the private incident procedure immediately: revoke (disable) or rotate (replace) the affected credential, preserve evidence with credentials and private details removed and report. Deleting a message or Git version does not contain it. Do not perform a real revocation for the fictional question.

- [Open the incident and help procedure](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/core/incidents-and-help.md)

**Expected:** You can name the containment action for the fictional credential and the private reporting route.

**Continue when:** Complete the fictional scenarios without performing a real revocation.

**If not:** Stop using the affected account. Use the linked incident procedure to contact your supervisor or lab IT, ETH cyber incident support, or ETH High-Performance Computing (HPC) support, according to the affected system.

### 5. Complete the scenarios

**Where:** This web page in your browser

Answer every question below using the rules above. Treat every credential question as safety-critical.

**Expected:** All credential-critical answers are correct.

**Continue when:** Run Check my work.

**If not:** Read the feedback and retry; do not guess around a secret-handling rule.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. This check runs on your computer and
checks only the practical work in this lesson. A score of 100% is required, and every
safety-critical question must be correct. Failed attempts provide targeted
feedback and can be retried without penalty.

## If Blocked

If you suspect a real exposure, stop the exercise and follow
[Incidents and getting help](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/core/incidents-and-help.md). Do not
post the secret in a GitHub issue or ask an AI tool to inspect it.

Useful references:

- [Accounts And Security](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/core/accounts-and-security.md)
- [Incidents And Help](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/core/incidents-and-help.md)

## Understand Before Accepting AI Output

An AI-generated cleanup command may destroy evidence without revoking the
credential. Verify the issuing service, scope, and incident path yourself.

## Finish And Continue

When **Check my work** passes, use **Submit lesson** once. The launcher
publishes only this lesson's generated submission after private information is excluded. Continue when the
progress page shows the automatic GitHub result as passed; a check on your computer alone is not a pass.
