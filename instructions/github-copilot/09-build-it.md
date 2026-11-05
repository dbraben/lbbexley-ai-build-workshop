# 09 Build it (GitHub Copilot)

*About 30 minutes · Dev environment needed*

Now **lbbexley-build** builds what you planned, on the everyday model, directly in your dev environment with Microsoft's tools. Your repository keeps the latest version: after each change in the dev environment, the agent brings it into the repository, **lbbexley-check** reviews it, and the agent commits it and pushes it to GitHub. You don't run Git.

## Set up your dev environment once

1. **Create the solution.** In [Power Apps](https://make.powerapps.com), open your dev environment, then **Solutions**, then **New solution**. Use the solution name from `AGENTS.md`, and the Bexley publisher (prefix `lbbexley`).
2. **Sign in to the Power Platform CLI**, in VS Code's terminal, with your environment's address. A browser opens for you to sign in:

   ```bash
   pac auth create --environment https://<your-dev-environment>.crm11.dynamics.com
   ```

3. **Bring the solution into your repository.** Choose **lbbexley-build** and ask: *"Clone the solution named in AGENTS.md into src/solution."* It runs `pac solution clone`. The Bexley hooks check first that `pac` is connected to the dev environment in `AGENTS.md`, and stop it if it isn't.
4. **Connect what your story uses.** Only the parts you need:

   **Dataverse**, for tables, a model-driven app, or a screen that uses a table. Run **MCP: List Servers** from the Command Palette, choose **dataverse** and start it. When VS Code asks for the Dataverse dev environment address, give yours: never a test or production address.

   **A canvas app.** Microsoft's tools can't create the app, so you do, once:

   - In your solution, select **New**, **App**, **Canvas app**. Name it after your service, and save it.
   - In Power Apps Studio, open **Settings**, **Updates**, and turn on **Coauthoring**. Keep this tab open while you build. Copy its address from the editing page, not the app player.
   - In VS Code, open the **Extensions** view, search for `@agentPlugins canvas apps`, and install **Canvas Apps**, published by Microsoft. Then, in the chat, run `/configure-canvas-mcp` and paste the address. Check it by asking: *"List the available Canvas App controls."* Microsoft's page [Create canvas apps with external tools](https://learn.microsoft.com/en-us/power-apps/maker/canvas-apps/create-canvas-external-tools) has more.

   **A flow.** Install Microsoft's Power Automate plugin the same way: search for `@agentPlugins power automate`. It signs in with the Azure CLI, so in VS Code's terminal, sign in with the same account as `pac`:

   ```bash
   az login
   ```

   **A Power Pages page.** Use a dev site in your environment: dev sites are private, so the public can't find them. Ask lbbexley-build: *"Download the dev site's source into src/pages."*

   **A Copilot Studio agent.** In [Copilot Studio](https://copilotstudio.microsoft.com), in your dev environment, create the agent, named for its one job, and make sure it's in your solution: in Power Apps, open the solution and use **Add existing** if it isn't there. Add its knowledge: the bexley.gov.uk pages about your service, or documents the service owner has approved, with general knowledge and web search turned off. Then open the Copilot Studio extension's **Agents** view, choose your environment, right-click the agent, select **Clone agent** and choose `src/agent/` in your repository.

> [!TIP]
> VS Code may ask the first time the agent uses each tool or command. For the tools above, and for `pac solution sync`, `git commit` and `git push`, choose to always allow them in this workspace. Never allow a delete, or anything aimed at another environment.

## Build it

1. Select **Build this plan** under the plan. It hands over to **lbbexley-build** with a prompt ready: send it. If the button isn't under the latest reply, choose **lbbexley-build** in the agent picker and say: *"Build the plan in docs/plans/."*
2. **Watch it build.** What happens depends on what your story needs:

   | You're building | What lbbexley-build does | Try this |
   |---|---|---|
   | Dataverse tables | Creates the tables and columns, and a few made-up records, through the Dataverse MCP server | Ask it to delete one of the records. The Bexley hooks block it: deletes are never allowed through the assistant |
   | A canvas app screen | Brings the app into `src/canvas/<AppName>/`, writes the screen there, and compiles it into the app: it appears in the Power Apps Studio tab | In Studio, play the app. Move through the screen with the Tab key only, and check every control shows a clear focus border |
   | A flow | Builds it in your dev environment, inside the solution, with Microsoft's Power Automate tools | The hooks ask you before the flow runs, because a run can send real emails or messages: test only with made-up data and your own address. Ask it to delete the flow: that's blocked too |
   | A model-driven app | Creates the tables and columns, as above | Build the app, its form and its views in the app designer yourself, keeping Microsoft's standard forms and theme. Then ask lbbexley-build to use the lbbexley-sync skill |
   | A Power Pages page | Works on the page in `src/pages/`, then uploads it to the dev site with `pac pages upload`: the hooks check it's the dev environment first | Watch the standards check on each page: the page title, the language, labels, heading order and no tracking scripts |
   | A Copilot Studio agent | Edits the agent's `.mcs.yml` files in `src/agent/`. The standards check rejects emoji, real-looking personal data, placeholder text and card images without alt text | Apply the changes with the Copilot Studio extension, then test the agent in Copilot Studio with every question in `tests/agent-test-set.md`. Ask lbbexley-build to update `docs/compliance/atrs-record.md` with the lbbexley-ai-transparency skill |

3. **Bring in the latest version.** Before the agent finishes, it runs `pac solution sync` into `src/solution`. If hooks are on and it hasn't, the end-of-run gate asks it to.
4. **Check, commit and push.** Select **Check my work**: lbbexley-check reviews the changes on a smaller model. If it reports problems, select **Fix what the check found**: lbbexley-build fixes them in the dev environment and syncs again. Then select **Check my work** again. When it finds nothing outstanding, select **Commit the work**: lbbexley-build commits the latest version, pushes it to GitHub and tells you it's done. The buttons are under every reply, whatever the check found, so look at the result first.
5. **Check what was built** against the plan. For a canvas app screen, read its source in `src/canvas/<AppName>/`:
   - every colour, font and size is a token, such as `BexleyFuchsia` or `BexleySizeBody`
   - there's one heading with `Role: =TextRole.Heading1`, and it says what the screen is for
   - every control has a name like `lblHeading` or `galItems`, and every icon and input has an `AccessibleLabel`
   - the words match the plan exactly

   To change anything that doesn't, ask lbbexley-build. It changes it in the dev environment, and the new version is synced, checked, committed and pushed in the same way.

## Changed something yourself?

If you change something in the dev environment yourself, in Power Apps Studio, the flow designer or the app designer, ask lbbexley-build to use the lbbexley-sync skill. It brings in the latest version; then select **Check my work** and **Commit the work** as usual. Never edit the files in `src/solution` yourself: they'd no longer match the dev environment.

## Check

- [ ] What you built is in your dev environment, and matches the plan, including the exact words
- [ ] lbbexley-check reported nothing outstanding, and lbbexley-build said the work is committed and pushed
- [ ] The latest version is in `src/` and on GitHub: `src/solution`, and `src/canvas/<AppName>/` for a canvas app
- [ ] Deleting a record or a flow was blocked
- [ ] `npm run check:all` finds no problems

## What just happened

- The handover moved the work from the strongest model to the everyday one, and then to a smaller one for the check: each step runs on the smallest model that does it well.
- The agent worked in the dev environment directly. The hooks kept it to the dev environment in `AGENTS.md`, blocked deletes, and asked before anything that could reach people outside it, such as running a flow.
- The latest version came into your repository before the check, so what was reviewed, committed and pushed is what's in the dev environment.

---

[← 08 Plan the first story](08-plan-the-first-story.md) · [Next: 10 Check and test →](10-check-and-test.md)
