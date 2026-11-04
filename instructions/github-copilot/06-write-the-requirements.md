# 06 Write the requirements (GitHub Copilot)

*About 20 minutes · No dev environment needed*

Copilot writes one document, `docs/requirements.md`, from what you gave it in exercises 04 and 05: who uses the service and what they need, user stories with priorities and acceptance criteria, rules, data, the duties that apply, what's out of scope, and open questions. You read it, ask for changes, commit it, and turn its stories into issues.

## Where the requirements will be

`docs/requirements.md` is a file in your repository, **on your computer**. Open it in VS Code: in the Explorer, select **docs**, then **requirements.md**.

It isn't on GitHub until you push your branch in exercise 11, and then it's on your branch, not on `main`.

## Steps

1. **Make a branch** for exercises 06 to 11, named after your first piece of work, in lower case with hyphens:

   ```bash
   git switch -c <branch name>
   ```

   For example `git switch -c see-free-rooms`. Not sure yet? Call it `first-story`.

2. **Run the requirements skill.** Start a new chat, choose the **lbbexley-plan** agent, and ask:

   ```text
   Use the lbbexley-requirements skill.
   ```

   It reads `AGENTS.md` and everything in `docs/discovery/`, sums up what it already knows, then asks about what's missing, all at once. Answer what you can. For the rest, say who would know, for example:

   ```text
   I don't know the peak volumes: list that as an open question for the service manager.
   ```

   If it stops for personal data, it says which file and roughly where. Fix it as in [exercise 05](../05-capture-your-requirements.md), step 5, then ask again.

3. **Open `docs/requirements.md` in VS Code and read it.** Check that:
   - each need is a need, not a solution
   - each user story has a priority (Must, Should, Could or Won't) and acceptance criteria someone can check, including accessibility
   - nothing is invented: every rule has a source, and every number matches what was said
   - each open question says who can answer it
   - nobody is named
4. **Ask for changes in plain words.** Copilot changes the file, and VS Code shows the new version. For example:

   ```text
   R5 is a Could, not a Must.
   Split R3 into two stories: one for the people who make requests, one for the officers who handle them.
   ```

5. **Commit it.** Run `git status` first: nothing in `docs/discovery/` should be listed. Then:

   ```bash
   git add docs/requirements.md
   git commit -m "Add the requirements"
   ```

6. **Turn the stories into issues.** Ask lbbexley-plan:

   ```text
   Draft an issue for each Must and Should story in docs/requirements.md.
   ```

   Read the drafts. The plan agent can't run commands, so to create them, choose **lbbexley-build** and ask: *"Create the issues drafted above with the GitHub CLI, one at a time."* Allow each `gh issue create` command. No GitHub CLI? Copy each draft into a new issue on GitHub, using the **Feature or change** form.

7. **Ask the service owner to check it.** This can wait until after the session. They don't need to read Markdown: copy the text into an email or Teams message. When they agree, ask Copilot to record their role and the date at the top. Until then it says *draft, not yet agreed*, and that's right.

## Check

- [ ] `docs/requirements.md` opens in VS Code, with users and needs, user stories with priorities and acceptance criteria, rules with sources, and open questions with owners
- [ ] Nothing in it is invented, and nobody is named
- [ ] It's committed on your branch, and `docs/discovery/` isn't
- [ ] Your repository on GitHub has an issue for each Must and Should story

## What just happened

- The requirements skill checked your material for personal data before anything else, and turned gaps into open questions rather than guessing.
- Every later step starts from this file: the design reads it, and each plan starts from one story.
- One story per issue keeps changes small: each can be planned, built, checked and reviewed on its own.

---

[← 05 Capture your requirements](../05-capture-your-requirements.md) · [Next: 07 Design the service →](07-design-the-service.md)
