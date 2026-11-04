# 04 Set up your service (GitHub Copilot)

*About 15 minutes · No dev environment needed*

The **lbbexley-new-app** skill fills in the template for your project: the service details in `AGENTS.md` and `README.md`, the compliance documents, and the test tools. It's also the first time you'll see the end-of-run check.

## Steps

1. In the chat view, choose Agent mode and the **lbbexley-build** agent, then ask, with your service's name in plain English:

   ```text
   Use the lbbexley-new-app skill to set up this repository for <your service's name>.
   ```

   If typing `/` in the chat box lists `lbbexley-new-app`, you can pick it from there instead.

2. Copilot asks about the service, all at once. Answer for your project:

   | Question | What to give | For example |
   |---|---|---|
   | Service name | What people would call it, in plain English | Meeting room bookings |
   | What it does | One sentence: what it lets people do | Staff book meeting rooms at the Civic Offices and see what's free |
   | Users | Residents, businesses, staff, or a mix | Staff, and the facilities team |
   | What you're building | Canvas app, Power Pages site, Copilot Studio agent, Power Automate flows, model-driven app, or a mix. Your best guess: the design may change it | Canvas app and flows |
   | Owner | The team that owns the service, not a person | Facilities |
   | Dev environment | Your dev environment's address, or "none yet" | none yet |
   | Personal data | What the real service will handle, in general terms. Never real examples | Staff names and teams |
   | AI | An agent, AI Builder, AI prompts in flows, or none | None |

   Not sure about an answer? Say so: "not decided yet" for what you're building, or "no environment yet" for the dev environment, are normal answers at this stage. Copilot records them, and the design step settles them. You can change anything after you've written the requirements.

3. Review each change Copilot proposes, and allow the commands it runs: `npm install` and `npm run test:a11y:install`.
4. Watch the end of the run. If hooks are on, the standards check has run after each edit, and before the agent finishes it asks you to hand the changes to **lbbexley-check**.
5. Select **Check my work**. The lbbexley-check agent, on a smaller model, runs the standards check, reviews the changes for what the check can't see, and logs any idea for improving the harness in `.lbbexley/improvements.md`. If it finds problems, select **Fix what the check found**: lbbexley-build fixes them. Then select **Check my work** again.
6. **Commit the set-up.** When lbbexley-check finds nothing outstanding, select **Commit the work**. lbbexley-build commits the set-up, on `main`, and tells you it's committed: allow the `git` command it runs. Committing saves a version of your work in Git, on your computer. You don't type any Git commands: you commit every piece of work this way.

   The buttons are under every reply from lbbexley-check, whatever it found, so read the result before you select one.

   If it says Git doesn't know who you are, set your name and email as in [exercise 00](../00-before-you-start.md), then ask lbbexley-build: *"Commit the set-up."*

> [!TIP]
> If the hooks didn't run (the agent finished without asking for lbbexley-check), run `npm run check` yourself and select lbbexley-check from the agent picker. Hooks are a preview feature and depend on your VS Code version.

## Check

- [ ] `AGENTS.md` and `README.md` describe your service, with no `{{...}}` placeholders left
- [ ] The compliance documents in `docs/compliance/` name your service. Any that depend on a decision you haven't made yet say "To be confirmed after the design."
- [ ] lbbexley-check reported nothing outstanding
- [ ] lbbexley-build said the set-up is committed

## What just happened

- The set-up left some `{{...}}` parts in the compliance documents on purpose. They need real decisions from the service team, so `npm run check:release` keeps failing until they're done.
- The check ran on a smaller model, because checking needs less than building.
- The set-up was committed only after the check, because the check reads the changes that haven't been committed yet. The agents never make a branch, push or open a pull request unless you ask.
- From now on, the standards check runs for every change: after each edit (with hooks), when you hand over to lbbexley-check, and again on GitHub whenever your work is pushed there.

---

[← 03 Turn on the standards](03-turn-on-the-standards.md) · [Next: 05 Answer the requirements questions →](../05-answer-the-requirements-questions.md)
