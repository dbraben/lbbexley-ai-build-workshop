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

   Not sure about an answer? Say so: Claude records it, and you can change it after you've written the requirements.

3. Because the session is in plan mode, Claude shows what it's going to change before changing anything. Read the plan, then approve it with **Yes, and manually approve edits**, so you see each change.
4. Approve the edits and commands as they come. It installs the test tools with `npm install` and `npm run test:a11y:install`.
5. Watch the end of the run. Before Claude can finish, the end-of-run check:
   - runs the standards check on every file it changed, and sends it back to fix anything it finds
   - asks the **lbbexley:end-of-run-reviewer** agent, on Haiku, to review the changes for what the check can't see, such as wording and missing tests

   When both are clean, Claude Code shows "Bexley end-of-run check passed".
6. Restart Claude Code so the Microsoft plugins it turned on are loaded: run `/exit` and start Claude Code again.
7. Commit the set-up on a branch and open a pull request. Ask Claude to do it, or run:

   ```bash
   git switch -c set-up
   git add -A
   git commit -m "Set up the service"
   git push -u origin set-up
   ```

   Then open a pull request on GitHub and fill in the template. Claude asks before it pushes, because the template sets `git push` to ask.
8. On the pull request, watch the **Quality** workflow. **Bexley standards** passes. **Accessibility tests** is skipped: it runs once the repository has an `A11Y_BASE_URL` variable. Merge the pull request, then update your copy:

   ```bash
   git switch main
   git pull
   ```

## Check

- [ ] `AGENTS.md` and `README.md` describe your service, with no `{{...}}` placeholders left
- [ ] The compliance documents in `docs/compliance/` name your service
- [ ] Claude Code showed "Bexley end-of-run check passed" before it finished
- [ ] The pull request passed **Bexley standards** and is merged

## What just happened

- The set-up left some `{{...}}` parts in the compliance documents on purpose. They need real decisions from the service team, so `npm run check:release` keeps failing until they're done.
- The end-of-run review ran on Haiku, a smaller and faster model, because checking needs less than building. It uses far less of your allowance than the build did.
- From now on, the standards check runs three times for every change: after each save, at the end of each run, and on the pull request.

---

[← 03 Turn on the standards](03-turn-on-the-standards.md) · [Next: 05 Capture your requirements →](../05-capture-your-requirements.md)
