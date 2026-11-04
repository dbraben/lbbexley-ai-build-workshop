# 06 Check the requirements (GitHub Copilot)

*About 20 minutes · No dev environment needed*

At the end of the conversation, Copilot writes the requirements in `docs/requirements.md` and shows you a summary in the chat: who uses the service and what they need, the user stories with their priorities, and the open questions. You check it in the chat, Copilot makes the changes, you commit them with two buttons, and you send the summary to the service owner. You don't need to open or edit the file.

## Steps

1. **Read the summary in the chat.** Check that:
   - each need is a need, not a solution
   - each user story has a priority: Must, Should, Could or Won't (this time)
   - nothing is invented: every rule has a source, and every number matches what you said
   - each open question says who can answer it
   - nobody is named
2. **Look at the acceptance criteria for the first Must story.** Ask, for example: *"Show me the acceptance criteria for R1."* Each one should be something a person or a test can check, including accessibility.
3. **Ask for changes in plain words.** For example:

   ```text
   R5 is a Could, not a Must.
   Split R3 into two stories: one for the people who make requests, one for the officers who handle them.
   ```

4. **Commit it.** Select **Check my work**: lbbexley-check reviews the requirements on a smaller model. If it finds problems, select **Fix what the check found**, then **Check my work** again. When it finds nothing outstanding, select **Commit the work**: lbbexley-build commits `docs/requirements.md` and tells you it's committed. Allow the `git` command it runs. Ignore **Build this plan** for now: it's for exercise 09.
5. **Send the summary to the service owner.** Ask:

   ```text
   Give me the summary as text for the service owner.
   ```

   Copy it into an email or a Teams message. This can wait until after the session. When the owner agrees, tell Copilot, for example *"The head of service agreed the requirements today"*: it records their role and the date. Then commit it again, as in step 4. Until then the requirements say *draft, not yet agreed*, and that's right.

## Check

- [ ] The summary has users and their needs, user stories with priorities, and open questions with who can answer them
- [ ] The first Must story's acceptance criteria are all things someone can check
- [ ] Nothing is invented, and nobody is named
- [ ] lbbexley-build said the requirements are committed
- [ ] You have the summary as text for the service owner

## What just happened

- lbbexley-check reviewed the requirements like any other change, then lbbexley-build committed them. Nothing in `docs/discovery/` is ever committed: Git ignores it.
- Every later step starts from this document: the design reads it, and each plan starts from one story.
- One story at a time keeps changes small: each can be planned, built, checked and reviewed on its own.

---

[← 05 Answer the requirements questions](../05-answer-the-requirements-questions.md) · [Next: 07 Design the service →](07-design-the-service.md)
