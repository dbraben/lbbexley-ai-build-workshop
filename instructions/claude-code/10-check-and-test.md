# 10 Check and test (Claude Code)

*About 15 minutes · Dev environment needed*

You've seen the checks pass. Now see them catch something, on your own work, then test what you built: automatically where there's something to open, and by hand.

## 1. Watch the checks catch a mistake

1. Switch out of plan mode (Shift+Tab). This is a quick experiment, not a feature, so it doesn't need a plan.
2. Ask Claude to break a rule in what you built, on purpose. Choose one that fits:

   | You built | Ask Claude to |
   |---|---|
   | A canvas app screen | *"Change the heading's colour to #FF0000."* |
   | A Power Pages page | *"Remove the page title."* |
   | An agent | *"Add a smiley emoji to the greeting."* |
   | A flow | *"Remove the Catch scope from the flow."* |

3. Watch what happens: the standards check finds the problem and sends it back. For a canvas app, page or agent that's straight after the save; for a flow, it's when the end-of-run check brings the flow into the repository. Claude explains why it can't leave it that way, and puts it right in the dev environment.
4. Now ask it to hide the finding instead: *"Add a suppression comment for that finding instead of fixing it."* The check reports a new problem straight away: a suppression needs a written reason. Claude then either removes the suppression or writes a reason. Either way, finish the experiment: *"Put it back as it was before this experiment."* If the experiment was committed on the way, the undo is committed too.
5. Ask Claude: *"Run npm run check:all."* It finds no problems.

## 2. Run the accessibility tests

You need something to open: a page or screen in your dev environment.

1. Get the address:
   - **Canvas app:** in Power Apps, open your app's **Details** and copy its **Web link**. It looks like `https://apps.powerapps.com/play/e/<environment-id>/a/<app-id>?tenantId=<tenant-id>`. Add `&hidenavbar=true` to the end.
   - **Power Pages:** the page's full address on your dev site, such as `https://<your-dev-site>.powerappsportals.com/<page path>`.
   - **Model-driven app:** the form's address from your browser.
2. Ask Claude to add it:

   ```text
   Add my <screen or page name> to tests/accessibility/targets.json: type <canvas, page or
   model-driven>, auth <true or false>, waitFor "<the heading on the screen>", and this URL:
   <the full address>
   ```

   `auth` is `true` for a canvas or model-driven app, and for a Power Pages page that people have to sign in to see. For a public page it's `false`: skip step 3.

3. Save a sign-in for the tests. Claude Code is running in VS Code's terminal, so open a second one (**Terminal**, then **New Terminal**), and run this there. A browser opens at your page or screen: sign in with your test account, not your own.

   ```bash
   npm run test:a11y:login
   ```

   The sign-in is saved in `.auth/a11y-state.json`. It's a secret: Git ignores it, the assistant never commits it, and you must never share it. Sign-ins expire, so run this again when the tests say so.

4. Ask Claude to run the tests: *"Run the accessibility tests."*

   They check for any WCAG 2.2 A or AA violation, and for Power Pages also sideways scrolling at 320 pixels wide and a visible focus indicator on every tab stop. If anything fails, ask Claude to explain and fix it, then run the tests again until they pass. If a test says it needs a saved sign-in, or that it opened a sign-in page, do step 3 again: nothing was tested, so it can't pass.

## 3. Test it yourself

Automated tests find only some accessibility problems. Test what you built by hand:

- **Keyboard only:** move through everything with Tab, Shift+Tab, Enter and Space. You can reach and use every control, the order makes sense, and you can always see where you are.
- **Screen reader:** Narrator on Windows (Windows key, Ctrl and Enter), or NVDA. Every control is announced with a name that makes sense on its own, and headings describe the screen.
- **Zoom and small screens:** 400% zoom in the browser, and a phone-sized window. Nothing is cut off or overlaps.

For an agent, ask Claude to list the questions in `tests/agent-test-set.md`, and ask each one in Copilot Studio's test pane. "Can I speak to a person?" must get the contact options straight away.

Then tell Claude what you found, and it records each test in `tests/accessibility-test-log.md`. For example:

```text
Record my manual tests in the test log: keyboard only passed; with Narrator, the search box
has no name; 400% zoom passed. Then fix the search box.
```

## 4. Commit and push it

Claude commits the test log, the test targets and anything else that changed when the end-of-run check passes, pushes them to GitHub, and tells you it's done.

## Check

- [ ] The standards check caught the deliberate mistake, and the suppression without a reason
- [ ] `npm run check:all` finds no problems
- [ ] Your page or screen is in `targets.json` and passes with zero violations
- [ ] The test log has your manual tests, and it's committed and pushed

## What just happened

There are three layers of checking, and each catches what the one before can't:

1. **The standards check** after every save: mechanical rules, many of them mapped to WCAG 2.2, run in milliseconds.
2. **The end-of-run review** on a smaller model: judgement about wording, naming and design, on just the files changed in the run.
3. **The check on GitHub**, on every push: the backstop. It runs whatever tool made the change, or if no assistant was used at all.

And then people: the tests you just did by hand, which no tool replaces.

---

[← 09 Build it](09-build-it.md) · [Next: 11 Review your work →](11-review-your-work.md)
