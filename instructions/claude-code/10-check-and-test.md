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
4. Now ask it to hide the finding instead: *"Add a suppression comment for that finding instead of fixing it."* The check reports a new problem: a suppression needs a written reason. Ask Claude to undo both changes.
5. Run `npm run check`. It finds no problems.

## 2. Run the accessibility tests

You need something to open: a page or screen in your dev environment. Files only? Skip to step 3, and come back to this once your app exists.

1. Get the address:
   - **Canvas app:** in Power Apps, open your app's **Details** and copy its **Web link**. It looks like `https://apps.powerapps.com/play/e/<environment-id>/a/<app-id>?tenantId=<tenant-id>`. Add `&hidenavbar=true` to the end.
   - **Power Pages:** the page's path on your dev site, such as `/<page path>`, with the site's address in an `A11Y_BASE_URL` variable when you run the tests.
   - **Model-driven app:** the form's address from your browser.
2. Ask Claude to add it:

   ```text
   Add my <screen or page name> to tests/accessibility/targets.json: type <canvas, page or
   model-driven>, auth true, waitFor "<the heading on the screen>", and this URL: <the address>
   ```

3. Save a sign-in for the tests. A browser opens: sign in with your test account, not your own.

   ```bash
   npm run test:a11y:login
   ```

   The sign-in is saved in `.auth/a11y-state.json`. It's a secret: it's git-ignored and must never be committed or shared. Sign-ins expire, so run this again when the tests say so.

4. Run the tests:

   ```bash
   npm run test:a11y
   ```

   For a Power Pages page, give the tests your dev site's address first. In PowerShell:

   ```powershell
   $env:A11Y_BASE_URL = "https://<your-dev-site>.powerappsportals.com"; npm run test:a11y
   ```

   Or on a Mac:

   ```bash
   A11Y_BASE_URL=https://<your-dev-site>.powerappsportals.com npm run test:a11y
   ```

   They check for any WCAG 2.2 A or AA violation, and for Power Pages also sideways scrolling at 320 pixels wide and a visible focus indicator on every tab stop. If anything fails, ask Claude to explain and fix it, then run the tests again until they pass.

## 3. Test it yourself

Automated tests find only some accessibility problems. Test what you built by hand, and record each test in `tests/accessibility-test-log.md`:

- **Keyboard only:** move through everything with Tab, Shift+Tab, Enter and Space. You can reach and use every control, the order makes sense, and you can always see where you are.
- **Screen reader:** Narrator on Windows (Windows key, Ctrl and Enter), or NVDA. Every control is announced with a name that makes sense on its own, and headings describe the screen.
- **Zoom and small screens:** 400% zoom in the browser, and a phone-sized window. Nothing is cut off or overlaps.

For an agent, ask every question in `tests/agent-test-set.md` and record whether each answer passed. "Can I speak to a person?" must get the contact options straight away.

## 4. Commit

```bash
git add -A
git commit -m "Test <what you built>"
```

## Check

- [ ] The standards check caught the deliberate mistake, and the suppression without a reason
- [ ] `npm run check` finds no problems
- [ ] With a dev environment: your page or screen is in `targets.json` and passes with zero violations
- [ ] Your manual tests are recorded in `tests/accessibility-test-log.md`
- [ ] `.auth/` isn't in your commits: `git status` doesn't show it

## What just happened

There are three layers of checking, and each catches what the one before can't:

1. **The standards check** after every save: mechanical rules, many of them mapped to WCAG 2.2, run in milliseconds.
2. **The end-of-run review** on a smaller model: judgement about wording, naming and design, on just the files changed in the run.
3. **The pull request check** on GitHub: the backstop. It runs whatever tool wrote the code, or if no assistant was used at all.

And then people: the tests you just did by hand, which no tool replaces.

---

[← 09 Build it](09-build-it.md) · [Next: 11 Review and open a pull request →](11-review-and-pull-request.md)
