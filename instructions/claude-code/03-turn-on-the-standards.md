# 03 Turn on the standards (Claude Code)

*About 10 minutes · No dev environment needed*

Claude Code gets the Bexley standards from the **lbbexley** plugin, which it installs from the standards repository when you trust your service repository. In this exercise you turn it on and check the settings the template gives you.

## Steps

1. In VS Code, with your service repository open, start Claude Code: select the Claude Code icon, or run `claude` in the terminal.
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
6. Run `/model`. The project sets **opusplan**: Opus while you plan, Sonnet once you approve the plan and build.
7. Look at the mode: the session starts in **plan mode**, where Claude can read and plan but not change files. Shift+Tab cycles the modes (in the VS Code extension, use the mode selector).

   > [!NOTE]
   > If the VS Code extension doesn't start in plan mode, set `claudeCode.initialPermissionMode` to `plan` in your VS Code **user** settings.

8. Ask Claude: *"Which rules apply in this repository, and where do they come from?"* It answers from `AGENTS.md`, the plugin's skills and the reminder the plugin adds when a session starts.
9. Try the personal-data guard. Type a message with a made-up email address at gmail.com in it, for example your first name. The guard stops the message before it reaches the model. Add `[fictional]` to the start and it goes through.

   > [!WARNING]
   > `[fictional]` is for made-up data only. Never use it to get real data past the guard.

## Check

- [ ] `/plugin` shows **lbbexley** enabled
- [ ] `/agents` lists the three lbbexley reviewers
- [ ] `/model` shows **opusplan**, and the session is in plan mode
- [ ] The guard stopped the message with the email address

## What just happened

The plugin is now active in this repository, and only in Bexley repositories like it. It adds:

- the skills: brand, accessibility, content style, the legal duties, one per platform, and the commands you just saw
- guardrails that run automatically: a reminder at the start of each session, the personal-data guard, a Dataverse guard, the standards check after every save, and the end-of-run check before Claude finishes
- the Microsoft Learn MCP server, so Claude checks Microsoft's current documentation rather than relying on memory

The template's settings also stop Claude running the transcript cleaner or reading `.vtt` and roles files, and turn off Claude Code's attribution lines, so commits and pull requests don't carry them.

---

[← 02 Create your service repository](../02-create-your-service-repo.md) · [Next: 04 Set up your service →](04-set-up-your-service.md)
