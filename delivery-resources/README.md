# Facilitator guide

How to run the Bexley AI build harness workshop, guided, for a group of developers. Attendees follow [the instructions](../instructions/README.md) with projects of their own; this guide is for whoever runs the session.

There's no set scenario: each attendee brings a real project. Your job is to help them choose a good one, and to come knowing enough about it to answer the requirements questions, so the time together goes on building.

## Before the session

### Two weeks before

- **Publish the harness.** The standards, the template and this workshop must be on GitHub at release `v0.6.1` or later, as the standards repository's `docs/setup.md` describes. The template must be marked as a **Template repository**.
- **Visibility.** Attendees must be able to see all three repositories. If they're private, add the attendees, and give each service repository a `standards-token` secret (see `standards-check.yml`), or the check on GitHub can't read the standards.
- **Labels.** Check the `harness-improvement` label exists in the standards repository. Decide whether attendees may open real harness-improvement issues in exercise 12, or only read the drafts. Opening them needs the GitHub CLI (`gh`), signed in, on attendees' computers.
- **AI accounts.** Each attendee needs Claude Pro or Max, or a GitHub Copilot plan with agent mode. Check which models each Copilot plan offers: the plan, build and check agents prefer Opus, Sonnet and Haiku, and fall back down their lists.
- **Information Governance.** Confirm the pilot's approval covers the workshop, as GOVERNANCE.md in the standards repository describes, including, for attendees who use them, recording discovery meetings and using cleaned transcripts for requirements.
- **Dev environments, one for each attendee.** Everyone builds in one from exercise 08 on: there's no route without one. Developer environments work well. Each needs:
  - Dataverse, holding fictional data only
  - the Bexley publisher (prefix `lbbexley`) imported
  - the Dataverse MCP server turned on for the environment, as the onboarding guide's "What the Digital Team sets up first" describes
  - a Copilot Studio licence or trial, for anyone building an agent
  - a test account for the accessibility tests' sign-in, with access to dev only
  - coauthoring allowed for canvas apps, and data policies that let Microsoft's canvas and Power Automate tools work. Check that the council's sign-in policies let attendees sign in to the Azure CLI (`az login`), which Microsoft's Power Automate tools use

### One week before: the pre-work

Send attendees [00 Before you start](../instructions/00-before-you-start.md), and ask them to:

1. **Choose a project.** Something real their team needs, with a first piece small enough to build in under an hour. Exercise 00 has what makes a good one, and what to leave for later.
2. **Gather what they know** about it, and ideally talk to the people who run the service. In the session, the requirements skill asks its questions in the chat, and anything they can't answer goes to the service team as a table they paste back later. Recording the conversation is optional: [Use a Teams meeting transcript](../instructions/use-a-teams-transcript.md) has the questions to ask and how to record it.
3. **Install the tools**, set their AI account's privacy settings, and check Git knows their name (exercise 00).

Anyone who records a meeting can't clean the transcript until they've created their repository in exercise 02, so they keep the downloaded `.vtt` in Downloads until the session. Offer a 15-minute drop-in for anyone who can't choose a project.

### The day before

- Run exercises 00 to 06 yourself on both tracks, on the release you'll use, with a project of your own. In exercise 05, try both ways of answering: in the chat, and pasting the table back in a new session. Then build one canvas app screen and one flow in a dev environment, as exercise 09 does, to check Microsoft's canvas and Power Automate tools work on the council's tenant, and that the latest version reaches GitHub. Assistants, VS Code, Teams and the harness all change.
- Check attendees' machines have the tools in exercise 00 installed, including Claude Code's command-line version for the Claude Code track: `claude --version` works in VS Code's terminal. The template's `.mcp.json` starts the Dataverse server through Windows' `cmd`, so Claude Code attendees on a Mac or Linux who build with Dataverse add their own server instead, as exercise 09 shows. Try that on a Mac before the session if anyone will use one.
- Have a few prompts ready to help anyone who arrives without a project choose one in five minutes, such as "What's the most annoying manual process in your team?" and "What do people email your team about most?"

## Running orders

### 2½ hours: the core, with the pre-work done

| Time | Exercise | Notes |
|---|---|---|
| 0:00 | Introduction and 01 | Why the harness exists, and the flow from a conversation to working software |
| 0:20 | 02 and 03 | Check 00 was done: don't install in the session |
| 0:40 | 04 | The first end-of-run check, and the commit and push after it: pause and point them out |
| 0:55 | 05 | Most attendees answer in the chat. Ask anyone with a transcript to clean it before the session |
| 1:15 | 06 | Walk the room: are the needs needs, not solutions? |
| 1:35 | 08 and 09 | Skip 07 in this session: the plan works without an architecture. Exercise 08 tells attendees to say so when they ask for the plan, or Copilot's lbbexley-plan offers to design the service first. Check everyone did "Set up your dev environment once" before the session: it's the slowest part |
| 2:15 | 13 | Exercises 07, 10, 11 and 12 as follow-up work. Their work is on GitHub already: the assistant pushed it |

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
| 01 | Every reference points from the service to the standards. A new release never changes a service's checks until the service updates |
| 03 | The guardrails only run in Bexley repositories. In Copilot there's no prompt guard and no way to stop it reading a file, so keeping originals out of the repository matters even more |
| 04 | Plan mode stops anything changing until it's approved. The end-of-run check ran on a smaller model before the assistant could finish, then the assistant committed the set-up and pushed it to GitHub: nobody ran Git |
| 05 | The skill asks only what it doesn't already know, a few questions at a time, and turns "don't know" into an open question instead of inventing an answer. The table's first line, "Bexley requirements answers", is how it knows where it was when the answers come back |
| The transcript page | The cleaner keeps names outside the repository and never prints them, but only a person can spot a resident's name or circumstances in what someone said. The read-through is the most important step |
| 06 | Needs, not solutions. Everything is checked in the chat: nobody opens or edits the file |
| 07 | Every component has to earn its place, and the duties are designed in, not added at the end |
| 08 | The plan has the real words users will read, and acceptance criteria someone can check, taken from the story |
| 09 | The assistant builds the real thing in the dev environment without asking each time, but the guardrails keep it there, block deletes and ask before a flow runs. The latest version comes into the repository before the check, so what's reviewed and pushed is what's in the dev environment |
| 10 | The check catches the deliberate mistake straight away, and refuses a suppression without a reason. Testing by people still matters |
| 11 | The review is the definition of done for a story. The check on GitHub doesn't care which assistant, if any, wrote the code |
| 12 | The harness improves itself, but people decide what changes |

## Common problems

| Problem | Fix |
|---|---|
| Someone arrives without a project | Help them choose in five minutes (see "The day before"). They answer the questions in the chat in exercise 05 |
| Teams won't let someone download the transcript | Only the organiser and co-organisers can. Ask the organiser to download it, or to make them a co-organiser |
| Transcription isn't available in a meeting | The council's Teams policy may turn it off. The attendee answers the questions in the chat from their notes instead |
| The cleaner says it couldn't find who said what | Usually a `.docx` in a layout it doesn't know. Download the transcript again as `.vtt` |
| The cleaner says the original is inside the repository | Move it to Downloads and run it again. The assistant can read anything in the repository's folder |
| The cleaner says the roles file isn't valid JSON | A missing comma or quote after editing. Fix it in VS Code, which shows the error, or delete the roles file to start again |
| The cleaner says a role includes part of a name | Change the role to the job only, such as "Team leader" |
| The cleaner won't replace a cleaned file | The attendee edited it by hand. That's deliberate: add `--force` only if they want to lose their edits |
| The attendee wants to see the requirements | The assistant shows a summary in the chat: ask it for any part, such as *"Show me the acceptance criteria for R1"*. The file is `docs/requirements.md` on the attendee's computer; GitHub shows it once the work is pushed. If Claude showed a plan instead of asking questions, the attendee was in plan mode: press Shift+Tab until it says **accept edits on**, and run `/lbbexley:requirements` again |
| The attendee lost the questions table | It's in `docs/discovery/requirements-questions.md`. Or ask the assistant again: *"Give me the requirements questions as a table."* The open questions are in the draft requirements, so it gives the same ones |
| The pasted answers aren't recognised | The first line is missing, or only part of the table was pasted. Paste it again, from the line starting "Bexley requirements answers" to the last row, or say *"Here are the answers to the requirements questions"* before pasting |
| The requirements skill stops for personal data | It's doing its job. The attendee says it again without the person, or, for a transcript, fixes the place it describes and runs it again |
| Claude Code didn't offer to install the plugin | Exit Claude Code and, in the same terminal, run `claude plugin marketplace add dbraben/lbbexley-digital-standards#v0.6.1 --scope local` and `claude plugin install lbbexley@lbbexley-digital --scope local`, with the release in the repository's `quality.yml`. Then start Claude Code again |
| There's no **Use this template** button | The attendee isn't signed in to GitHub. Or give them the link in exercise 02, which opens the same page |
| Someone typed a terminal command, such as the transcript cleaner, into Claude Code | Claude Code runs in VS Code's terminal, so commands go in a second one (**Terminal**, then **New Terminal**). Claude isn't allowed to run the cleaner, so nothing ran: run it again in a second terminal. The command, including the file's name, went to Claude as a message: if the name includes a person's name, tell the facilitator |
| `claude` isn't found in VS Code's terminal | Only the VS Code extension is installed, and it doesn't add `claude` to the terminal. Install the command-line version (exercise 00), then open a new terminal |
| `/model` doesn't show `opusplan` | Claude Code calls it **Opus Plan Mode**. It's the last option, and it's only listed while it's the model in use. If it isn't there, type `/model opusplan` |
| Claude Code shows a **Stop hook error** at the end of a run | It's the end-of-run check: first asking for its review, then, once everything passes, asking Claude to commit the work ("Bexley end-of-run check passed. Now save the work"). Both are the check working. Claude carries on by itself |
| Claude says the commit failed because Git doesn't know who they are | Set the attendee's name and email (exercise 00), then ask Claude to commit again |
| The push to GitHub fails | Usually the attendee isn't signed in to GitHub in Git, or `main` is protected on GitHub. Sign in (the GitHub CLI's `gh auth login` sets Git up too), then ask the assistant to push again. A protected `main` means the team wants pull requests: work on a branch |
| The end-of-run check keeps saying "Before finishing, bring the latest version from the dev environment into the repository" | `pac solution sync` isn't working: usually `pac` isn't signed in, or there's no `src/solution` yet. Do steps 2 and 3 of "Set up your dev environment once" in exercise 09. After three tries, the check stops and tells the attendee instead |
| The guardrails say `pac` is connected to another environment | The attendee's `pac` profile points somewhere else. `pac env select --environment <the dev address in AGENTS.md>`, or `pac auth create` for it, then try again. That's the guard doing its job |
| A flow or table the attendee built isn't in `src/solution` after the sync | Microsoft's tools create them outside the solution. Ask the assistant to add it (`pac solution add-solution-component`) and sync again. Check the attendee set the preferred solution in step 1 of the set-up |
| The end-of-run check says the work hasn't been committed or pushed | The assistant stopped before it could, usually because Git doesn't know the attendee's name (`git config --global user.name`) or they aren't signed in to GitHub. Fix that, then ask it to commit and push |
| `/configure-canvas-mcp` fails, or `dnx` isn't found | The .NET 10 SDK is missing (`dotnet --list-sdks`), coauthoring isn't on, or the address was the player's, not Studio's editing page. Keep the Studio tab open: closing it ends the connection |
| The Power Automate tools can't sign in | Run `az login` with the same account as `pac`. If the council's sign-in policies block it, build the flow in the designer and ask the assistant to sync it in |
| VS Code asks before every tool and command (Copilot) | Choose to always allow the canvas, Power Automate and Dataverse tools, `pac solution sync`, `pac solution add-solution-component`, `git commit` and `git push` in the workspace. Never allow deletes |
| Claude doesn't commit the work at the end of a run | The check only asks for the commit once everything passes. It stops without one when a reviewer's problem was explained rather than fixed (the attendee decides, then says *"That's fine: commit the work"*), when a standards problem is still there after three attempts, after five reviews in one request, and in plan mode. If none of those, the plugin is older than 0.4.0: update it as in the row after next |
| The end-of-run check asks for the same review again and again, then says the review didn't run | The attendee's Claude Code plugin is older than 0.3.1: update it as in the next row |
| The plugin isn't on the repository's release | `claude plugin list`, in a second terminal in the service repository, shows the plugin's version: it should match the release in `.github/workflows/quality.yml`. If not, run `claude plugin marketplace add dbraben/lbbexley-digital-standards#v0.6.1 --scope local` (with that release), then `claude plugin update lbbexley@lbbexley-digital`, and start Claude Code again |
| Claude Code doesn't start in plan mode | The attendee is using the Claude Code panel, which never takes its starting mode from the project. Run `claude` in VS Code's terminal instead, or set `claudeCode.initialPermissionMode` to `plan` in VS Code user settings |
| Copilot doesn't list the lbbexley agents | Check the workspace is trusted, Agent mode is on, and VS Code is up to date |
| The Copilot hooks don't run | They're a preview feature: check `chat.useHooks` is on and VS Code is up to date. Meanwhile, run `npm run check` and hand over to lbbexley-check by hand |
| Copilot's **Commit the work** button | It's under every reply from lbbexley-check, whatever the check found, so attendees read the result before they select it. If it isn't there at all, the repository's agents are older than 0.4.0: ask lbbexley-build to update the Bexley standards to v0.6.1 |
| A model on an agent's list isn't available | Copilot uses the next one on the list. Tell attendees which model they're getting |
| The check on GitHub fails with "Bexley files out of date" | Someone edited a synced file. Ask the assistant to undo the change to that file, or to update the Bexley standards to the version in `.github/workflows/quality.yml` |
| The check on GitHub can't find the standards | The standards repository is private and the service repository has no `standards-token` secret |
| An accessibility test says it needs a saved sign-in, or that it opened a sign-in page | Nothing was tested, so it fails. Run `npm run test:a11y:login` again, signing in with the test account: sign-ins expire |
| `npm run test:a11y:login` says a path needs A11Y_BASE_URL | The target's `url` in `targets.json` is a path. Give the page's full address instead (exercise 10), or set `A11Y_BASE_URL` in that terminal first, as the message shows |
| Dataverse MCP tools don't appear | Check `DATAVERSE_DEV_URL` (Claude Code on Windows), the address in `claude mcp add` (Claude Code on a Mac or Linux: `claude mcp get dataverse` shows it) or the address given to VS Code (Copilot), and that the environment has the Dataverse MCP server turned on |

## Turning on the accessibility tests in the Quality workflow

Optional, for a service that has something to test:

1. In the service repository, add a variable **A11Y_BASE_URL** (Settings, Secrets and variables, Actions, Variables): the Power Pages site's address, or the dev environment's address for a service with no Power Pages site. Add it once `tests/accessibility/targets.json` lists a page or screen: with the variable set, an empty list fails.
2. For screens behind a sign-in, add a secret **A11Y_STORAGE_STATE**: the base64 of `.auth/a11y-state.json` from the test account. Sign-ins expire, so refresh it when the tests say so. Without it, every target with `auth: true` fails, because a test that didn't run hasn't passed.
3. The council's sign-in policies may block sign-ins from GitHub's servers. If they do, add a variable **A11Y_SKIP_SIGNED_IN** set to `1`: the check on GitHub then skips the targets with `auth: true`, and developers run those tests on their own computers. The run's summary says how many targets were run, so a skipped one is never mistaken for a pass.

## After the session

- Remind attendees to paste the service team's answers back into the chat when they arrive, and, if they used a transcript, to delete the original and its roles file from Downloads once their service owner has agreed the requirements.
- Read the feedback issues in this repository, and turn anything that didn't work into a change (see CONTRIBUTING.md).
- Triage the harness-improvement issues attendees raised, in the standards repository.
- Clean up dev environments and test accounts that aren't needed. Attendees' service repositories are theirs to keep.
