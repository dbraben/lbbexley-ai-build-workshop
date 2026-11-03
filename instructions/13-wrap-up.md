# 13 Wrap-up and next steps

*About 5 minutes · Both tracks*

## What you did

- Learned how the harness works: the three repositories, plan, build and check, and the guardrails.
- Created a service repository for your own project, and found the four places it refers to the Bexley standards.
- Captured your requirements from a cleaned Teams transcript or your own requirement prompt, without any personal data going near the assistant.
- Turned them into requirements the service owner can check, a design, and an issue for each story.
- Planned one story and built its first piece, with the standards checked after every save, at the end of every run on a smaller model, and on the pull request.
- Saw the checks catch a mistake, tested what you built by hand, and opened a reviewed pull request.
- Sent an idea for improving the harness back to the Digital Team.

## The habits to keep

1. **Start from what people said.** Requirements come from the people who run and use the service, cleaned of personal data, never from assumptions.
2. **One story per change.** Plan it from its issue, build it, check it, review it. Clear the session between changes; the plan in `docs/plans/` carries what matters.
3. **Plan features, not fixes.** Plan on the strongest model; skip planning for a one-line fix.
4. **Let the checks run.** Don't repeat them by hand during a build. Run the review once, before the pull request.
5. **Add every page, screen and agent topic to its test list in the same change that builds it.**
6. **Zero findings is done.** Never weaken a check or suppress a finding without a written reason.

## Carry on with your project

- **The next story.** Pick the next Must from your issues, and plan it in a fresh session, as in exercise 08.
- **New information.** After another conversation with the service team, clean the new transcript (exercise 05) and run the requirements skill again. It updates `docs/requirements.md`; check what changed before you commit it.
- **The compliance documents** in `docs/compliance/` need real decisions from the service team before go-live: `npm run check:release` tells you what's left.
- **Sign-offs.** Agree with Information Governance and Communications the ones your service needs. The review tells you which.
- **The onboarding guide** in the standards repository, [docs/onboarding.md](https://github.com/dbraben/lbbexley-digital-standards/blob/main/docs/onboarding.md), covers everything for a real service, including moving it to the council's GitHub.

## Tidy up

- Delete the original transcript and its roles file from Downloads once the service owner has agreed the requirements, unless your team's records rules say otherwise.
- In your dev environment, delete test records you no longer need, and anything you made only to try the harness.

## Tell us how it went

Open a [feedback issue](https://github.com/dbraben/lbbexley-ai-build-workshop/issues/new/choose) in this repository: what helped, what got in the way, and anything that didn't work as these instructions said.

---

[← Exercises](README.md)
