# Mission: Start And Resume Your Passport

## Outcome

Open the assigned Passport, understand where progress is stored, and reopen
the same Passport later.

## Concept

The passport uses several locations for different purposes. The local browser
remembers where you were, while the trusted GitHub check records whether a
submitted mission passed. A locally checked box is therefore not an official
result.

## Worked Example

The same route reopens locally, and GitHub stores the submitted completion result.

Check these points:

- **Which source proves that submitted work passed?** The trusted GitHub controller result for the submitted commit.
- **How do you reopen the real passport later?** Run gh passport open; the launcher uses its local registry.

## Common Trap

Treating a remembered browser page as proof that a mission passed.

## Your Action

Confirm that you are in your assigned local Passport, review your route, then prove that you can close and resume it.

**Follow these steps in order.** Do not submit anything from a curriculum preview. Complete each check before moving to the next one.

### 1. Confirm the page mode

**Where:** This browser

Read the banner at the top of the page. Your working copy must say that this is your local Passport. A page labelled Curriculum preview is only a public example.

**Expected:** The banner identifies your local Passport.

**Continue when:** Continue to your route.

**If not:** Return to How to start and launch your Passport before continuing.

### 2. Check your operating system

**Where:** This browser

Open the Passport dashboard and confirm that it names the computer platform you are actually using: Windows, macOS, or Linux.

**Expected:** The dashboard platform matches this computer.

**Continue when:** Continue to the assigned route.

**If not:** Stop before platform-specific work, submit one sanitized help request, and return later. Keep this Passport; do not create a second one or alter its files.

### 3. Review the assigned missions

**Where:** This browser

Read the mission list from top to bottom. Check that it covers your real responsibilities. Dependencies are added automatically.

**Expected:** You can explain why each optional track appears.

**Continue when:** Continue when the route matches your work.

**If not:** Use the sanitized help request if a required responsibility is missing or an irrelevant one was assigned.

### 4. Know where progress is stored

**Where:** This browser

Draft answers stay on this computer. Submitted receipts and the trusted completion result live on GitHub. A checked box in the browser alone is not an official pass.

**Expected:** You can distinguish a local draft from a trusted GitHub result.

**Continue when:** Continue to the resume test.

**If not:** Re-read the status explanation before submitting any mission.

### 5. Close and reopen the Passport

**Where:** Your computer

Close this browser tab. Return to the terminal that is running the Passport, press Ctrl+C once, and wait until the normal PowerShell or shell prompt returns. Then run the open command below from that prompt. Do not reinstall the extension or clone another repository.

**Run on Windows - PowerShell:**

```powershell
gh passport open
```

**Run on macOS - zsh:**

```zsh
gh passport open
```

**Run on Linux - Bash:**

```bash
gh passport open
```

**Expected:** The first local server stops, then the browser reopens the same Passport and route from a new local server.

**Continue when:** Return to this mission and run Check my work.

**If not:** If Ctrl+C does not return a prompt, open one new terminal. Run gh passport doctor there, then use the sanitized help path if the same Passport cannot be found.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. The local verifier checks only the
mission activity above. A score of 80% is required, and every
safety-critical question must be correct. Failed attempts provide targeted
feedback and can be retried without penalty.

## If Blocked

If `gh passport open` stops, run `gh passport doctor`. Keep only its non-secret
check names and statuses. Do not delete the Passport folder, regenerate SSH
keys, reset Git, or change file permissions.
Use **Request help without posting secrets** on the dashboard if the named
recovery step does not resolve the problem. The public issue is assigned to
the lab maintainer for asynchronous triage; nobody needs to be online when you
submit it.

Use the [glossary](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/glossary.md) when a term is unfamiliar.

Useful references:

- [Passport start page](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/README.md)
- [Glossary](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/glossary.md)

## Understand Before Accepting AI Output

An AI tool cannot determine which systems, project data, or responsibilities
your supervisor approved. Do not let it invent access, edit `passport.json`,
or claim that the trusted check passed when you did not observe that result.

## Finish And Continue

When **Check my work** passes, use **Submit mission** once. The launcher
publishes only this mission's generated, sanitized submission. Continue when the
dashboard shows the trusted result; a local check alone is not a pass.
