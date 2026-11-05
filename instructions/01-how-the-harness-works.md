# 01 How the harness works

*About 15 minutes · Both tracks · Reading, then a short look around*

Before you use the harness on your project, it helps to know what it is, where things live, and what happens when you ask the assistant to do something. Nothing here is specific to one assistant: both tracks work the same way underneath.

## What it's for

An AI coding assistant can build a canvas app screen, a flow or a Copilot Studio topic in minutes. Quick isn't the same as accessible, lawful and on brand. The harness gives the assistant the council's standards as instructions it follows, and makes it check its own work at every step, so what it builds meets the same bar as the work of the council's best developers.

## Three repositories, and yours

```mermaid
flowchart LR
    template["lbbexley-app-template<br/>a stamp"] -- "Use this template, once" --> service["Your service repository<br/>where all your work happens"]
    service -- "follows, at a pinned release" --> standards["lbbexley-digital-standards<br/>owned by the Digital Team"]
    workshop["lbbexley-ai-build-workshop<br/>these instructions"] -. "you read" .-> service
```

| Repository | What it is | What you do with it |
|---|---|---|
| **Your service repository** | Your project: its requirements, design, plans, source, tests and compliance documents | Everything. You create it in exercise 02 |
| **lbbexley-app-template** | A stamp for new service repositories | Select **Use this template**, once. You never change it |
| **lbbexley-digital-standards** | The standards themselves: skills, guardrails, the standards check, and the check that runs on GitHub | Nothing directly. Your repository follows it, and you can propose changes (exercise 12) |
| **lbbexley-ai-build-workshop** | These instructions | Read them |

Every reference points one way: from your repository to the standards. The standards never need to know your project exists, and a new release never changes your checks until you choose to update.

## What happens when you ask the assistant for something

```mermaid
flowchart TD
    ask["You ask for a change"] --> plan["Plan on the strongest model<br/>skills: requirements, architect, plan"]
    plan --> approve{"You approve the plan"}
    approve --> build["Build on the everyday model,<br/>in the dev environment"]
    build -- "every change" --> check["Standards check<br/>problems go straight back"]
    check --> build
    build --> sync["The latest version comes<br/>into your repository"]
    sync --> gate["End-of-run check on a smaller model<br/>standards check on everything changed,<br/>then a review for what tools can't see"]
    gate -- "anything found" --> build
    gate -- "clean" --> save["The assistant commits and pushes it for you"]
    save --> github["GitHub runs the same checks again,<br/>whichever assistant made the change, or none"]
```

1. **Plan, on the strongest model.** The assistant writes down what it will do before it does it: the user need, the exact words people will read, and acceptance criteria someone can check. Nothing changes until you approve.
2. **Build, on the everyday model, in your dev environment.** The assistant builds the real thing with Microsoft's tools: the canvas app open in Power Apps Studio, the flow, the tables, the Power Pages site. It doesn't ask before each change in the dev environment. The standards check runs on everything it writes and sends every problem straight back to it.
3. **Bring in the latest version.** After a change in the dev environment, the assistant brings the latest version into your repository: the solution with `pac solution sync`, after adding any new flow or table to it, and a canvas app's source through Microsoft's canvas tools. Your repository holds the guidelines and the latest version: nobody edits the service's source there by hand.
4. **Check, on a smaller model.** Before the assistant can finish, the end-of-run check runs the standards check on everything that changed, and a reviewer looks for what rules can't catch, such as unclear wording or a missing test. It also notes ideas for improving the harness.
5. **Commit and push.** Once the check is clean, the assistant commits the latest version and pushes it to GitHub for you. In Claude Code the check asks it to; in Copilot you select **Commit the work**. You never need to run Git, make a branch or open a pull request.
6. **On GitHub.** Every push runs the Bexley standards check again. It doesn't depend on any assistant, so it's the backstop.

Along the way, guardrails stop the assistant doing things it shouldn't: working in any environment but your dev one, deleting Dataverse records, flows or connections, force-pushing, or (in Claude Code) receiving a prompt with real-looking personal data in it.

## How each assistant gets the standards

| | Claude Code | GitHub Copilot |
|---|---|---|
| Skills (brand, accessibility, content style, the legal duties, one per platform, and requirements, architect, plan, review, improve, sync) | The **lbbexley** plugin, installed from the standards repository at the same release | Copies in `.github/skills/lbbexley-*` |
| Plan, build and check | Plan mode with `opusplan`: Opus plans, Sonnet builds, Haiku reviews | The **lbbexley-plan**, **lbbexley-build** and **lbbexley-check** agents, which hand over to each other |
| Standards check after each save, and the end-of-run check | Plugin hooks | Copilot hooks (a preview feature) in `.github/hooks/lbbexley.json` |
| Rules for particular files | `.claude/rules/lbbexley-*` | `.github/instructions/lbbexley-*` |

The copies are synced from the standards repository at the release your repository is on, and Claude Code installs the plugin from that release too, so both assistants follow identical rules.

## Where things live in your repository

| Where | What | Who changes it |
|---|---|---|
| `AGENTS.md` (and `CLAUDE.md`) | Your service's details and the rules that always apply. Both assistants read it first | The set-up in exercise 04 |
| `docs/discovery/` | What you said at set-up, and any cleaned meeting transcripts | The set-up, and you if you clean a transcript. Git ignores everything here except the README, but approved AI tools may still read and process its contents, so only cleaned material goes in |
| `docs/requirements.md` | Users, user stories with acceptance criteria, rules, data, duties and open questions | The requirements skill, from your answers in the chat, checked by the service owner |
| `docs/architecture.md` | The design: components, data flow, duties, diagram | The architect skill |
| `docs/plans/` | One plan per change | The plan skill |
| `src/` | The latest version from your dev environment: the solution (with flows and Dataverse), each canvas app's source, the Power Pages site, the agent | Nobody by hand: it's synced from the dev environment after each change |
| `tests/` | What the accessibility tests open, the agent test set, and the log of your manual tests | The assistant, from what you tell it |
| `docs/compliance/` | Accessibility statement, DPIA screening, equality impact, publicity check, ATRS record, retention | The assistant drafts them; the service team makes the decisions |
| `.github/skills/lbbexley-*`, `.github/agents/lbbexley-*`, `.lbbexley/standards/` and the other synced files | Copies of the standards | Nobody by hand. `npm run standards:update` replaces them |

## From a conversation to working software

```mermaid
flowchart LR
    talk["Your answers in the chat,<br/>or a table the service team filled in"] -- "requirements skill" --> req["docs/requirements.md"]
    meeting["A cleaned Teams transcript<br/>(optional)"] -.-> req
    req -- "architect skill" --> arch["docs/architecture.md"]
    req -- "one story at a time:<br/>plan skill" --> plan["docs/plans/"]
    plan -- "build, checked as it goes" --> dev["Your dev environment"]
    dev -- "latest version synced" --> src["src/"]
```

That's the path you'll follow in exercises 05 to 11, with your own project.

## Look around

Open [lbbexley-app-template](https://github.com/dbraben/lbbexley-app-template) on GitHub and find:

1. `AGENTS.md`: the **Never** list. Which commands can't the assistant run?
2. `.github/workflows/quality.yml`: the line with `uses:`. Which release of the standards does the check on GitHub use? Find the same release in `.claude/settings.json`.
3. `docs/discovery/.gitignore`: why does it contain a single `*`?
4. `.claude/settings.json`: the `allow` and `deny` lists. Which `pac` and Git commands can Claude run without asking you, and which pushes are denied? Which file types can't it read?
5. `.github/skills/`: is there a skill for each platform you might use in your project?

## Check

- [ ] You can say what each of the three repositories is for, and which one you'll work in
- [ ] You can name the three steps every change goes through, and the model each runs on
- [ ] You know that Git never commits anything in `docs/discovery/`, and why only cleaned material goes there
- [ ] You found the answers to the five questions above

---

[← 00 Before you start](00-before-you-start.md) · [Next: 02 Create your service repository →](02-create-your-service-repo.md)
