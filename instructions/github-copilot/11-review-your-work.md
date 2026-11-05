# 11 Review your work (GitHub Copilot)

*About 10 minutes · No dev environment needed*

The **lbbexley-review** skill is the definition of done for a story. It runs the standards check, reviews what tools can't check against the Bexley checklist, checks the compliance documents, and reports what passes, what to fix and what needs a person to test. For anything people use, such as a screen or a page, it also runs the accessibility tests. Run it once per story, when you think the story is finished, not after every change: it's the most thorough check, and the slowest.

## Steps

1. Start a new chat, choose **lbbexley-build** (it can run commands) and ask:

   ```text
   Use the lbbexley-review skill.
   ```

   If typing `/` lists `lbbexley-review`, you can pick it from there instead. Your work is all on `main`, so it reviews the whole service.

2. Read the report. It starts with the result and a table showing each check as pass, fix or needs a person, then two lists:
   - **Must fix:** every item, however minor.
   - **Needs a person:** tests no tool can do for you, and sign-offs to ask for. You did the tests in exercise 10: check they're all in the test log.

   If you haven't built anything people use yet, it checks your documents only, and says the accessibility tests and the accessibility review don't apply. A screen or page you've built that the accessibility tests can't open is reported as a gap, not a pass.
3. **Check the compliance documents** it mentions. If your story collects or shows information about people, the DPIA screening in `docs/compliance/dpia-screening.md` needs it. Ask the agent to draft the parts the review lists; the decisions stay as `{{...}}` for the service team.
4. **Fix what it found.** Ask lbbexley-build to fix every item under **Must fix**, in the dev environment, then run the review again, until there's nothing under it. Then select **Check my work** and, when lbbexley-check finds nothing outstanding, **Commit the work**: lbbexley-build commits and pushes the fixes.
5. **See it on GitHub.** Every commit is pushed, so your work is already on GitHub. Open your repository's **Actions** tab: the **Quality** workflow ran the Bexley standards check again on each push, and passed.

## Check

- [ ] The review reports nothing under "Must fix"
- [ ] The tests that need a person are recorded in the test log
- [ ] lbbexley-build said the fixes are committed and pushed, and the **Quality** workflow passed on GitHub

## What just happened

- The check on GitHub doesn't depend on any assistant. Code written with Copilot, Claude Code or no assistant at all meets the same bar.
- Your requirements, design, plan and the latest version of what you built are committed in your repository and on GitHub, one commit for each piece of work, so anyone can see what was asked for, what was planned and what was built.

> [!NOTE]
> A team working on a real service may want a colleague to review each story before it joins `main`. With `main` protected on GitHub, the agent's push to it fails, and it tells you: then each story goes on a branch of its own with a pull request. Ask the Digital Team if your team wants to work that way. You don't need it for this workshop.

---

[← 10 Check and test](10-check-and-test.md) · [Next: 12 Improve the harness →](12-improve-the-harness.md)
