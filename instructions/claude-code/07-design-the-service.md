# 07 Design the service (Claude Code)

*About 15 minutes · No dev environment needed*

`/lbbexley:architect` designs the service from your requirements: who uses it and how they reach it, which Power Platform components it needs and why, how data moves through it, which legal and accessibility duties apply and what the design does about each, and a diagram. It runs on Opus. Do this once per service, and again for a big change, not for every story.

## Steps

1. **Go back to plan mode.** Press Shift+Tab until the line below the prompt says **⏸ plan mode on**: the design changes several files, so you see the plan first.
2. Run:

   ```text
   /lbbexley:architect
   ```

   It starts from `docs/requirements.md`.

3. Claude asks about anything the requirements leave open that changes the design: devices, a non-digital route, special category data, decisions about people, payments, other systems. Answer what you can. For the rest, say: *"Assume the simplest option and list it as an open decision."*
4. **Read the plan: it's the draft design.** Claude hasn't written the design yet. Check that:
   - each component has a reason. Push back if one hasn't earned its place: *"Why do we need Power Pages if only staff use it?"*
   - there's a non-digital route if residents use the service
   - the duties cover accessibility and every other duty that applies, with what the design does about each
   - the risks and open decisions are listed, with who decides

   Ask for changes before you approve it.
5. **Approve it** with **Yes, manually approve edits**, then approve each edit as it comes. Claude writes `docs/architecture.md`, then brings the configuration into line with the design: the Microsoft plugins, the compliance documents, the accessibility test targets, the environment settings and "Built with" in `AGENTS.md`. It tells you what it changed and what's still open. If there's no dev environment yet, that's expected: it records that the environment is still to be set up.
6. **Let the end-of-run check finish.** It reviews the design and the configuration changes, then asks Claude to commit them. Claude commits them and tells you.
7. **Optional: see the diagram.** Open `docs/architecture.md` in VS Code and press Ctrl+Shift+V (Cmd+Shift+V on a Mac) for the preview. A Mermaid preview extension draws the diagram; GitHub draws it too, once your work is pushed there.

## Check

- [ ] `docs/architecture.md` has users, components, how it works, duties, risks and a diagram
- [ ] Every component has a reason, and open questions are listed as decisions, not guessed
- [ ] Claude said the design is committed

## What just happened

- The architect skill is pinned to Opus, so it uses the strongest model even outside plan mode.
- The duties come from the legal-duty skills: accessibility, data protection, equality, publicity and AI transparency. Each points to the compliance document in `docs/compliance/` it feeds.
- Every plan reads the requirements and this architecture, so you never explain the service again.

---

[← 06 Check the requirements](06-check-the-requirements.md) · [Next: 08 Plan the first story →](08-plan-the-first-story.md)
