# Mission: Choose And Configure An AI Access Route

## Outcome

Choose and configure one AI coding route by identifying its model, access provider, agent, and editor. Keep credentials private and do not assume that the lab pays for the service.

## Concept

An AI setup contains several parts. A model generates text. A provider or gateway supplies API access and billing. An agent uses the model while reading files or requesting tools. The editor or terminal is the interface where you control it; MCP or ACP may connect additional tools.

Choose the complete access route, not only a model name. Account ownership, cost limits, permissions, and data rules still apply independently.

## Worked Example

The components are classified correctly and no credential appears in a file, prompt, screenshot, or Git diff.

Check these points:

- **What is OpenRouter in this stack?** A provider or gateway for model access, routing, billing, and limits.
- **Where may an API key be stored?** In the supported operating-system keychain or approved secret store.

## Common Trap

Calling OpenRouter an agent, confusing a model with an IDE, or pasting an API key into settings tracked by Git.

## Your Action

Configure one AI route, open only the synthetic practice repository, and prove that a read-only request changes no file.

**Follow these steps in order.** An AI model, access provider, coding agent, and editor are separate parts. Identify them first. Use the no-cost Copilot Student route if eligible; any personal paid service remains your financial responsibility.

### 1. Identify the components

**Where:** This browser

Identify each part of the setup: the model generates a response; the provider or gateway supplies access and billing; the agent can read files or request tools; the editor or terminal is the interface; MCP or ACP may connect extra tools. For example, OpenRouter is a gateway, not the coding agent.

- [Read agents and interfaces](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/ai/agents-and-interfaces.md)

**Expected:** You can name the role of every component in the chosen setup.

**Continue when:** Choose one access route.

**If not:** Do not configure credentials until the billing path and agent are clear.

### 2. Choose the access route

**Where:** This browser

Use exactly one route. Eligible students use VS Code with GitHub Copilot Student. If you deliberately choose Zed with a personal OpenRouter account, skip the two Copilot-only steps and follow the linked Zed procedure. Use another route only when its owner has supplied written setup, data, cost, and permission rules. If no route is available, leave this mission pending and continue the non-AI missions.

- [Compare supported AI routes](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/ai/README.md)

**Expected:** You have selected one route and can name its account owner, payer, editor, and agent interface.

**Continue when:** Follow only the selected route below.

**If not:** Leave this mission pending and continue manually. Do not create a paid account merely to pass.

### 3. Copilot route: activate the Student benefit

**Where:** This browser

Do this step only for the Copilot route. After GitHub Education approval, open Education benefits. If Copilot Student is already active, keep it. Otherwise select the Copilot Student activation offered by GitHub. If GitHub asks for payment or a payment method, stop; payment is not required for this route.

- [Open Education benefits](https://github.com/settings/education/benefits)

- [Read Copilot Student setup](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/ai/vscode-copilot-student.md)

**Expected:** GitHub identifies the Student benefit without a paid checkout.

**Continue when:** Continue to the Copilot VS Code step. Zed users skip to the Zed step.

**If not:** Continue manual onboarding while verification is pending; do not purchase access to pass.

### 4. Copilot route: connect VS Code

**Where:** Your computer

Do this step only for the Copilot route. Install or open VS Code. Open Extensions, install GitHub Copilot from publisher GitHub if it is absent, then select the Copilot icon, choose Use AI Features, and sign in with the same GitHub account used for the Passport. If more than one GitHub account is present, use the Accounts menu to select the intended account for Copilot.

- [Download VS Code](https://code.visualstudio.com/)

- [Follow the IDEAL Lab VS Code setup](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/onboarding_IT_guides/vscode.md)

**Expected:** VS Code shows the intended GitHub account and opens its Chat or Agent interface.

**Continue when:** Continue to Prepare the synthetic practice repository.

**If not:** Use the Accounts menu to select the intended account. Do not purchase a plan or grant unexplained access to pass this mission.

### 5. Zed route: follow the personal OpenRouter procedure

**Where:** This browser

Do this step only for the Zed route; Copilot users skip it. Follow the linked procedure from start to finish: create a separate personal key, set a low key limit before use, and enter it only through Zed's provider UI so the operating-system keychain stores it. The lab does not provide credits, reimburse charges, or accept liability for personal usage or loss.

- [Read the optional Zed and OpenRouter procedure](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/ai/zed-openrouter.md)

**Expected:** For the Zed route, a dedicated limited key is stored outside files and Git. For the Copilot route, this step is skipped.

**Continue when:** Continue to Prepare the synthetic practice repository.

**If not:** Revoke an exposed key and stop requests until account activity is understood.

### 6. Open the synthetic practice repository

**Where:** Your computer

Press Prepare practice folder, run the displayed enter-folder command, and open that exact folder in the editor configured above. Check the editor title or file tree before opening the agent. Do not use a research repository for this test.

**Expected:** The editor is open at the Passport practice repository and the terminal is at its root.

**Continue when:** Run the read-only prompt.

**If not:** Run gh passport doctor; do not substitute another repository or create a second clone.

### 7. Run a read-only agent check

**Where:** Your computer

Start a new agent chat for the open practice repository and paste the prompt below. Do not approve an edit or terminal command.

**Paste this into the agent:**

```text
Read the repository instructions and list the top-level files and folders you can see. Do not edit files, run terminal commands, install software, or access anything outside this repository. Tell me when you are finished.
```

**Expected:** The response refers to files that exist in the practice repository and no edit or command was attempted.

**Continue when:** Verify the working tree yourself.

**If not:** Stop the agent and inspect every action it attempted.

### 8. Verify that configuration changed no project file

**Where:** Your computer

Run the scoped Git status command at the practice-repository root. It checks the AI fixture and common editor or credential-file locations without confusing this mission with unfinished files from another exercise.

**Run on Windows - PowerShell:**

```powershell
git status --short -- workspace/agent_task .vscode .zed .env .env.local
```

**Run on macOS - zsh:**

```zsh
git status --short -- workspace/agent_task .vscode .zed .env .env.local
```

**Run on Linux - Bash:**

```bash
git status --short -- workspace/agent_task .vscode .zed .env .env.local
```

**Expected:** The command prints nothing: no AI fixture, editor setting, transcript, or credential file changed.

**Continue when:** Complete the questions and run Check my work.

**If not:** Do not commit the change; remove it safely and rotate any exposed credential.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use **Check my work** before submitting. The local verifier checks only the
mission activity above. A score of 100% is required, and every
safety-critical question must be correct. Failed attempts provide targeted
feedback and can be retried without penalty.

## If Blocked

Use the offline route. Purchasing access is never a recovery requirement. For
technical symptoms, use [AI-agent troubleshooting](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/troubleshooting/ai-agents.md).

Useful references:

- [AI coding agents](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/ai/README.md)
- [Vscode Copilot Student](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/ai/vscode-copilot-student.md)
- [Zed Openrouter](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/ai/zed-openrouter.md)
- [Cost Context And Failures](https://github.com/IDEALLab/onboarding-IT/blob/docs/llm-agent-overhaul/docs/reference/ai/cost-context-and-failures.md)

## Understand Before Accepting AI Output

Budget limits reduce financial exposure but do not prove data approval,
correctness, or safe execution. You remain responsible for charges on a
personal account and for every accepted command and diff.

## Finish And Continue

When **Check my work** passes, use **Submit mission** once. The launcher
publishes only this mission's generated, sanitized submission. Continue when the
dashboard shows the trusted result; a local check alone is not a pass.
