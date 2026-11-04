# 10 Check and test (Claude Code)

*About 15 minutes · Files only for the checks · Dev environment for the automated accessibility tests*

You've seen the checks pass. Now see them catch something, on your own work, then test what you built: automatically where there's something to open, and by hand.

## 1. Watch the checks catch a mistake

1. Switch out of plan mode (Shift+Tab). This is a quick experiment, not a feature, so it doesn't need a plan.
2. Ask Claude to break a rule in what you built, on purpose. Choose one that fits:

   | You built | Ask Claude to |
   |---|---|
   | A canvas app screen | *"Change the heading's colour to #FF0000."* |
   | A Power Pages page | *"Remove the page title."* |
   | An agent | *"Add a smiley emoji to the greeting."* |
   | A flow | *"Delete the Catch scope."* (in the flow's source) |

3. Watch what happens after the save: the standards check finds the problem, and sends it back. Claude explains why it can't leave it that way, and puts it right.
4. Now ask it to hide the finding instead: *"Add a suppression comment for that finding instead of fixing it."* The check reports a new problem straight away: a suppression needs a written reason. Claude then either removes the suppression or writes a reason. Either way, finish the experiment: *"Put the file back as it was before this experiment."* If the experiment was committed on the way, the undo is committed too.
5. Ask Claude: *"Run npm run check:all."* It finds no problems.

## 2. Run the accessibility tests

You need something to open: a page or screen in your dev environment.

**Files only?** There's nothing to open yet, so skip to [4. Commit it](#4-commit-it). Ask Claude first: *"Note in the test log that the automated and manual accessibility tests are still to do, once the app is in a dev environment."* Come back to sections 2 and 3 once your app exists.

1. Get the address:
   - **Canvas app:** in Power Apps, open your app's **Details** and copy its **Web link**. It looks like `https://apps.powerapps.com/play/e/<environment-id>/a/<app-id>?tenantId=<tenant-id>`. Add `&hidenavbar=true` to the end.
   - **Power Pages:** the page's path on your dev site, such as `/<page path>`. The tests also need the site's address, which you give them in step 4.
   - **Model-driven app:** the form's address from your browser.
2. Ask Claude to add it:

   ```text
   Add my <screen or page name> to tests/accessibility/targets.json: type <canvas, page or
   model-driven>, auth true, waitFor "<the heading on the screen>", and this URL: <the address>
   ```

3. Save a sign-in for the tests. Claude Code is running in VS Code's terminal, so open a second one (**Terminal**, then **New Terminal**), and run this there. A browser opens: sign in with your test account, not your own.

   ```bash
   npm run test:a11y:login
   ```

   The sign-in is saved in `.auth/a11y-state.json`. It's a secret: Git ignores it, the assistant never commits it, and you must never share it. Sign-ins expire, so run this again when the tests say so.

4. Ask Claude to run the tests: *"Run the accessibility tests."* For a Power Pages page, give it your dev site's address: *"Run the accessibility tests against https://<your-dev-site>.powerappsportals.com."*

   They check for any WCAG 2.2 A or AA violation, and for Power Pages also sideways scrolling at 320 pixels wide and a visible focus indicator on every tab stop. If anything fails, ask Claude to explain and fix it, then run the tests again until they pass.

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

## 4. Commit it

Claude commits the test log, the test targets and anything else it changed when the end-of-run check passes, and tells you it's committed.

## Check

- [ ] The standards check caught the deliberate mistake, and the suppression without a reason
- [ ] `npm run check:all` finds no problems
- [ ] With a dev environment: your page or screen is in `targets.json` and passes with zero violations
- [ ] The test log has your manual tests, or, for files only, a note that the tests are still to do, and it's committed

## What just happened

There are three layers of checking, and each catches what the one before can't:

1. **The standards check** after every save: mechanical rules, many of them mapped to WCAG 2.2, run in milliseconds.
2. **The end-of-run review** on a smaller model: judgement about wording, naming and design, on just the files changed in the run.
3. **The check on GitHub**, whenever your work is pushed there: the backstop. It runs whatever tool wrote the code, or if no assistant was used at all.

And then people: the tests you just did by hand, which no tool replaces.

---

[← 09 Build it](09-build-it.md) · [Next: 11 Review your work →](11-review-your-work.md)
