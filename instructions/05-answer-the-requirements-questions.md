# 05 Answer the requirements questions

*About 20 minutes · Both tracks · No dev environment needed*

Requirements come from the people who run and use the service. The requirements skill gets them in a conversation: it asks about your project in the chat, a few questions at a time, and writes the requirements for you. You don't create or edit any files.

There are two ways to answer, and you can switch at any time:

| | Use it when |
|---|---|
| **Answer here** | You know the project well enough to answer now, in the chat |
| **Answer later** | The service team should answer. You get the questions as a table to copy into an email, a Teams chat or a document, and you paste it back into the chat when it's filled in |

> [!TIP]
> Recorded a Teams meeting with the service team? Clean the transcript first, and the skill reads it before it asks anything, so it asks fewer questions: see [Use a Teams meeting transcript](use-a-teams-transcript.md). It's optional.

## Steps

1. **Start the conversation.**
   - **Claude Code:** press Shift+Tab until the line below the prompt says **⏵⏵ accept edits on**, then run `/lbbexley:requirements`. Claude saves the requirements as it goes, so it doesn't need to plan first.
   - **GitHub Copilot:** start a new chat, choose the **lbbexley-plan** agent, and ask: *"Use the lbbexley-requirements skill."*
2. **Check what it already knows.** It starts with three or four points from the set-up in exercise 04. Correct anything that's wrong, in plain words.
3. **Choose how to answer.** Say *"Answer here"*, or *"Answer later: give me the questions as a table"*.

### Answering here

4. It asks two or three questions at a time, each with a short example. Answer in your own words:
   - Describe the need, not the solution: "officers need to see which requests are overdue", not "a red column in a table".
   - Give numbers if you have them: how many requests, how often, how long things take now.
   - Say where each rule comes from: "we must reply within 10 working days (complaints policy)".
   - Don't know? Say who would, for example *"I don't know the peak volumes: ask the service manager"*. It becomes an open question, not a guess.
5. After each answer, it says in a line what it noted. If it got something wrong, say so straight away.
6. Want the rest as a table after all? Say *"Give me the rest as a table"*, and carry on as below.

### Answering later

4. It writes down what it knows so far, with each unanswered question numbered Q1, Q2 and so on, then gives you the questions in a box. For example:

   ```text
   Bexley requirements answers · Room bookings · questions of 4 November 2026

   | # | Question | Answer |
   |---|---|---|
   | Q1 | Who will use it, and on what devices? (for example: residents applying for a permit, mostly on phones) | |
   ```

5. **Let it finish, then copy the table.** In Claude Code, the end-of-run check runs after the table, then Claude commits the draft requirements and says so: those messages appear below the table. In Copilot, lbbexley-plan may ask you to select **Check my work**: do that, then **Commit the work**, to commit the draft.

   The table is saved in `docs/discovery/requirements-questions.md` too, which Git ignores: open that file from VS Code's Explorer and copy it from there. Or copy it from the chat: in Copilot, hover over the box and select the copy button; in Claude Code, select it in the terminal from the first line to the last, and copy it (Ctrl+C, or Cmd+C on a Mac).
6. **Send it to the service team.** Paste it into an email, a Teams chat or a document. Ask them to fill in what they can, leave gaps for what nobody knows, and describe people by role, never by name.
7. **Paste it back** when it's filled in: the whole thing, **including the first line**. That line tells the assistant what it is and where you'd got to, even in a new session days later. Start the session as in step 1, then paste it.

In the workshop you won't have the team's answers yet. Fill in what you can yourself, paste it back, and carry on. Paste the team's answers in when they arrive.

### Either way

- **Describe people by role, never by name**, and don't paste anyone's details: "a resident who rings several times", not a name. If the assistant finds anything that could identify someone, it stops and asks you to say it again without the person. In Claude Code, a message with real-looking personal data in it, such as an email address, is stopped before it's sent.
- When it has enough, it writes the requirements and shows you a summary in the chat. Checking it is the next exercise.

## Check

- [ ] The assistant asked about your project in the chat, and you answered there, or pasted the table back
- [ ] Everyone is described by role, and nobody's details are in your answers
- [ ] It showed you a summary of the requirements

## What just happened

- You didn't create or edit a file: the assistant asked, and it writes the requirements.
- It asked only what the set-up hadn't already told it, and turned every "don't know" into an open question with who can answer it, instead of guessing.
- The requirements skill runs on the strongest model: Opus in Claude Code, whatever mode you're in, and the plan agent's model in Copilot.

---

Previous: 04 Set up your service, for [Claude Code](claude-code/04-set-up-your-service.md) or [GitHub Copilot](github-copilot/04-set-up-your-service.md) · Next: 06 Check the requirements, for [Claude Code →](claude-code/06-check-the-requirements.md) or [GitHub Copilot →](github-copilot/06-check-the-requirements.md)
