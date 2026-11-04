# Build your own service with the Bexley AI build harness

You'll bring a real project, capture its requirements from a recorded Teams meeting or in your own words, and use an AI coding assistant to plan, build and check the first part of it, to the council's brand, accessibility and legal standards. Everything happens in your own service repository, made from the Bexley app template.

There's no set scenario. Every example in these instructions is an illustration of what an answer could look like: use your own project throughout.

Do the exercises in order. Exercises 00, 01, 02, 05 and 13 are the same for everyone. For the others, follow the track for your assistant.

## Choose your track

| Track | Use it if you have | Start at |
|---|---|---|
| **Claude Code** | A Claude Pro or Max subscription, and the Claude Code extension for VS Code or the command line | [00 Before you start](00-before-you-start.md), then [claude-code/](claude-code/) |
| **GitHub Copilot** | A GitHub Copilot plan with agent mode in VS Code | [00 Before you start](00-before-you-start.md), then [github-copilot/](github-copilot/) |

Both tracks use the same standards and produce the same documents. The commands differ, and so does how the plan, build and check steps hand over to each other.

## Exercises

| # | Exercise | Dev environment? | About |
|---|---|---|---|
| 00 | [Before you start](00-before-you-start.md): choose your project and check your tools | No | 20 min, before the session |
| 01 | [How the harness works](01-how-the-harness-works.md) | No | 15 min |
| 02 | [Create your service repository](02-create-your-service-repo.md) | No | 10 min |
| 03 | Turn on the standards: [Claude Code](claude-code/03-turn-on-the-standards.md) · [Copilot](github-copilot/03-turn-on-the-standards.md) | No | 10 min |
| 04 | Set up your service: [Claude Code](claude-code/04-set-up-your-service.md) · [Copilot](github-copilot/04-set-up-your-service.md) | No | 15 min |
| 05 | [Capture your requirements](05-capture-your-requirements.md): a cleaned Teams transcript, your own requirement prompt, or both | No | 20 min, or before the session |
| 06 | Write the requirements: [Claude Code](claude-code/06-write-the-requirements.md) · [Copilot](github-copilot/06-write-the-requirements.md) | No | 20 min |
| 07 | Design the service: [Claude Code](claude-code/07-design-the-service.md) · [Copilot](github-copilot/07-design-the-service.md) | No | 15 min |
| 08 | Plan the first story: [Claude Code](claude-code/08-plan-the-first-story.md) · [Copilot](github-copilot/08-plan-the-first-story.md) | No | 10 min |
| 09 | Build it: [Claude Code](claude-code/09-build-it.md) · [Copilot](github-copilot/09-build-it.md) | Depends on what you build | 30 min |
| 10 | Check and test: [Claude Code](claude-code/10-check-and-test.md) · [Copilot](github-copilot/10-check-and-test.md) | For the automated tests | 15 min |
| 11 | Review and open a pull request: [Claude Code](claude-code/11-review-and-pull-request.md) · [Copilot](github-copilot/11-review-and-pull-request.md) | No | 10 min |
| 12 | Improve the harness: [Claude Code](claude-code/12-improve-the-harness.md) · [Copilot](github-copilot/12-improve-the-harness.md) | No | 10 min |
| 13 | [Wrap-up and next steps](13-wrap-up.md) | No | 5 min |

**No dev environment yet?** You can do everything except some of the build routes in exercise 09 on files alone. Exercise 09 has a files-only route for a canvas app screen.

## How to read these instructions

- `Text in angle brackets`, like `<your-account>`, is for you to replace with your own.
- "For example" shows what an answer could look like for an invented project. It's never something you have to build.
- Prompts in grey boxes are a starting point. Change the wording to fit your project.
- Each exercise ends with a **Check** list. Don't move on until everything on it is ticked.

## Returning to an existing project?

Don't rerun the introductory questions in exercise 04. Ask the assistant where the project is: it reads the saved state (`AGENTS.md`, `docs/discovery/`, `docs/requirements.md`, `docs/architecture.md`) and resumes at the next exercise that isn't finished. For example: *"Where am I in the workshop for this project? Resume at the next incomplete stage."*

## The rules for the whole workshop

- **Your project, fictional data.** Build your real project, but test it only with made-up data. Never type, paste or upload real resident or staff information.
- **Transcripts are cleaned first.** An original meeting transcript never goes into your repository or near an assistant. Exercise 05 shows how to clean one.
- **Dev environments only.** Never point the assistant at a test or production environment.
- **Zero findings is done.** A piece of work isn't finished while any check reports anything, however minor.

Start with [00 Before you start →](00-before-you-start.md)
