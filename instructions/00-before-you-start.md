# 00 Before you start

*About 20 minutes, before the session · Both tracks*

Choose the project you'll work on, gather what you already know about it, and check your tools and accounts. In a guided session, the facilitator has done the Digital Team's part for you.

## 1. Choose your project

Bring something real that you or your team need. You'll capture its requirements, design it, and build and check its first small piece. You won't finish the whole project in the workshop, and that's fine: you'll leave with everything you need to carry on.

A good workshop project:

- is wanted by a team you can talk to, ideally the people who run the service now
- has a first piece small enough to build in under an hour, such as one screen, one table, one page, one agent topic or one flow
- suits the Power Platform: forms, case work, lists, approvals, notifications or answering questions
- can be built and tested with made-up data

Some kinds of project that work well, as illustrations:

- a staff tool that replaces a shared spreadsheet or a busy inbox
- an online form that replaces a paper, PDF or email process
- an agent that answers common questions from pages already on bexley.gov.uk
- a flow that sends reminders, or routes requests to the right team
- a model-driven app for case work that's currently tracked in Excel

Leave these for later, with the Digital Team: anything that takes payments, connects to on-premises systems, makes decisions about people (eligibility, priority, enforcement), or can't be built without real personal data.

> [!TIP]
> Not sure? Pick the most annoying manual process in your team. Talk to the facilitator before the session if you can't choose.

## 2. Gather what you know

You need at least one of these. Exercise 05 shows how to use each one.

| Source | Why it helps | What to do before the session |
|---|---|---|
| **A recorded Teams meeting** with the people who run the service | Their words, including the rules and problems nobody wrote down. The best source | Hold a 30-minute conversation and record it with transcription on. Exercise 05 has the questions to ask and how to record it |
| **Notes** from conversations, or a process you've written down | Quick, if you already have them | Make sure they name people by role, not by name |
| **Your own requirement prompt** | Fine on its own for a small project | Nothing: you'll write it in exercise 05 |

> [!IMPORTANT]
> If you record a meeting, don't download the transcript into your repository or share it with an assistant. Exercise 05 shows how to clean it first.

## 3. Install the tools

| Tool | Why | Check it with |
|---|---|---|
| Visual Studio Code | Where you work | Open it |
| Git | Version control | `git --version` |
| Node.js 22 or later | Runs the standards check, the transcript cleaner and the accessibility tests | `node --version` |
| GitHub CLI | Creates issues from your requirements (exercise 06). Optional: you can create them by hand | `gh --version` |

Then, for your track:

- **Claude Code track:** install the Claude Code extension for VS Code (or the command-line version), and sign in with your Claude Pro or Max account.
- **GitHub Copilot track:** install GitHub Copilot Chat in VS Code, sign in with your GitHub account, and check that the chat view offers **Agent** mode.

If you'll build in a dev environment in exercise 09, also install:

- the **Power Platform Tools** extension for VS Code, which includes the Power Platform CLI (`pac`)
- the **.NET 10 SDK** for a canvas app, which Microsoft's canvas app authoring tools need (`dotnet --list-sdks`)
- the **Copilot Studio** extension for VS Code for an agent

> [!TIP]
> When you open your service repository in VS Code in exercise 02, it recommends these extensions. Accept the recommendation to install them in one go.

## 4. Set your privacy settings

During the pilot you use an AI account you pay for yourself, so set these first:

- **Claude:** in Settings, then Privacy, turn off the setting that lets Anthropic use your chats and coding sessions to improve its models.
- **GitHub Copilot:** in your GitHub settings under Copilot, turn off any option that lets GitHub use your prompts, suggestions or code to improve its products.

## 5. Check your access

You need to be able to see these repositories on GitHub. Ask the facilitator if you can't.

- [lbbexley-app-template](https://github.com/dbraben/lbbexley-app-template): the starting point for every service
- [lbbexley-digital-standards](https://github.com/dbraben/lbbexley-digital-standards): the standards your service follows

To build in a dev environment in exercise 09, you also need:

- a Power Platform dev environment with Dataverse, with fictional data only, and its address (like `https://<your-org>-dev.crm11.dynamics.com`)
- the Bexley publisher (prefix `lbbexley`) imported into it
- for an agent, a Copilot Studio licence or trial in that environment

## Check

- [ ] You've chosen a project, and you can say in one sentence what it's for
- [ ] You have a recorded Teams meeting, notes, or enough in your head to write a requirement prompt
- [ ] `git --version` and `node --version` work, and Node.js is 22 or later
- [ ] Your assistant is installed and signed in, and your AI account's privacy settings are set
- [ ] You can open both repositories on GitHub

---

[← Exercises](README.md) · [Next: 01 How the harness works →](01-how-the-harness-works.md)
