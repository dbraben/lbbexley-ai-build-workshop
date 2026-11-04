# 04 Set up your service (Claude Code)

*About 15 minutes · No dev environment needed*

`/lbbexley:new-app` fills in the template for your project: the service details in `AGENTS.md` and `README.md`, the compliance documents, the Microsoft plugins your build needs, and the test tools. It's also the first time you'll see the end-of-run check.

## Steps

1. Make sure the session is in plan mode, then run the command with your service's name, in plain English:

   ```text
   /lbbexley:new-app <your service's name>
   ```

2. Claude asks about the service, all at once. Answer for your project:

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

   Not sure about an answer? Say so: "not decided yet" for what you're building, or "no environment yet" for the dev environment, are normal answers at this stage. Claude records them, and the design step settles them. You can change anything after you've written the requirements.

3. Because the session is in plan mode, Claude shows what it's going to change before changing anything. Read the plan, then approve it with **Yes, manually approve edits**, so you see each change.
4. Approve the edits and commands as they come. It installs the test tools with `npm install` and `npm run test:a11y:install`.
5. Watch the end of the run. Before Claude can finish, the end-of-run check:
   - runs the standards check on every file it changed, and sends it back to fix anything it finds
   - asks the **lbbexley:end-of-run-reviewer** agent, on Haiku, to review the changes for what the check can't see, such as wording and missing tests

   Claude Code shows the request for the review as a **Stop hook error**. That's the check working, not a fault. The reviewer runs in the background, so you may see "the review on the smaller model is still running" while Claude waits for it. When the review reports, Claude carries on by itself and fixes anything it found.
6. **Watch Claude commit the set-up.** When everything passes, the check asks Claude to commit the work: one more **Stop hook error**, starting "Bexley end-of-run check passed. Now save the work". Claude commits the set-up, on `main`, and tells you it's committed. Then Claude Code shows "Bexley end-of-run check passed". Committing saves a version of your work in Git, on your computer. You don't run any Git commands: Claude does this at the end of every piece of work.

   If Claude says Git doesn't know who you are, set your name and email as in [exercise 00](../00-before-you-start.md), then ask Claude: *"Commit the set-up."*
7. Restart Claude Code so the Microsoft plugins it turned on are loaded: run `/exit`, then `claude`.

## Check

- [ ] `AGENTS.md` and `README.md` describe your service, with no `{{...}}` placeholders left
- [ ] The compliance documents in `docs/compliance/` name your service. Any that depend on a decision you haven't made yet say "To be confirmed after the design."
- [ ] Claude said the set-up is committed, and Claude Code showed "Bexley end-of-run check passed" before it finished

## What just happened

- The set-up left some `{{...}}` parts in the compliance documents on purpose. They need real decisions from the service team, so `npm run check:release` keeps failing until they're done.
- The end-of-run review ran on Haiku, a smaller and faster model, because checking needs less than building. It uses far less of your allowance than the build did.
- The set-up was committed only after the review, because the review reads the changes that haven't been committed yet. Claude never makes a branch, pushes or opens a pull request unless you ask.
- From now on, the standards check runs for every change: after each save, at the end of each run, and again on GitHub whenever your work is pushed there.

---

[← 03 Turn on the standards](03-turn-on-the-standards.md) · [Next: 05 Answer the requirements questions →](../05-answer-the-requirements-questions.md)
