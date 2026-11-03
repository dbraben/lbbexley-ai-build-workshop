# 12 Improve the harness (Claude Code)

*About 10 minutes · No dev environment needed*

Each end-of-run review also asks whether the harness itself let you down: a mistake the standards check should have caught, guidance a skill was missing, a rule that got it wrong. Those ideas collect in `.lbbexley/improvements.md`. `/lbbexley:improve` turns them into changes, with people deciding.

## Steps

1. Make a branch from the latest `main`, and open `.lbbexley/improvements.md`:

   ```bash
   git switch main
   git pull
   git switch -c harness-ideas
   ```

   Each unticked line (`- [ ]`) is an idea the reviewer logged while you worked on your project, with its evidence. No ideas? Read on anyway: you'll have some after a few more stories.

2. Run:

   ```text
   /lbbexley:improve
   ```

3. Claude sorts the ideas into two groups and drops any with weak evidence:
   - **For this service**, such as a test target or a decision in `AGENTS.md`: it applies them here.
   - **For the Bexley standards**, such as a skill, a path rule or a check: it writes a proposal for each. It never edits the synced Bexley files in your repository, because the next update would overwrite them.
4. For proposals, Claude offers to open an issue in the standards repository with the GitHub CLI, labelled `harness-improvement`.

   > [!IMPORTANT]
   > In a guided session, ask the facilitator before opening real issues in the standards repository. Otherwise, just read the text Claude drafts.

5. Check that each idea is now ticked, with `(applied: ...)`, `(proposed: ...)` or `(dropped: ...)` after it. Commit the file and open a small pull request.
6. **See how an update arrives.** Find the release your repository is on: it's the version after `@` on the `uses:` line in `.github/workflows/quality.yml`, such as `v0.3.0`. Then run the update with that version:

   ```bash
   npm run standards:update -- <the version in quality.yml>
   ```

   Your repository is already on that release, so nothing changes. When the Digital Team announces a newer release, run the same command with the new version, always in a pull request of its own.

## Check

- [ ] Every idea in `.lbbexley/improvements.md` is ticked, with what happened to it
- [ ] You've read at least one proposal for the standards, or know where they'll appear

## What just happened

The loop goes:

1. The end-of-run review, on a smaller model, logs an idea with its evidence.
2. `/lbbexley:improve` applies the local ones and proposes the rest.
3. The Digital Team triages the proposals, with the sign-offs in the standards repository's GOVERNANCE.md.
4. Accepted ideas go into a release, and every service gets them with `npm run standards:update`.

Nothing in the standards changes without a person deciding.

---

[← 11 Review and open a pull request](11-review-and-pull-request.md) · [Next: 13 Wrap-up →](../13-wrap-up.md)
