# 13 Wrap-up and next steps

*About 5 minutes · Both tracks*

## What you did

- Learned how the harness works: the three repositories, plan, build and check, and the guardrails.
- Created a service repository for your own project, and found the four places it refers to the Bexley standards.
- Answered questions about your project in the chat, or from a table for the service team, with everyone described by role and nobody's personal data going near the assistant.
- Checked requirements the service owner can agree, and a design, without writing a file yourself.
- Planned one story and built its first piece, with the standards checked after every save and at the end of every run, on a smaller model.
- Saw the checks catch a mistake, tested what you built by hand, and reviewed it to zero findings.
- Had every piece of work committed for you, without running Git.
- Sent an idea for improving the harness back to the Digital Team.

## The habits to keep

1. **Start from what people said.** Requirements come from the people who run and use the service, described by role, never from assumptions.
2. **One story per change.** Plan it, build it, check it, review it. Clear the session between changes; the plan in `docs/plans/` carries what matters.
3. **Plan features, not fixes.** Plan on the strongest model; skip planning for a one-line fix.
4. **Let the checks run.** Don't repeat them by hand during a build. Run the review once, when the story is finished.
5. **Add every page, screen and agent topic to its test list in the same change that builds it.**
6. **Zero findings is done.** Never weaken a check or suppress a finding without a written reason.

## Carry on with your project

- **The service team's answers.** When the table comes back, paste it into the chat, first line included, in any session: the requirements skill updates `docs/requirements.md` and shows you what changed.
- **The next story.** Ask the assistant which Must stories are left, and plan the next one in a fresh session, as in exercise 08.
- **New information.** After another conversation with the service team, run the requirements skill again and tell it what's new. If you recorded the conversation, clean the transcript first, as in [Use a Teams meeting transcript](use-a-teams-transcript.md).
- **Changes you make yourself.** If you change something in the dev environment yourself, in Power Apps Studio or the flow designer, ask the assistant to sync it (`/lbbexley:sync` in Claude Code, the lbbexley-sync skill in Copilot), so your repository keeps the latest version. The assistant commits and pushes it after the check, as usual.
- **The compliance documents** in `docs/compliance/` need real decisions from the service team before go-live: `npm run check:release` tells you what's left.
- **Sign-offs.** Agree with Information Governance and Communications the ones your service needs. The review tells you which.
- **New releases of the standards.** Exercise 12 says what to do when the Digital Team announces one.
- **The onboarding guide** in the standards repository, [docs/onboarding.md](https://github.com/dbraben/lbbexley-digital-standards/blob/main/docs/onboarding.md), covers everything else for a real service.

## Tidy up

- If you used a Teams transcript, delete the original and its roles file from Downloads once the service owner has agreed the requirements, unless your team's records rules say otherwise.
- In your dev environment, delete test records you no longer need, and anything you made only to try the harness.

## Tell us how it went

Open a [feedback issue](https://github.com/dbraben/lbbexley-ai-build-workshop/issues/new/choose) in this repository: what helped, what got in the way, and anything that didn't work as these instructions said.

---

[← Exercises](README.md)
