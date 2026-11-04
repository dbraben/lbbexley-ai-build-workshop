# 09 Build it (Claude Code)

*About 30 minutes · Files only, or with a dev environment*

Now Claude builds what you planned, on Sonnet. Watch the checks as it works: the standards check runs every time Claude saves a file, and the end-of-run check runs before it can finish.

Follow the route for what your plan builds. Each route starts the same way:

- Approve the plan with **Yes, manually approve edits**, so you see each change.
- After each save, read what the standards check says: "Bexley standards check passed for ..." means the file is clean. A list of problems means Claude must fix them straight away, however minor, and it does.
- At the end, the end-of-run check runs. When Claude Code shows "Bexley end-of-run check passed", the run is finished.

## Route A: a canvas app screen, files only

1. Approve the plan. Claude builds the screen as source, for example `src/canvas/<AppName>/<ScreenName>.pa.yaml`, from the Bexley screen pattern and with the Bexley design tokens, and puts the made-up sample data in a named formula.
2. Approve each edit as it comes, and watch the standards check after each save.
3. Claude may say it can't add the screen to `tests/accessibility/targets.json` yet, because there's no app to open. That's right: you'll add it once the app exists in a dev environment. If the end-of-run reviewer raises it, Claude explains, and the check passes the decision to you.
4. When Claude finishes, read the screen's source and check:
   - every colour, font and size is a token, such as `BexleyFuchsia` or `BexleySizeBody`
   - there's one heading with `Role: =TextRole.Heading1`, and it says what the screen is for
   - every control has a name like `lblHeading` or `galItems`, and every icon and input has an `AccessibleLabel`
   - the words match the plan exactly
5. Commit it on your branch:

   ```bash
   git add -A
   git commit -m "<what the story lets people do>"
   ```

## Route B: in your dev environment

### Set up the environment once, before you approve the plan

1. **Create the solution.** In [Power Apps](https://make.powerapps.com), open your dev environment, then **Solutions**, then **New solution**. Use the solution name from `AGENTS.md`, and the Bexley publisher (prefix `lbbexley`).
2. **Connect the Power Platform CLI** and clone the solution into your repository, using your environment's address and solution name:

   ```bash
   pac auth create --environment https://<your-dev-environment>.crm11.dynamics.com
   pac solution clone --name <solution name> --outputDirectory src/solution
   ```

3. **Connect the Dataverse MCP server** if your story uses Dataverse. Set your dev environment's address, then restart VS Code. In PowerShell:

   ```powershell
   setx DATAVERSE_DEV_URL "https://<your-dev-environment>.crm11.dynamics.com"
   ```

   When Claude Code asks whether to use the MCP servers in `.mcp.json`, approve **dataverse**. Run `/mcp` to check it's connected.

   > [!NOTE]
   > The template starts the Dataverse server through `cmd`, which is for Windows. On a Mac, ask the facilitator.

### Then build what your story needs

**Dataverse tables and data**

- Approve the plan. Claude looks at your tables without asking: listing and describing them is allowed.
- It asks before it creates a table or columns, and before it adds records. Check every record is made up.
- Ask it to delete one of the records. The Dataverse guard blocks it: deletes are never allowed through the assistant.
- It runs `pac solution sync` in `src/solution`, so the table is in source control. Approve it.

**A canvas app screen**

- Create a blank canvas app in your solution (**New**, **App**, **Canvas app**), named after your service, and save it. In Power Apps Studio, open **Settings**, **Updates**, and turn on **Coauthoring**. Copy the Studio address from your browser.
- Run `/configure-canvas-mcp` and paste the Studio address when asked. Check it by asking: *"List the available Canvas App controls."*
- Approve the plan. Claude builds the screen with Microsoft's canvas tools: it appears in Power Apps Studio. Ask Claude to keep the source in `src/canvas/<AppName>/`.
- In Power Apps Studio, play the app. Move through the screen with the Tab key only, and check every control shows a clear focus border.

**A model-driven app**

- Claude creates the tables and columns through the Dataverse MCP server, as above.
- Build the app, its form and its views in the app designer, or ask Claude to use Microsoft's model-apps plugin if the set-up turned it on. Keep Microsoft's standard forms and theme: they're tested for accessibility.
- Run `pac solution sync` in `src/solution` so the app is reviewed in your pull request.

**A Power Pages page**

- Use a dev site in your environment. Dev sites are private, so the public can't find them.
- Claude uses Microsoft's power-pages plugin, if the set-up turned it on, or the Power Platform CLI (`pac pages download` and `pac pages upload`) to work on the site's source in `src/`. It asks before any upload, and only ever to the dev site.
- Watch the standards check on each page: the page title, the language, labels, heading order and no tracking scripts.

**A Power Automate flow**

- Build the flow in the Power Automate designer, inside your solution, following the plan: Claude plans and reviews flows, but doesn't build them in the designer.
- Run `pac solution sync` in `src/solution`. Then ask Claude: *"Check the flow in src/solution against the power-automate skill."* The standards check also runs on the flow's source: error handling, hard-coded mailboxes and personal data in emails.
- Make the fixes in the designer, and sync again.

**A Copilot Studio agent**

- In [Copilot Studio](https://copilotstudio.microsoft.com), in your dev environment, create the agent, named for its one job. Make sure it's in your solution: in Power Apps, open the solution and use **Add existing** if it isn't there.
- Add its knowledge: the bexley.gov.uk pages about your service, or documents the service owner has approved. Turn off general knowledge and web search, so it answers only from those.
- In VS Code, open the Copilot Studio extension's **Agents** view, choose your environment, right-click the agent and select **Clone agent**. Choose `src/agent/` in your repository.
- Approve the plan. The standards check runs on every `.mcs.yml` file Claude saves: it rejects emoji, real-looking personal data, placeholder text and card images without alt text.
- Use the Copilot Studio extension to apply your changes to the agent, then test it in Copilot Studio with every question in `tests/agent-test-set.md`.
- Ask Claude to update `docs/compliance/atrs-record.md` for the agent, using the ai-transparency skill.

### Commit

Whatever you built, commit it on your branch:

```bash
git add -A
git commit -m "<what the story lets people do>"
```

## Check

- [ ] `npm run check` finds no problems
- [ ] Claude Code showed "Bexley end-of-run check passed"
- [ ] What you built matches the plan, including the exact words
- [ ] With a dev environment: the source is in `src/`, and deleting a record was blocked

## What just happened

- Approving the plan switched Claude from Opus to Sonnet: planning needs the strongest model, building doesn't.
- The standards check sends every finding back to Claude straight away, so problems are fixed while the file is still open, not found later in review.
- In your dev environment, the Dataverse guard let Claude explore freely, asked you before any record was read or changed, and blocked deletes.

---

[← 08 Plan the first story](08-plan-the-first-story.md) · [Next: 10 Check and test →](10-check-and-test.md)
