# 09 Build it (Claude Code)

*About 30 minutes · Dev environment needed*

Now Claude builds what you planned, on Sonnet, directly in your dev environment with Microsoft's tools. Your repository keeps the latest version: after each change in the dev environment, Claude brings it into the repository, the end-of-run check reviews it, and Claude commits it and pushes it to GitHub. You don't approve each change in the dev environment, and you don't run Git.

## Set up your dev environment once

Do this before exercise 08 if you can: it restarts Claude Code, and a plan waiting for approval doesn't survive a restart. If you've already planned, restart, run `claude --continue`, and say: *"Show me the plan for approval."*

Claude Code is running in VS Code's terminal, so run the commands below in a second terminal: **Terminal**, then **New Terminal**.

1. **Create the solution.** In [Power Apps](https://make.powerapps.com), open your dev environment, then **Solutions**, then **New solution**. Use the solution name from `AGENTS.md`, and the Bexley publisher (prefix `lbbexley`). Then select the solution and choose **Set preferred solution**, so anything you create in Power Apps lands in it.
2. **Sign in to the Power Platform CLI**, with your environment's address. A browser opens for you to sign in:

   ```bash
   pac auth create --environment https://<your-dev-environment>.crm11.dynamics.com
   ```

3. **Bring the solution into your repository.** Ask Claude: *"Clone the solution named in AGENTS.md into src/solution."* It runs `pac solution clone` without asking: the Bexley guardrails check first that `pac` is connected to the dev environment in `AGENTS.md`, and stop it if it isn't.
4. **Connect what your story uses.** Only the parts you need:

   **Dataverse**, for tables, a model-driven app, or a screen that uses a table.

   On Windows, set your dev environment's address, then restart VS Code. In PowerShell:

   ```powershell
   setx DATAVERSE_DEV_URL "https://<your-dev-environment>.crm11.dynamics.com"
   ```

   When Claude Code asks whether to use the MCP servers in `.mcp.json`, approve **dataverse**.

   On a Mac or Linux, the template's server starts through Windows' `cmd`, so add your own instead, for this computer only. Run this in the second terminal, with your dev environment's address, then start Claude Code again. It takes the place of the template's **dataverse** server, and nothing in the repository changes:

   ```bash
   claude mcp add --scope local dataverse -- npx -y @microsoft/dataverse mcp https://<your-dev-environment>.crm11.dynamics.com
   ```

   Then run `/mcp` to check **dataverse** is connected.

   **A canvas app.** Microsoft's tools can't create the app, so you do, once:

   - In your solution, select **New**, **App**, **Canvas app**. Name it after your service, and save it.
   - In Power Apps Studio, open **Settings**, **Updates**, and turn on **Coauthoring**. Keep this tab open while you build. Copy its address from the editing page, not the app player.
   - In Claude Code, run `/configure-canvas-mcp` and paste the address. Check it by asking: *"List the available Canvas App controls."*

   No `/configure-canvas-mcp`? Microsoft's canvas-apps plugin isn't on yet, because the design in exercise 07 turns it on. Ask Claude to turn it on, then restart Claude Code.

   **A flow.** Microsoft's Power Automate plugin signs in with the Azure CLI. In the second terminal, sign in with the same account as `pac`:

   ```bash
   az login
   ```

   No Power Automate tools when Claude builds? The plugin isn't on yet: ask Claude to turn on `power-automate` from the power-platform-skills marketplace, then restart Claude Code.

   **A Power Pages page.** Use a dev site in your environment: dev sites are private, so the public can't find them. Ask Claude: *"Download the dev site's source into src/pages."*

   **A Copilot Studio agent.** In [Copilot Studio](https://copilotstudio.microsoft.com), in your dev environment, create the agent, named for its one job, and make sure it's in your solution: in Power Apps, open the solution and use **Add existing** if it isn't there. Add its knowledge: the bexley.gov.uk pages about your service, or documents the service owner has approved, with general knowledge and web search turned off. Then, in VS Code, open the Copilot Studio extension's **Agents** view, choose your environment, right-click the agent, select **Clone agent** and choose `src/agent/` in your repository.

## Build it

1. **Approve the plan**, choosing to auto-accept edits. Claude switches to Sonnet and builds in your dev environment without asking before each change.
2. **Watch it build.** What happens depends on what your story needs:

   | You're building | What Claude does | Try this |
   |---|---|---|
   | Dataverse tables | Creates the tables and columns, and a few made-up records, through the Dataverse MCP server, then adds each table to the solution | Ask it to delete one of the records. The Bexley guardrails block it: deletes are never allowed through the assistant |
   | A canvas app screen | Brings the app into `src/canvas/<AppName>/`, writes the screen there, and compiles it into the app: it appears in the Power Apps Studio tab | In Studio, play the app. Move through the screen with the Tab key only, and check every control shows a clear focus border |
   | A flow | Builds it in your dev environment with Microsoft's Power Automate tools, then adds it to the solution with `pac solution add-solution-component` | Claude asks before it runs the flow, because a run can send real emails or messages: test only with made-up data and your own address. Ask it to delete the flow: that's blocked too |
   | A model-driven app | Creates the tables and columns, as above | Build the app, its form and its views in the app designer yourself, keeping Microsoft's standard forms and theme. Then ask Claude: *"Bring in the latest version from the dev environment."* |
   | A Power Pages page | Works on the page in `src/pages/`, then uploads it to the dev site with `pac pages upload`: the guardrails check it's the dev environment first | Watch the standards check on each page: the page title, the language, labels, heading order and no tracking scripts |
   | A Copilot Studio agent | Edits the agent's `.mcs.yml` files in `src/agent/`. The standards check rejects emoji, real-looking personal data, placeholder text and card images without alt text | Apply the changes with the Copilot Studio extension, then test the agent in Copilot Studio with every question in `tests/agent-test-set.md`. Ask Claude to update `docs/compliance/atrs-record.md` with the ai-transparency skill |

3. **Watch the end of the run.** Before Claude can finish, the end-of-run check:
   - has Claude bring in the latest version: any new flow or table added to the solution, then `pac solution sync` in `src/solution/<solution>/`. Claude Code shows this as a **Stop hook error** starting "Before finishing, bring the latest version from the dev environment into the repository"
   - runs the standards check on everything that changed, and sends it back to fix anything it finds, in the dev environment
   - asks the end-of-run reviewer, on Haiku, to review the changes
   - asks Claude to commit the latest version and push it to GitHub, and checks it did: if not, it asks once more, then tells you what's unsaved

   When Claude says it's committed and pushed, and Claude Code shows "Bexley end-of-run check passed", the run is finished.
4. **Check what was built** against the plan. For a canvas app screen, read its source in `src/canvas/<AppName>/`:
   - every colour, font and size is a token, such as `BexleyFuchsia` or `BexleySizeBody`
   - there's one heading with `Role: =TextRole.Heading1`, and it says what the screen is for
   - every control has a name like `lblHeading` or `galItems`, and every icon and input has an `AccessibleLabel`
   - the words match the plan exactly

   Ask Claude to change anything that doesn't. It changes it in the dev environment, and the new version is synced, checked, committed and pushed in the same way.

## Changed something yourself?

If you change something in the dev environment yourself, in Power Apps Studio, the flow designer or the app designer, run `/lbbexley:sync`. Claude brings in the latest version, and the end-of-run check reviews it, then has it committed and pushed. Never edit the files in `src/solution` yourself: they'd no longer match the dev environment.

## Check

- [ ] What you built is in your dev environment, and matches the plan, including the exact words
- [ ] Claude said the work is committed and pushed, and Claude Code showed "Bexley end-of-run check passed"
- [ ] The latest version is in `src/` and on GitHub: `src/solution/<solution>/` (a flow you built appears under its `src/Workflows/`), and `src/canvas/<AppName>/` for a canvas app
- [ ] Deleting a record or a flow was blocked
- [ ] `npm run check:all` finds no problems

## What just happened

- Approving the plan switched Claude from Opus to Sonnet: planning needs the strongest model, building doesn't.
- Claude worked in the dev environment directly. You didn't approve each change, but the guardrails kept it to the dev environment in `AGENTS.md`, blocked deletes, and asked before anything that could reach people outside it, such as running a flow.
- The end-of-run check made sure your repository has what's in the dev environment, had it reviewed on a smaller model, then had it saved on GitHub, where the same checks run again.

---

[← 08 Plan the first story](08-plan-the-first-story.md) · [Next: 10 Check and test →](10-check-and-test.md)
