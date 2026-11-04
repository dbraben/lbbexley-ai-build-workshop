# 09 Build it (GitHub Copilot)

*About 30 minutes · Files only, or with a dev environment*

Now **lbbexley-build** builds what you planned, on the everyday model. With hooks on, the standards check runs after every edit, and the end-of-run gate holds the agent back until everything it changed passes.

Follow the route for what your plan builds. Each route starts and ends the same way:

- Select **Build this plan** under the plan. It hands over to **lbbexley-build** with a prompt ready: send it. If the button isn't under the latest reply, choose **lbbexley-build** in the agent picker and say: *"Build the plan in docs/plans/."*
- Review and keep each change. After each edit, the standards check's result goes back to the agent: "Bexley standards check passed for ...", or a list of problems it must fix straight away, however minor.
- When the build finishes, select **Check my work** to hand over to **lbbexley-check**. If it reports problems, select **Fix what the check found**, then **Check my work** again. When it finds nothing outstanding, select **Commit the work**. The buttons are under every reply, whatever the check found, so look at the result first.

## Route A: a canvas app screen, files only

1. Select **Build this plan**. The agent builds the screen as source, for example `src/canvas/<AppName>/<ScreenName>.pa.yaml`, from the Bexley screen pattern and with the Bexley design tokens, and puts the made-up sample data in a named formula.
2. Review and keep each change, and watch the standards check after each edit.
3. The agent may say it can't add the screen to `tests/accessibility/targets.json` yet, because there's no app to open. That's right: you'll add it once the app exists in a dev environment.
4. Select **Check my work**, and fix anything it finds.
5. Read the screen's source and check:
   - every colour, font and size is a token, such as `BexleyFuchsia` or `BexleySizeBody`
   - there's one heading with `Role: =TextRole.Heading1`, and it says what the screen is for
   - every control has a name like `lblHeading` or `galItems`, and every icon and input has an `AccessibleLabel`
   - the words match the plan exactly

   To change anything that doesn't, choose **lbbexley-build** in the agent picker and ask for it, then select **Check my work** again.
6. Select **Commit the work**. lbbexley-build commits the screen and tells you it's committed. If the check's only problem is the missing test target, that's expected with no app to open yet: commit the work anyway.

## Route B: in your dev environment

### Set up the environment once, before you hand over

1. **Create the solution.** In [Power Apps](https://make.powerapps.com), open your dev environment, then **Solutions**, then **New solution**. Use the solution name from `AGENTS.md`, and the Bexley publisher (prefix `lbbexley`).
2. **Sign in to the Power Platform CLI**, in VS Code's terminal, with your environment's address. A browser opens for you to sign in:

   ```bash
   pac auth create --environment https://<your-dev-environment>.crm11.dynamics.com
   ```

3. **Start the Dataverse MCP server** if your story uses Dataverse. Run **MCP: List Servers** from the Command Palette, choose **dataverse** and start it. When VS Code asks for the Dataverse dev environment address, give yours: never a test or production address.
4. **Get the solution's source.** Choose **lbbexley-build** and ask: *"Clone the solution named in AGENTS.md into src/solution."* It runs `pac solution clone`: allow it.

### Then build what your story needs

**Dataverse tables and data**

- Select **Build this plan**. VS Code asks before each Dataverse tool runs. Approve listing and describing tables, and creating the tables, columns and a few made-up records.
- Ask the agent to delete one of the records. The Bexley hook blocks it: deletes are never allowed through the assistant. Never approve a delete yourself.
- It runs `pac solution sync` in `src/solution`, so the table's source is in your repository.

**A canvas app screen**

- Create a blank canvas app in your solution (**New**, **App**, **Canvas app**), named after your service, and save it. In Power Apps Studio, open **Settings**, **Updates**, and turn on **Coauthoring**.
- Follow Microsoft's page [Create canvas apps with external tools](https://learn.microsoft.com/en-us/power-apps/maker/canvas-apps/create-canvas-external-tools), which covers GitHub Copilot: install the canvas apps plugin, then connect it to your app with the Studio address.
- Select **Build this plan**. The agent builds the screen with Microsoft's canvas tools: it appears in Power Apps Studio. Ask it to keep the source in `src/canvas/<AppName>/`.
- In Power Apps Studio, play the app. Move through the screen with the Tab key only, and check every control shows a clear focus border.

**A model-driven app**

- The agent creates the tables and columns through the Dataverse MCP server, as above.
- Build the app, its form and its views in the app designer. Keep Microsoft's standard forms and theme: they're tested for accessibility.
- Ask lbbexley-build: *"Sync the solution into src/solution."* Then the app's source is in your repository, where the checks can see it.

**A Power Pages page**

- Use a dev site in your environment. Dev sites are private, so the public can't find them.
- Ask lbbexley-build: *"Download the dev site's source into src/pages."* It finds the site's ID with `pac pages list`, then runs `pac pages download`: allow both.
- Select **Build this plan**. The agent works on the page in `src/pages/`. It uploads to the dev site only, with `pac pages upload`: allow the command only when you've read the changes.
- Watch the standards check on each page: the page title, the language, labels, heading order and no tracking scripts.

**A Power Automate flow**

- Build the flow in the Power Automate designer, inside your solution, following the plan: the agents plan and review flows, but don't build them in the designer.
- Ask lbbexley-build: *"Sync the solution into src/solution, and check the flow against the lbbexley-power-automate skill."* The standards check also runs on the flow's source: error handling, hard-coded mailboxes and personal data in emails.
- Make the fixes in the designer, and ask the agent to sync again.

**A Copilot Studio agent**

- In [Copilot Studio](https://copilotstudio.microsoft.com), in your dev environment, create the agent, named for its one job. Make sure it's in your solution: in Power Apps, open the solution and use **Add existing** if it isn't there.
- Add its knowledge: the bexley.gov.uk pages about your service, or documents the service owner has approved. Turn off general knowledge and web search, so it answers only from those.
- In VS Code, open the Copilot Studio extension's **Agents** view, choose your environment, right-click the agent and select **Clone agent**. Choose `src/agent/` in your repository.
- Select **Build this plan**. The standards check runs on every `.mcs.yml` file the agent edits: it rejects emoji, real-looking personal data, placeholder text and card images without alt text.
- Use the Copilot Studio extension to apply your changes to the agent, then test it in Copilot Studio with every question in `tests/agent-test-set.md`.
- Ask lbbexley-build to update `docs/compliance/atrs-record.md` for the agent, using the lbbexley-ai-transparency skill.

### Check and commit

Whatever you built, select **Check my work**, fix anything it finds, then select **Commit the work**. When you change something outside the agents, such as a flow in the designer, ask lbbexley-build to sync the solution again, then check and commit as usual.

## Check

- [ ] `npm run check:all` finds no problems
- [ ] lbbexley-check reported nothing outstanding, and lbbexley-build said the work is committed
- [ ] What you built matches the plan, including the exact words
- [ ] With a dev environment: the source is in `src/`, and deleting a record was blocked

## What just happened

- The handover moved the work from the strongest model to the everyday one, and then to a smaller one for the check: each step runs on the smallest model that does it well.
- The standards check sends every finding back to the agent straight away, so problems are fixed while the file is still open, not found later in review.

---

[← 08 Plan the first story](08-plan-the-first-story.md) · [Next: 10 Check and test →](10-check-and-test.md)
