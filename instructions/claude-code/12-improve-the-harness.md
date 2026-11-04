# 12 Improve the harness (Claude Code)

*About 10 minutes · No dev environment needed*

Each end-of-run review also asks whether the harness itself let you down: a mistake the standards check should have caught, guidance a skill was missing, a rule that got it wrong. Those ideas collect in `.lbbexley/improvements.md`. `/lbbexley:improve` turns them into changes, with people deciding.

## Steps

1. Run `/clear`, then:

   ```text
   /lbbexley:improve
   ```

   It reads the ideas the reviewer logged while you worked on your project, each with its evidence. If you're in plan mode, Claude shows its plan first: approve it as usual. No ideas? Read on anyway: you'll have some after a few more stories.

2. Claude sorts the ideas into two groups and drops any with weak evidence:
   - **For this service**, such as a test target or a decision in `AGENTS.md`: it applies them here.
   - **For the Bexley standards**, such as a skill, a path rule or a check: it writes a proposal for each. It never edits the synced Bexley files in your repository, because the next update would overwrite them.
3. For proposals, Claude offers to open an issue in the standards repository with the GitHub CLI, labelled `harness-improvement`.

   > [!IMPORTANT]
   > In a guided session, ask the facilitator before opening real issues in the standards repository. Otherwise, just read the text Claude drafts.

   Opening an issue needs the GitHub CLI (`gh`), signed in. Without it, Claude gives you the text to paste into the standards repository's **Harness improvement** issue form.

4. Claude marks each idea with what happened to it: applied, proposed or dropped. When the end-of-run check passes, it commits the changes.

## When there's a new release

You don't need to do this today. When the Digital Team announces a new release of the standards, such as `v0.5.0`:

1. Ask Claude: *"Update the Bexley standards to v0.5.0."* It runs `npm run standards:update -- v0.5.0`, which updates the synced Bexley files and the release the check on GitHub uses. Approve the command. Keep the update on its own, with no other work in the same request, so it's committed as a change of its own.
2. Update Claude Code's plugin. Run these in a terminal, then start Claude Code again:

   ```bash
   claude plugin marketplace update lbbexley-digital
   claude plugin update lbbexley@lbbexley-digital
   ```

## Check

- [ ] Every idea in `.lbbexley/improvements.md` is marked with what happened to it
- [ ] You've read at least one proposal for the standards, or know where they'll appear

## What just happened

The loop goes:

1. The end-of-run review, on a smaller model, logs an idea with its evidence.
2. `/lbbexley:improve` applies the local ones and proposes the rest.
3. The Digital Team triages the proposals, with the sign-offs in the standards repository's GOVERNANCE.md.
4. Accepted ideas go into a release, and every service gets them with `npm run standards:update`.

Nothing in the standards changes without a person deciding.

---

[← 11 Review your work](11-review-your-work.md) · [Next: 13 Wrap-up →](../13-wrap-up.md)
