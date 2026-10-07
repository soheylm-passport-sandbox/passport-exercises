# Mission: Start And Resume Your Passport

## Outcome

Open the working Passport on this computer and reopen the same lesson list.
A public course preview lets you explore; it cannot save or submit work.

## Concept

The Passport itself runs locally. Its launcher starts a local server, a program
serving the page from your computer. A terminal is the application containing
a text prompt; a shell is the program reading its commands. No separate Bash
application is needed. Keep the server terminal open; use another for commands.

| What you see | Where it lives | What it establishes |
| --- | --- | --- |
| Draft answers | This computer | Work you can resume; no official pass |
| Submitted exercise | GitHub | The requested safe record awaiting assessment |
| Passed result | GitHub automatic Passport check | Official completion for that submission |

Git records file history; GitHub hosts shared code and review. NAS means
network-attached storage for approved durable shared data. Blade is a shared
remote Windows computer for graphical software. Euler is an ETH Zurich service
that schedules research calculations on managed computers. Later lessons teach their access separately.

## Learning Challenge

Close and reopen this Passport. Check that the lesson list returns before
answering the questions. An old browser address is not the way to start it.

## Worked Example

<details>
<summary>Why the old local address may stop working</summary>

Stopping the server closes that address, not the saved Passport. Run
`gh passport open` to start or reuse its process and open the current address.
Do not clone again or create a second learning record.

</details>

## Common Trap

Use a command terminal for lesson commands and wait for the official GitHub
result after submission.

## Your Action

Confirm that you are in your local Passport, review your assigned lessons, then prove that you can close and reopen it.

**Follow these steps in order.** Confirm local mode and this computer, then reopen the same Passport. A public preview cannot save or submit.

**New to text commands?** A command is a line of text that tells a
computer to do one task. A terminal is the text application in which a
shell reads that command. Open PowerShell on Windows or the application
named Terminal on macOS or Linux. The application starts the correct
shell automatically; do not install a separate Bash or zsh application. Read
[Terminal and command basics](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/core/command-line-basics.md)
before continuing if these words are new.

### 1. Confirm the page mode

**Where:** This web page in your browser

Read the banner at the top of the page. Your working copy must say that this is your local Passport. A page labelled Public course preview is only an example and cannot save or submit work.

**Expected:** The banner identifies your local Passport.

**Continue when:** Continue to the computer check.

**If not:** Return to How to start and launch your Passport before continuing.

### 2. Check your operating system

**Where:** This web page in your browser

Open the Passport progress page and confirm that it names the operating system on the computer in front of you: Windows, macOS, or Linux.

**Expected:** The operating system shown on the progress page matches this computer.

**Continue when:** Continue to the command basics.

**If not:** Stop before platform-specific work, submit one help request without private information, and return later. Keep this Passport; do not create a second one or alter its files.

### 3. Learn where commands run

**Where:** This web page in your browser

Use the machine and shell label above each command. Open PowerShell on Windows or Terminal on macOS/Linux. A terminal is the text application; a shell is the program inside it that reads commands. PowerShell, zsh and Bash are shells. You do not need to install a separate Bash or zsh application. Paste after the prompt, the cursor showing readiness, press Enter once and read the result. A path is a file or folder address. Keep the server terminal open; use another terminal for lesson commands.

- [Optional: terminal basics if the prompt is unfamiliar](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/core/command-line-basics.md)

**Expected:** You can distinguish a terminal from a shell and identify the machine named above a command.

**Continue when:** Continue to the system map.

**If not:** Reopen How to start and read Before step 1 before running any command.

### 4. Meet the systems used by the lab

**Where:** This web page in your browser

Use the system map above to distinguish code history, durable data, graphical software and scheduled computation. A CPU is the general-purpose processor; a GPU is an accelerator for compatible programs. Do not connect to any remote system in this step.

- [Optional: compare the lab systems](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/core/environments-overview.md)

**Expected:** You can state in one sentence what GitHub, NAS, Blade, and Euler are used for.

**Continue when:** Review why each lesson was assigned to you.

**If not:** Read the linked system map before choosing or removing a responsibility.

### 5. Review your assigned lessons

**Where:** This web page in your browser

Read the lesson list from top to bottom. Each lesson teaches and checks one practical skill. Related lessons are grouped by topic. The Passport automatically adds any earlier lessons needed for the work you selected. Check that the list covers what you expect to do in the lab.

**Expected:** You can explain why each optional group of lessons appears.

**Continue when:** Continue when the lesson list matches your work.

**If not:** Use the help request without private information if a required responsibility is missing or an irrelevant one was assigned.

### 6. Know where progress is stored

**Where:** This web page in your browser

Use the three progress states above. Check my work verifies locally; Submit lesson sends only the requested safe exercise record. Wait for the official GitHub result before treating a lesson as passed.

**Expected:** You can distinguish a local draft, a public submission record, and the automatic GitHub result.

**Continue when:** Continue to the resume test.

**If not:** Re-read the status explanation before submitting any lesson.

### 7. Close and reopen the Passport

**Where:** The laptop or desktop in front of you

The Passport page is provided by a small local server: a program running on this computer in the terminal you kept open. Close this browser tab. Return to that terminal. Hold the Ctrl key and tap C once; do not type the characters Ctrl+C. This asks the local server to stop. Wait until the normal PowerShell, zsh, or Bash prompt returns, then paste and run the open command below. Do not reinstall the extension or clone another repository.

**Open PowerShell on your Windows computer, then run:**

```powershell
gh passport open
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
gh passport open
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
gh passport open
```

**Expected:** The first local server stops, then the browser reopens the same Passport and lesson list from a new local server.

**Continue when:** Return to this lesson and select Check my work.

**If not:** If Ctrl+C does not return a prompt, open one new terminal. Run gh passport doctor there, then request help without including private information if the same Passport cannot be found.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. This check runs on your computer and
checks only the practical work in this lesson. A score of 80% is required, and every
safety-critical question must be correct. Failed attempts provide targeted
feedback and can be retried without penalty.

## Learning Check

### Practise

Try an answer before opening the explanation. These questions are for
practice; they do not affect your progress.

1. Tomorrow the old localhost browser bookmark does not open. How do you resume?

   - Create a new Passport and start over.
   - Run gh passport open on this computer; use the address it opens.
   - Change the saved URL until something loads.

<details class="learning-explanation">
<summary>See an explanation</summary>

The local address belongs to a running process. The launcher finds your saved Passport and starts or reuses that process; a stale address does not mean your progress was lost.

</details>

## If Blocked

If `gh passport open` stops, run `gh passport doctor`. Keep only its non-secret
check names and statuses. Do not delete the Passport folder, regenerate SSH
keys, reset Git, or change file permissions.
Use **Request help without posting secrets** on the progress page if the named
recovery step does not resolve the problem. The public issue is assigned to
the lab maintainer for asynchronous triage; nobody needs to be online when you
submit it.

Use the [glossary](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/glossary.md) when a term is unfamiliar.

Useful references:

- [Passport start page](https://github.com/IDEALLab/onboarding-IT/blob/main/README.md)
- [Glossary](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/glossary.md)

## Understand Before Accepting AI Output

An AI tool cannot determine which systems, project data, or responsibilities
your supervisor approved. Do not let it invent access, edit `passport.json`,
or claim that the trusted check passed when you did not observe that result.

## Finish And Continue

When **Check my work** passes, use **Submit lesson** once. The launcher
publishes only this lesson's generated submission after private information is excluded. Continue when the
progress page shows the automatic GitHub result as passed; a check on your computer alone is not a pass.
