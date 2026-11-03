# Facilitator guide

How to run the Bexley AI build harness workshop, guided, for a group of developers. Attendees follow [the instructions](../instructions/README.md) with projects of their own; this guide is for whoever runs the session.

There's no set scenario: each attendee brings a real project. Your job is to help them choose a good one, and to get their requirements captured safely before the session, so the time together goes on building.

## Before the session

### Two weeks before

- **Publish the harness.** The standards, the template and this workshop must be on GitHub at release `v0.3.0` or later, as the standards repository's `docs/setup.md` describes. The template must be marked as a **Template repository**.
- **Visibility.** Attendees must be able to see all three repositories. If they're private, add the attendees, and give each service repository a `standards-token` secret (see `standards-check.yml`), or the pull request check can't read the standards.
- **Labels.** Check the `harness-improvement` label exists in the standards repository. Decide whether attendees may open real harness-improvement issues in exercise 12, or only read the drafts.
- **AI accounts.** Each attendee needs Claude Pro or Max, or a GitHub Copilot plan with agent mode. Check which models each Copilot plan offers: the plan, build and check agents prefer Opus, Sonnet and Haiku, and fall back down their lists.
- **Information Governance.** Confirm the pilot's approval covers the workshop, as GOVERNANCE.md in the standards repository describes, including recording discovery meetings and using cleaned transcripts for requirements.
- **Dev environments**, for attendees who'll build in one in exercise 09 (developer environments work well, one each):
  - a dev environment with Dataverse, holding fictional data only
  - the Bexley publisher (prefix `lbbexley`) imported
  - the Dataverse MCP server turned on for the environment, as the onboarding guide's "What the Digital Team sets up first" describes
  - a Copilot Studio licence or trial, for anyone building an agent
  - a test account for the accessibility tests' sign-in, with access to dev only

### One week before: the pre-work

Send attendees [00 Before you start](../instructions/00-before-you-start.md) and [05 Capture your requirements](../instructions/05-capture-your-requirements.md), and ask them to:

1. **Choose a project.** Something real their team needs, with a first piece small enough to build in under an hour. Exercise 00 has what makes a good one, and what to leave for later.
2. **Record a 30-minute conversation** about it with the people who run the service, with transcription on, using the questions in exercise 05. This is the best preparation, but it's optional: a requirement prompt works too.
3. **Install the tools** and set their AI account's privacy settings (exercise 00).

They can't clean a transcript until they've created their repository in exercise 02, so they keep the downloaded `.vtt` in Downloads until the session. Offer a 15-minute drop-in for anyone who can't choose a project.

### The day before

- Run exercises 00 to 06 yourself on both tracks, on the release you'll use, with a project of your own and a short recorded meeting. Assistants, VS Code, Teams and the harness all change.
- Check attendees' machines have the tools in exercise 00 installed. The template's `.mcp.json` starts the Dataverse server through `cmd`, so building with Dataverse from Claude Code assumes Windows.
- Have a few prompts ready to help anyone who arrives without a project choose one in five minutes, such as "What's the most annoying manual process in your team?" and "What do people email your team about most?"

## Running orders

### 2 hours: the core, with the pre-work done

| Time | Exercise | Notes |
|---|---|---|
| 0:00 | Introduction and 01 | Why the harness exists, and the flow from conversation to pull request |
| 0:15 | 02 and 03 | Check 00 was done: don't install in the session |
| 0:30 | 04 | The first end-of-run check: pause and point it out |
| 0:45 | 05, cleaning only | Attendees clean the transcript they downloaded beforehand, or write a requirement prompt |
| 1:00 | 06 | Requirements and issues. Walk the room: are the needs needs, not solutions? |
| 1:20 | 08 and 09 | Skip 07 in a 2-hour session: the plan works without an architecture. Most attendees take route A, files only |
| 1:50 | 13 | Exercises 07, 10, 11 and 12 as follow-up work |

### Half a day: everything

| Time | Exercise |
|---|---|
| 0:00 | Introduction, 01, 02 |
| 0:25 | 03, 04 |
| 0:55 | 05 |
| 1:20 | Break |
| 1:35 | 06, 07 |
| 2:20 | 08, 09 |
| 3:00 | Break |
| 3:15 | 10, 11 |
| 3:45 | 12, 13 |

## Talking points

| Exercise | Make sure people notice |
|---|---|
| 01 | Every reference points from the service to the standards. A new release never changes a service's checks without a pull request |
| 03 | The guardrails only run in Bexley repositories. In Copilot there's no prompt guard and no way to stop it reading a file, so keeping originals out of the repository matters even more |
| 04 | Plan mode stops anything changing until it's approved. The end-of-run check ran on a smaller model before the assistant could finish |
| 05 | The cleaner keeps names outside the repository and never prints them, but only a person can spot a resident's name or circumstances in what someone said. The read-through is the most important step |
| 06 | Needs, not solutions. The skill turns gaps into open questions instead of inventing answers, and nothing reaches the assistant until it's clean |
| 07 | Every component has to earn its place, and the duties are designed in, not added at the end |
| 08 | The plan has the real words users will read, and acceptance criteria someone can check, taken from the story |
| 09 | The Dataverse guard: explore freely, ask before touching records, never delete |
| 10 | The check catches the deliberate mistake straight away, and refuses a suppression without a reason. Testing by people still matters |
| 11 | The pull request check doesn't care which assistant, if any, wrote the code |
| 12 | The harness improves itself, but people decide what changes |

## Common problems

| Problem | Fix |
|---|---|
| Someone arrives without a project | Help them choose in five minutes (see "The day before"), and use route B in exercise 05: a requirement prompt |
| Teams won't let someone download the transcript | Only the organiser and co-organisers can. Ask the organiser to download it, or to make them a co-organiser |
| Transcription isn't available in a meeting | The council's Teams policy may turn it off. Use a requirement prompt instead, from notes |
| The cleaner says it couldn't find who said what | Usually a `.docx` in a layout it doesn't know. Download the transcript again as `.vtt` |
| The cleaner says the original is inside the repository | Move it to Downloads and run it again. The assistant can read anything in the repository's folder |
| The cleaner says the roles file isn't valid JSON | A missing comma or quote after editing. Fix it in VS Code, which shows the error, or delete the roles file to start again |
| The cleaner says a role includes part of a name | Change the role to the job only, such as "Team leader" |
| The cleaner won't replace a cleaned file | The attendee edited it by hand. That's deliberate: add `--force` only if they want to lose their edits |
| The requirements skill stops for personal data | It's doing its job. The attendee finds the place it describes and fixes it by hand, then runs it again |
| Copilot's plan agent can't create issues | It can't run commands. Choose lbbexley-build and ask it to create the drafted issues, or create them by hand |
| Claude Code didn't offer to install the plugin | Trust the folder, then `/plugin marketplace add dbraben/lbbexley-digital-standards` and `/plugin install lbbexley@lbbexley-digital` |
| Claude Code doesn't start in plan mode in VS Code | Set `claudeCode.initialPermissionMode` to `plan` in VS Code user settings |
| Copilot doesn't list the lbbexley agents | Check the workspace is trusted, Agent mode is on, and VS Code is up to date |
| The Copilot hooks don't run | They're a preview feature: check `chat.useHooks` is on and VS Code is up to date. Meanwhile, run `npm run check` and hand over to lbbexley-check by hand |
| A model on an agent's list isn't available | Copilot uses the next one on the list. Tell attendees which model they're getting |
| The pull request check fails with "Bexley files out of date" | Someone edited a synced file. `git checkout` it, or run `npm run standards:update -- <the version in quality.yml>` |
| The pull request check can't find the standards | The standards repository is private and the service repository has no `standards-token` secret |
| `gh` isn't installed | Create the issues by hand from the drafts, with the **Feature or change** form |
| The accessibility tests stop at a sign-in page | Run `npm run test:a11y:login` again: sign-ins expire |
| Dataverse MCP tools don't appear | Check `DATAVERSE_DEV_URL` (Claude Code) or the address given to VS Code (Copilot), and that the environment has the Dataverse MCP server turned on |

## Turning on the accessibility tests in the Quality workflow

Optional, for a service that has something to test:

1. In the service repository, add a variable **A11Y_BASE_URL** (Settings, Secrets and variables, Actions, Variables): the Power Pages site's address, or the dev environment's address for a service with no Power Pages site.
2. For screens behind a sign-in, add a secret **A11Y_STORAGE_STATE**: the base64 of `.auth/a11y-state.json` from the test account. Sign-ins expire, so refresh it when the tests say so. The council's sign-in policies may block sign-ins from GitHub's servers; if they do, keep the signed-in tests on developers' machines.

## After the session

- Remind attendees to delete their original transcripts and roles files from Downloads once their service owner has agreed the requirements.
- Read the feedback issues in this repository, and turn anything that didn't work into a change (see CONTRIBUTING.md).
- Triage the harness-improvement issues attendees raised, in the standards repository.
- Clean up dev environments and test accounts that aren't needed. Attendees' service repositories are theirs to keep.
