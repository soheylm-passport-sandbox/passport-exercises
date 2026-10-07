# Mission: Set Up One AI Coding Tool Safely

## Outcome

An AI coding tool can inspect project files and request actions. Configure one
for a read-only check on fictional files; no paid purchase is required to pass.

## Concept

An editor is the application where you read and change code. Its coding agent
requests tools; a model generates text in response. A provider or gateway supplies model access and billing.

| Chosen setup | Access/cost owner | Permission for this test |
| --- | --- | --- |
| VS Code/Copilot student route | Intended verified GitHub account and current included benefit | Read fictional practice files only |
| Optional Zed/OpenRouter route | Your personal account and charges | Same read-only boundary; no purchase obligation |

An extension is an add-on inside the editor. An application programming interface (API) key is a secret authorizing service use and spending. Keep API keys private and use only the supported secret store. The official questions include one gateway distinction: OpenRouter
is a provider/gateway, not the coding agent. You do not need to configure a tool protocol such as MCP or ACP for this test.

## Learning Challenge

The tool is configured, but its first response asks to install a package.
Would approving that satisfy this read-only request? Decide before acting.

## Worked Example

<details>
<summary>What a successful read-only check establishes</summary>

The response names files actually present, no edit or command was attempted,
and the independent limited Git status check is empty. This checks the exercise's
scope, not the whole computer. Use the intended verified account and stop at a
paid checkout. Unavailable access leaves this AI lesson pending while non-AI
work continues; a manual alternative is not an AI completion.

</details>

## Common Trap

Review permission before approving a proposed action. Keep keys in the
supported secret store.

## Your Action

Configure one AI coding tool, open only the fictional practice repository, and prove that a read-only request changes no file.

**Follow these steps in order.** Choose one setup. Use fictional practice files, approve no paid purchase for onboarding, and keep the request read-only.

**New to text commands?** A command is a line of text that tells a
computer to do one task. A terminal is the text application in which a
shell reads that command. Open PowerShell on Windows or the application
named Terminal on macOS or Linux. The application starts the correct
shell automatically; do not install a separate Bash or zsh application. Read
[Terminal and command basics](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/core/command-line-basics.md)
before continuing if these words are new.

### 1. Identify the components

**Where:** This web page in your browser

Use the chosen setup table above. The editor is where you review work; the agent can request tools; the model generates a response; its provider or gateway supplies access and billing. No tool protocol setup is required.

- [Read agents and interfaces](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/ai/agents-and-interfaces.md)

**Expected:** You can name the role of every component in the chosen setup.

**Continue when:** Choose one setup option.

**If not:** Do not configure credentials until the billing path and agent are clear.

### 2. Choose one setup option

**Where:** This web page in your browser

Choose one complete setup. Eligible students use VS Code/Copilot. Zed/personal OpenRouter is an optional paid alternative, not a purchase to pass. Other tools need written owner-approved data, cost and permission rules. If access is unavailable, leave this AI lesson pending and continue non-AI lessons; manual work does not award an AI pass.

- [Compare supported AI setup options](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/ai/README.md)

**Expected:** You have selected one option and can name its account owner, payer, editor, and agent interface.

**Continue when:** Follow only the selected option below.

**If not:** Leave this lesson pending and continue manually. Do not create a paid account merely to pass.

### 3. Copilot option: activate the Student benefit

**Where:** This web page in your browser

Do this step only for the Copilot option. After GitHub Education approval, open Education benefits. If Copilot Student is already active, keep it. Otherwise select the Copilot Student activation offered by GitHub. If GitHub asks for payment or a payment method, stop; payment is not required for this option.

- [Open Education benefits](https://github.com/settings/education/benefits)

- [Read Copilot Student setup](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/ai/vscode-copilot-student.md)

**Expected:** GitHub identifies the Student benefit without a paid checkout.

**Continue when:** Continue to the Copilot VS Code step. Zed users skip to the Zed step.

**If not:** Continue manual onboarding while verification is pending; do not purchase access to pass.

### 4. Copilot option: connect VS Code

**Where:** The laptop or desktop in front of you

Do this step only for the Copilot option. VS Code is the editor used here. An extension is an add-on installed inside the editor; GitHub Copilot is the coding-agent extension. Install or open VS Code. Open Extensions, install GitHub Copilot from publisher GitHub if it is absent, then select the Copilot icon, choose Use AI Features, and sign in with the same GitHub account used for the Passport. If more than one GitHub account is present, use the Accounts menu to select the intended account for Copilot.

- [Download VS Code](https://code.visualstudio.com/)

- [Follow the IDEAL Lab VS Code setup](https://github.com/IDEALLab/onboarding-IT/blob/main/onboarding_IT_guides/vscode.md)

**Expected:** VS Code shows the intended GitHub account and opens its Chat or Agent interface.

**Continue when:** Continue to Prepare the fictional practice repository.

**If not:** Use the Accounts menu to select the intended account. Do not purchase a plan or grant unexplained access to pass this mission.

### 5. Zed option: follow the personal OpenRouter procedure

**Where:** This web page in your browser

Only for the deliberately selected Zed alternative: follow the linked optional procedure, then return to Prepare practice folder here. Copilot users skip this step. Personal spending, loss and liability remain yours; the lab provides no credits or reimbursement. Enter a key only through the supported secret store, never a project file or prompt.

- [Optional paid alternative only: Zed/OpenRouter setup](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/ai/zed-openrouter.md)

**Expected:** For the Zed option, a dedicated limited key is stored outside files and Git. For the Copilot option, this step is skipped.

**Continue when:** Continue to Prepare the fictional practice repository.

**If not:** Revoke an exposed key and stop requests until account activity is understood.

### 6. Open the fictional practice repository

**Where:** The laptop or desktop in front of you

Press Prepare practice folder, run the displayed enter-folder command, and open that exact folder in the editor configured above. Check the editor title or file tree before opening the agent. Do not use a research repository for this test.

**Expected:** The editor is open at the Passport practice repository and the terminal is at its root.

**Continue when:** Run the read-only prompt.

**If not:** Run gh passport doctor; do not substitute another repository or create a second clone.

### 7. Run a read-only agent check

**Where:** The laptop or desktop in front of you

Start a new agent chat for the open practice repository and paste the prompt below. Do not approve an edit or terminal command.

**Paste this into the agent:**

```text
Read the repository instructions and list the top-level files and folders you can see. Do not edit files, run terminal commands, install software, or access anything outside this repository. Tell me when you are finished.
```

**Expected:** The response refers to files that exist in the practice repository and no edit or command was attempted.

**Continue when:** Verify the working tree yourself.

**If not:** Stop the agent and inspect every action it attempted.

### 8. Verify that configuration changed no project file

**Where:** The laptop or desktop in front of you

Run the existing limited Git status command at the practice repository root. An empty result means the named practice and common settings paths did not change; it is not an audit of every secret or service on your computer. Inspect any output before continuing.

**Open PowerShell on your Windows computer, then run:**

```powershell
git status --short -- workspace/agent_task .vscode .zed .env .env.local
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
git status --short -- workspace/agent_task .vscode .zed .env .env.local
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
git status --short -- workspace/agent_task .vscode .zed .env .env.local
```

**Expected:** This limited Git status prints nothing for the named paths; independently confirm the response attempted no edit or command.

**Continue when:** Confirm the read-only result you observed, then answer the two questions.

**If not:** Stop and inspect the named change; preserve intended manual work. If a credential was exposed, use the private incident procedure.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. This check runs on your computer and
checks only the practical work in this lesson. A score of 100% is required, and every
safety-critical question must be correct. Failed attempts provide targeted
feedback and can be retried without penalty.

## Learning Check

### Practise

Try an answer before opening the explanation. These questions are for
practice; they do not affect your progress.

1. The read-only request makes an agent propose a terminal install. Which action stays inside the lesson?

   - Approve it because the agent says it is needed.
   - Reject the install, stop the request and inspect the practice folder before retrying with the stated boundary.
   - Enable all future tool approvals to finish setup faster.

<details class="learning-explanation">
<summary>See an explanation</summary>

The request authorized reading fictional files, not installing software or running commands. Reject the extra action and inspect state independently. A model suggestion does not expand your permission.

</details>

## If Blocked

Use the offline route. Purchasing access is never a recovery requirement. For
technical symptoms, use [AI-agent troubleshooting](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/troubleshooting/ai-agents.md).

Useful references:

- [AI coding agents](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/ai/README.md)
- [Vscode Copilot Student](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/ai/vscode-copilot-student.md)
- [Zed Openrouter](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/ai/zed-openrouter.md)
- [Cost Context And Failures](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/ai/cost-context-and-failures.md)

## Understand Before Accepting AI Output

Budget limits reduce financial exposure but do not prove data approval,
correctness, or safe execution. You remain responsible for charges on a
personal account and for every accepted command and diff.

## Finish And Continue

When **Check my work** passes, use **Submit lesson** once. The launcher
publishes only this lesson's generated submission after private information is excluded. Continue when the
progress page shows the automatic GitHub result as passed; a check on your computer alone is not a pass.
