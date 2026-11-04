# 11 Review and open a pull request (Claude Code)

*About 10 minutes · No dev environment needed*

`/lbbexley:review` is the definition of done before a pull request. It runs the standards check, has the compliance reviewer check what tools can't, checks the compliance documents, and reports what passes, what to fix and what needs a person to test. For anything people use, such as a screen or a page, it also runs the accessibility tests and the accessibility reviewer. Run it once per pull request, not after every change: it's the most thorough check, and the slowest.

## Steps

1. Run `/clear`, then:

   ```text
   /lbbexley:review
   ```

2. Read the report. It starts with the result and a table showing each check as pass, fix or needs a person, then two lists:
   - **Must fix:** fix every item, however minor. Ask Claude to fix them, then run the review again.
   - **Needs a person:** tests no tool can do for you, and sign-offs to ask for. You did the tests in exercise 10: check they're all in the test log.

   If you haven't built anything people use yet, it checks your documents only, and says the accessibility tests and the accessibility review don't apply. A screen or page you've built that the accessibility tests can't open is reported as a gap, not a pass.
3. **Check the compliance documents** it mentions. If your story collects or shows information about people, the DPIA screening in `docs/compliance/dpia-screening.md` needs it. Ask Claude to draft the parts the review lists; the decisions stay as `{{...}}` for the service team.
4. **Push your branch and open a pull request:**

   ```bash
   git push -u origin <branch name>
   ```

   Use the branch you made in exercise 06: `git branch` shows it.

   On GitHub, open the pull request and fill in the template:
   - link the issue: put `Closes #<issue number>` in the description, so the issue closes when the pull request is merged
   - link the plan in `docs/plans/`
   - tick what you've done, and leave unticked what you haven't

5. **Watch the Quality workflow.** **Bexley standards** checks every file the pull request changes, and fails on any finding. It also fails if anyone edited the synced Bexley files by hand.
6. **Ask a colleague to review** the pull request: the requirements, the design and the build. If the service owner has a GitHub account, ask them to look at `docs/requirements.md` too. Then merge it.

## Check

- [ ] The review reports nothing under "Must fix"
- [ ] The tests that need a person are recorded in the test log
- [ ] The pull request closes the story's issue, passed **Bexley standards**, was reviewed and is merged

## What just happened

- The review used two reviewer agents on Sonnet, and the end-of-run checks used Haiku: each check runs on the smallest model that does it well.
- The pull request check doesn't depend on any assistant. Code written with Copilot, Claude Code or no assistant at all meets the same bar.
- Your requirements, design, plan and build are now in one reviewed change: anyone can see what was asked for, what was planned and what was built.

---

[← 10 Check and test](10-check-and-test.md) · [Next: 12 Improve the harness →](12-improve-the-harness.md)
