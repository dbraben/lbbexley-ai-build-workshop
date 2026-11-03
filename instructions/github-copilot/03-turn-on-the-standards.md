# 03 Turn on the standards (GitHub Copilot)

*About 10 minutes · No dev environment needed*

GitHub Copilot gets the Bexley standards from files already in your repository: copies synced from the standards repository at the release your repository is on. There's nothing to install. In this exercise you check Copilot can see them.

| Where | What Copilot gets |
|---|---|
| `AGENTS.md` and `.github/copilot-instructions.md` | Your service's details and the rules that always apply |
| `.github/skills/lbbexley-*` | The Bexley skills: brand, accessibility, content style, the legal duties, one per platform, and the requirements, architect, plan, quality-checks, review and improve skills |
| `.github/agents/lbbexley-*` | The plan, build and check agents, and read-only reviewers |
| `.github/instructions/lbbexley-*` | Rules that apply automatically to the files they cover, such as canvas app source |
| `.github/hooks/lbbexley.json` | Hooks (a preview feature) that run the standards check after each edit and before the agent finishes |

## Steps

1. In VS Code, with your service repository open, open the chat view and choose **Agent** mode.
2. Open the agent picker in the chat box. Find **lbbexley-plan**, **lbbexley-build** and **lbbexley-check**, and the reviewers **lbbexley-accessibility-reviewer**, **lbbexley-compliance-reviewer** and **lbbexley-end-of-run-reviewer**.
3. Choose **lbbexley-plan** and look at the model it uses. Each Bexley agent lists the models it prefers, in order: Opus for planning, Sonnet for building, Haiku for checking. Copilot uses the first one your plan offers.

   > [!NOTE]
   > If your Copilot plan doesn't include a model on the list, Copilot uses the next one, or the model you pick. The facilitator can tell you which models your plan has.

4. Ask: *"Which Bexley skills and rules apply in this repository?"* Copilot lists the lbbexley skills, including **lbbexley-requirements**, and the rules from `AGENTS.md`.
5. Check the workspace settings that turn these on, in `.vscode/settings.json`: `chat.useAgentsMdFile`, `chat.useAgentSkills` and `chat.useHooks`.
6. Open `.github/hooks/lbbexley.json` and read what runs when. You'll see the hooks work in exercise 04.

> [!WARNING]
> In Copilot there's no guard that stops a message containing personal data before it reaches the model, and no setting that stops it reading a file in your repository's folder. Take extra care: fictional data only, and keep original transcripts and roles files out of your repository (exercise 05).

## Check

- [ ] The agent picker shows lbbexley-plan, lbbexley-build and lbbexley-check
- [ ] Copilot can list the lbbexley skills, including lbbexley-requirements
- [ ] You know which model each agent uses on your plan

## What just happened

- Copilot reads the same standards as Claude Code. The synced copies are written from the standards repository, so the two tools follow identical rules.
- Never edit the synced files by hand. The pull request check fails if they differ from the release, and `npm run standards:update` replaces them.

---

[← 02 Create your service repository](../02-create-your-service-repo.md) · [Next: 04 Set up your service →](04-set-up-your-service.md)
