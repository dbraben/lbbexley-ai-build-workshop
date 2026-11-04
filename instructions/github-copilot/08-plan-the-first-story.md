# 08 Plan the first story (GitHub Copilot)

*About 10 minutes · No dev environment needed*

Every change starts with a plan, on the strongest model. A Bexley plan has the user need, the exact words users will read, acceptance criteria someone can check, the files to change and the tests to add. Here you choose one story from your requirements and plan it, ready to build in exercise 09.

## Steps

1. **Choose the story.** Pick a Must story whose first piece you can build in under an hour, with what you have:

   | You have | Good first stories |
   |---|---|
   | No dev environment | One canvas app screen, built as source with made-up sample data |
   | A dev environment | A Dataverse table and the screen or form that uses it, one Power Pages page, one flow, or one agent topic |

   Too big? Ask lbbexley-plan to split it: *"Story R2 is too big to build in an hour. Suggest how to split it."* Then pick the first part.

2. Start a new chat and choose the **lbbexley-plan** agent.
3. **Ask it to plan the story**, naming the story and saying what you have. Choose the wording that fits:

   **With a dev environment:**

   ```text
   Plan story R<number> from docs/requirements.md: <the story's short name>.
   Build it in my dev environment, in the solution named in AGENTS.md.
   ```

   **Files only:**

   ```text
   Plan story R<number> from docs/requirements.md: <the story's short name>.
   There's no dev environment yet: build the screen as pa.yaml source only, with a named
   formula holding a few rows of made-up sample data instead of Dataverse.
   ```

   > [!NOTE]
   > Skipped exercise 07, so there's no design yet? Add this line to the end of the request, so lbbexley-plan doesn't stop to offer one first: *"There's no design yet: plan the story from the requirements."*

4. The agent uses the **lbbexley-plan** skill and writes the plan to `docs/plans/`. It reads `AGENTS.md`, `docs/requirements.md`, `docs/architecture.md` and the skill for your platform first.
5. **Read the plan.** Check it has:
   - the user need, from the story
   - the exact words users will read: headings, labels, hints, buttons, error messages, and what shows when there's nothing to show
   - acceptance criteria for accessibility, content and data, matching the story's
   - the files it will create or change, under `src/`
   - the tests: the page or screen in `tests/accessibility/targets.json`, or agent questions in `tests/agent-test-set.md`
6. **Ask for one change**, to see how planning works. For example: *"Use the words from the service team: they call them 'cases', not 'requests'."*
7. Don't select **Build this plan** yet. You do that at the start of exercise 09. If lbbexley-plan asks you to select **Check my work** for the plan, you can skip it: the plan is checked with what you build.

## Check

- [ ] The plan is in `docs/plans/`, and names the story
- [ ] It has the exact words users will read, and acceptance criteria someone can check
- [ ] Nothing outside `docs/` has changed

## What just happened

- The plan agent is told to write only documents in `docs/`, so nothing is built until you hand over.
- The plan is kept with the code, so reviewers can compare what was planned with what was built.

---

[← 07 Design the service](07-design-the-service.md) · [Next: 09 Build it →](09-build-it.md)
