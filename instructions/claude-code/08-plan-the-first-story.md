# 08 Plan the first story (Claude Code)

*About 10 minutes · No dev environment needed*

Every change starts with a plan, on the strongest model. A Bexley plan has the user need, the exact words users will read, acceptance criteria someone can check, the files to change and the tests to add. Here you choose one story from your requirements and plan it, ready to build in exercise 09.

## Steps

1. **Choose the story.** Pick a Must story whose first piece you can build in under an hour, with what you have:

   | You have | Good first stories |
   |---|---|
   | No dev environment | One canvas app screen, built as source with made-up sample data |
   | A dev environment | A Dataverse table and the screen or form that uses it, one Power Pages page, one flow, or one agent topic |

   Too big? Ask Claude to split it: *"Story R2 is too big to build in an hour. Suggest how to split it."* Then pick the first part.

2. Run `/clear`, and check you're in plan mode.
3. **Ask Claude to plan it**, naming the story and its issue, and saying what you have. Choose the wording that fits:

   **With a dev environment:**

   ```text
   Plan story R<number> from docs/requirements.md (issue #<number>): <the story's short
   name>. Build it in my dev environment, in the solution named in AGENTS.md.
   ```

   **Files only:**

   ```text
   Plan story R<number> from docs/requirements.md (issue #<number>): <the story's short
   name>. There's no dev environment yet: build the screen as pa.yaml source only, with a
   named formula holding a few rows of made-up sample data instead of Dataverse.
   ```

4. Claude uses the plan skill, which runs on Opus. It reads `AGENTS.md`, `docs/requirements.md`, `docs/architecture.md` and the skill for your platform, then writes the plan.
5. **Read the plan.** Check it has:
   - the user need, from the story
   - the exact words users will read: headings, labels, hints, buttons, error messages, and what shows when there's nothing to show
   - acceptance criteria for accessibility, content and data, matching the story's
   - the files it will create or change, under `src/`
   - the tests: the page or screen in `tests/accessibility/targets.json`, or agent questions in `tests/agent-test-set.md`
6. **Ask for one change**, to see how planning works. For example: *"Use the words from the service team: they call them 'cases', not 'requests'."*
7. Leave the plan waiting for approval. You approve it at the start of exercise 09.

## Check

- [ ] The plan has the exact words users will read, and acceptance criteria someone can check
- [ ] The plan is saved in `docs/plans/`, and names the story and its issue
- [ ] Claude hasn't changed any other files yet

## What just happened

- In plan mode, Claude can read and search but not change files, so nothing happens until you approve.
- `opusplan` keeps planning on Opus. Approving switches to Sonnet, which does most of the work at lower cost.
- The template sets `plansDirectory` to `docs/plans`, so plans are kept with the code, and reviewers can compare what was planned with what was built.

---

[← 07 Design the service](07-design-the-service.md) · [Next: 09 Build it →](09-build-it.md)
