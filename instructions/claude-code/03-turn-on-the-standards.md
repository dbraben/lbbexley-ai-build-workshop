# 03 Turn on the standards (Claude Code)

*About 10 minutes · No dev environment needed*

Claude Code gets the Bexley standards from the **lbbexley** plugin, which it installs from the standards repository when you trust your service repository. In this exercise you turn it on and check the settings the template gives you.

## Steps

1. In VS Code, with your service repository open, open the terminal (**Terminal**, then **New Terminal**) and start Claude Code:

   ```bash
   claude
   ```

   > [!IMPORTANT]
   > Use Claude Code in the terminal for this workshop, not the Claude Code panel that opens from the Claude Code icon. The panel doesn't read the project's setting that starts sessions in plan mode, so it usually starts in **Auto** mode, where a classifier decides on most actions instead of asking you. If you have to use the panel, set `claudeCode.initialPermissionMode` to `plan` in your VS Code **user** settings, and check the mode and the model in each new conversation.

2. When Claude Code asks whether you trust this folder, say yes. It then offers to add the plugin marketplaces listed in `.claude/settings.json` (**lbbexley-digital** and **power-platform-skills**) and to turn on the **lbbexley** plugin. Accept both.

   > [!TIP]
   > No offer? Add them yourself:
   > ```text
   > /plugin marketplace add dbraben/lbbexley-digital-standards
   > /plugin install lbbexley@lbbexley-digital
   > ```

3. Check the plugin is on: run `/plugin`. **lbbexley** is listed as enabled.
4. Type `/lbbexley` and look at the commands it offers, including `requirements`, `architect`, `plan`, `review`, `improve` and `new-app`. You'll use each of them on your project.
5. Run `/agents`. The plugin adds three read-only reviewers: `lbbexley:accessibility-reviewer`, `lbbexley:compliance-reviewer` and `lbbexley:end-of-run-reviewer`.
6. **Check the model.** The project's `.claude/settings.json` sets `opusplan`: Opus while you plan, Sonnet once you approve the plan and build. Claude Code calls it **Opus Plan**, so you won't see the word `opusplan`:
   - When the session starts, Claude Code says it's **Using Opus Plan**, from `.claude/settings.json`.
   - Run `/model`. The last option, **Opus Plan Mode** ("Use Opus in plan mode, Sonnet otherwise"), has a tick. It's only listed while it's the model in use. Press Esc to close the list without changing anything.

   No **Opus Plan Mode** in the list? Type `/model opusplan` and press Enter. That also makes it your default in other projects. You can change it back with `/model` at any time.

7. **Check the mode.** The session starts in **plan mode**, where Claude can read and plan but not change files. Below the prompt it says **⏸ plan mode on**. Shift+Tab cycles the modes.
8. Ask Claude: *"Which rules apply in this repository, and where do they come from?"* It answers from `AGENTS.md`, the plugin's skills and the reminder the plugin adds when a session starts.
9. Try the personal-data guard. Type a message with a made-up email address at gmail.com in it, for example your first name. The guard stops the message before it reaches the model. Add `[fictional]` to the start and it goes through.

   > [!WARNING]
   > `[fictional]` is for made-up data only. Never use it to get real data past the guard.

## Check

- [ ] `/plugin` shows **lbbexley** enabled
- [ ] `/agents` lists the three lbbexley reviewers
- [ ] `/model` has **Opus Plan Mode** ticked, and the session is in plan mode
- [ ] The guard stopped the message with the email address

## What just happened

The plugin is now active in this repository, and only in Bexley repositories like it. It adds:

- the skills: brand, accessibility, content style, the legal duties, one per platform, and the commands you just saw
- guardrails that run automatically: a reminder at the start of each session, the personal-data guard, a Dataverse guard, the standards check after every save, and the end-of-run check before Claude finishes
- the Microsoft Learn MCP server, so Claude checks Microsoft's current documentation rather than relying on memory

The template's settings also let Claude commit your work without asking you, while it still asks before it pushes anything to GitHub. They stop Claude running the transcript cleaner or reading `.vtt` and roles files, and turn off Claude Code's attribution lines, so its commits don't carry them.

---

[← 02 Create your service repository](../02-create-your-service-repo.md) · [Next: 04 Set up your service →](04-set-up-your-service.md)
