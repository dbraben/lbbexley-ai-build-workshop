# 06 Write the requirements (Claude Code)

*About 20 minutes · No dev environment needed*

`/lbbexley:requirements` turns what's in `docs/discovery/` into `docs/requirements.md`: the users and what they need, user stories with priorities and acceptance criteria, rules, data, the duties that apply, what's out of scope, and open questions. It runs on Opus, the strongest model. Then you turn the stories into issues, so each one can be planned and built on its own.

## Steps

1. Run `/clear` to start a fresh conversation, and check you're in plan mode.
2. Make a branch for the work in exercises 06 to 11, named after your first piece of work, in lower case with hyphens:

   ```bash
   git switch -c <branch name>
   ```

   For example `git switch -c see-free-rooms`. Not sure yet? Call it `first-story`.

3. Run:

   ```text
   /lbbexley:requirements
   ```

   It reads everything in `docs/discovery/`. To use one file, name it: `/lbbexley:requirements docs/discovery/transcript-1.md`.

4. **If it stops for personal data**, it tells you which file and roughly where, without repeating it. Fix it as in [exercise 05](../05-capture-your-requirements.md), step 5, then run the command again.
5. **Answer its questions.** It asks what's missing, all at once. Answer what you can. For the rest, say who would know, for example:

   ```text
   I don't know the peak volumes: list that as an open question for the service manager.
   ```

6. Read what it plans to write, then approve the plan so it saves `docs/requirements.md`.
7. **Read `docs/requirements.md` carefully.** Check that:
   - the users and their needs are right, and each need is a need, not a solution
   - each user story has one need, a priority (Must, Should, Could or Won't), and acceptance criteria someone can check, including accessibility
   - every rule has a source, and every number matches what was said: nothing is invented
   - open questions say who can answer them
   - nobody is named, and nothing could identify a person
8. **Ask for changes in plain words.** For example:

   ```text
   Split R3 into two stories: one for the people who make requests, one for the officers who handle them.
   R5 is a Could, not a Must.
   The 10-working-day rule comes from the team's service standards: add that as its source.
   ```

9. **Ask the service owner to check it.** They don't need to read Markdown: copy the text into an email or Teams message, or show them the file on GitHub after exercise 11. Make their changes the same way.
10. **Commit the requirements.** Check that nothing from `docs/discovery/` is included, then commit:

    ```bash
    git status
    git add docs/requirements.md
    git commit -m "Add the requirements"
    ```

11. **Turn the stories into issues.** Ask Claude:

    ```text
    Draft an issue for each Must and Should story in docs/requirements.md.
    ```

    Read the drafts. When they're right, say *"Create them"*. Claude asks before it runs each `gh issue create` command: approve them. No GitHub CLI? Copy each draft into a new issue on GitHub, using the **Feature or change** form.

## Check

- [ ] `docs/requirements.md` has users and needs, user stories with priorities and acceptance criteria, rules with sources, and open questions with owners
- [ ] Nothing in it is invented, and nobody is named
- [ ] It's committed on your branch, and `docs/discovery/` isn't
- [ ] Your repository on GitHub has an issue for each Must and Should story

## What just happened

- The requirements skill checked your material for personal data before it read anything else, and turned gaps into open questions rather than guessing.
- Every later step starts from these requirements: the design reads them, and each plan starts from one story's user need and acceptance criteria.
- One story per issue keeps changes small: each can be planned, built, checked and reviewed on its own.

---

[← 05 Capture your requirements](../05-capture-your-requirements.md) · [Next: 07 Design the service →](07-design-the-service.md)
