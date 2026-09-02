# Mission: Start And Resume Your Passport

## Outcome

You can identify your assigned route, distinguish local navigation from
official assessment, submit the first evidence on the correct branch, and
reopen the passport later without searching through browser history.

## Why This Matters

The passport uses several locations for different purposes. The local browser
remembers where you were, GitHub records submitted work, the automatic check
reports objective results, and the controller queues the few decisions that
require human judgment. Mixing those roles can make unfinished work look
complete.

## Before You Start

Run `gh passport start` once, then keep that terminal running when the command
opens this page. The command creates or reuses your personal public exercise
fork, onboarding branch, and draft assessment pull request. At the top of the
browser, confirm that the strip says **Your local passport** and names your
onboarding branch. If it says **Curriculum preview**, return to the terminal,
enter your local `passport-exercises` folder, and run `gh passport open`.

## Machine And Shell

Use the local passport in your web browser. For the verification command, use
the same Windows PowerShell, macOS zsh, or Linux bash terminal from which you
ran `gh passport open`.

## Steps

1. On the passport dashboard, read the assigned responsibilities and mission
   sequence. If they do not match your work, do not edit `passport.json`. Open
   **Request help without posting secrets**, submit one sanitized request, and
   return later for the asynchronous response.
2. Open **Assessment pull request** from the dashboard and bookmark it. Keep
   that draft pull request open throughout onboarding. Do not merge or close it.
3. Return to the dashboard and select **Edit evidence on GitHub** for this
   mission.
4. Before typing, confirm that GitHub shows the branch
   `onboarding/<your-github-username>`. If it shows another branch, cancel the
   edit and run `gh passport doctor` in the local terminal.
5. Complete only the requested fields. Do not include passwords, tokens,
   recovery codes, private keys, protected research content, or broad logs.
6. Use the commit message `docs(passport): record orientation evidence` and
   commit directly to the displayed onboarding branch.
7. Return to the local dashboard. It may show that the automatic check is
   still pending; do not submit the same change again.

## Expected Result

The evidence commit appears on `onboarding/<your-github-username>`, the draft
assessment pull request remains open, and the local passport distinguishes
your last visited page from any result verified on GitHub.

## Independent Verification

In the terminal where the passport repository is open, run:

```text
git status --short --branch
```

The first line starts with `## onboarding/`. Close the browser tab, rerun
`gh passport open`, and confirm that the dashboard reopens without requiring a
new clone. Local navigation may remember this page, but only the GitHub result
may identify the officially current mission.

## Evidence To Submit

Complete `evidence/core/orientation.md`. Record the assigned responsibilities,
your operating system, the displayed assessment branch, and the difference
between local navigation and official completion. Do not include credentials
or unnecessary personal information.

## If Blocked

If the repository, pull request, or evidence link does not open, run
`gh auth status --hostname github.com` and confirm that it names the same
GitHub account as your personal fork. Then run
`gh passport doctor` and keep its non-secret check names and statuses. Do not
delete the folder, regenerate SSH keys, reset Git, or change file permissions.
Use **Request help without posting secrets** on the dashboard if the named
recovery step does not resolve the problem. The public issue is assigned to
the lab maintainer for asynchronous triage; nobody needs to be online when you
submit it.

Use the [glossary](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/glossary.md) when a term is unfamiliar.

## Understand Before Accepting AI Output

An AI tool cannot determine which systems, project data, or responsibilities
your supervisor approved. Do not let it invent access, change the assigned
branch, edit `passport.json`, or claim that GitHub accepted a commit you did
not verify.

## Finish And Continue

Wait for the automatic check on the submitted commit, then use
`gh passport open` and **Sync from GitHub**. The check is scheduled every 15
minutes and GitHub can start scheduled work later. Do not push a duplicate
commit merely because the result is not immediate. If the dashboard says
**Awaiting human review**, the controller has already requested it. Close the
passport and return later; no appointment or live handoff is required.
