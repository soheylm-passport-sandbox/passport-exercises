# Mission: Protect Accounts And Secrets

## Outcome

You can protect GitHub and ETH access, distinguish public from private SSH-key
material, and respond safely if a credential is exposed.

## Why This Matters

Commands run under your identity. A leaked token or private key may provide
access to private repositories, research data, or shared compute even when no
password was disclosed.

## Before You Start

Read [Accounts and security](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/core/accounts-and-security.md). Keep
all passwords, recovery codes, tokens, private keys, and unpublished material
out of the evidence and this conversation.

## Machine And Shell

**Your computer - web browser.** Account settings are changed only on the
official service page reached through your own bookmark or typed address.

## Steps

1. Confirm that multi-factor authentication is enabled for GitHub.
2. Store recovery codes in an approved private password manager or other
   supervisor-approved secure location.
3. Confirm that you use your own account rather than a shared login.
4. Learn the SSH boundary: a file ending in `.pub` is intended to be copied;
   the matching file without `.pub` is private and must never be shared.
5. Work through this fictional scenario: a token appears in a Git commit.
   Decide how to revoke it, report it, preserve useful evidence, and replace it.

Deleting the visible line or rewriting Git history does not revoke a secret.
Containment starts by disabling the credential at its issuing service.

## Expected Result

Your account uses MFA, recovery material is stored privately, and your scenario
response starts with revocation and reporting rather than concealment or broad
destructive cleanup.

## Independent Verification

Without revealing any value, identify where GitHub reports MFA status. Point to
a fictitious pair of filenames and correctly identify which SSH-key file may be
copied.

## Evidence To Submit

Complete `evidence/core/accounts-secrets.md`. State safeguards and reasoning
only. Never paste a token, private key, recovery code, ETH password, or account
settings screenshot.

## If Blocked

If you suspect a real exposure, stop the exercise and follow
[Incidents and getting help](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/core/incidents-and-help.md). Do not
post the secret in a GitHub issue or ask an AI tool to inspect it.

## Understand Before Accepting AI Output

An AI-generated cleanup command may destroy evidence without revoking the
credential. Verify the issuing service, scope, and incident path yourself.

## Finish And Continue

Commit the sanitized scenario response. It accumulates for the final universal
core review, so you can continue without waiting after every reflective step.
