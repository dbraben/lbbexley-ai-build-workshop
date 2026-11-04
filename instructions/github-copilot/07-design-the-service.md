# 07 Design the service (GitHub Copilot)

*About 15 minutes · No dev environment needed*

The **lbbexley-architect** skill designs the service from your requirements: who uses it and how they reach it, which Power Platform components it needs and why, how data moves through it, which legal and accessibility duties apply and what the design does about each, and a diagram. Use it with the **lbbexley-plan** agent, which prefers the strongest model. Do this once per service, and again for a big change, not for every story.

## Steps

1. Start a new chat, choose the **lbbexley-plan** agent and ask:

   ```text
   Use the lbbexley-architect skill to design the service from docs/requirements.md.
   ```

2. Copilot asks about anything the requirements leave open that changes the design: devices, a non-digital route, special category data, decisions about people, payments, other systems. Answer what you can. For the rest, say: *"Assume the simplest option and list it as an open decision."*
3. **Read the design it describes**, and let it write `docs/architecture.md`. Check that:
   - each component has a reason. Push back if one hasn't earned its place: *"Why do we need Power Pages if only staff use it?"*
   - there's a non-digital route if residents use the service
   - the duties cover accessibility and every other duty that applies, with what the design does about each
   - the risks and open decisions are listed, with who decides

   If lbbexley-plan asks you to select **Check my work** now, you can leave it until step 5, which checks the design and the configuration together. Ignore **Build this plan** for now: it's for exercise 09.
4. **Reconcile the configuration.** A design can change more than the component list. Choose **lbbexley-build** (the plan agent only writes in `docs/`) and ask: *"Reconcile the configuration with docs/architecture.md, as the architect skill describes."* It brings the compliance documents, the accessibility test targets, the environment settings and "Built with" in `AGENTS.md` into line with the design, and says what it changed and what's still open.
5. **Commit it.** Select **Check my work**. When lbbexley-check finds nothing outstanding, select **Commit the work**: lbbexley-build commits the design and the configuration changes, and tells you they're committed.
6. **Optional: see the diagram.** Open `docs/architecture.md` in VS Code and press Ctrl+Shift+V (Cmd+Shift+V on a Mac) for the preview. A Mermaid preview extension draws the diagram; GitHub draws it too, once your work is pushed there.

## Check

- [ ] `docs/architecture.md` has users, components, how it works, duties, risks and a diagram
- [ ] Every component has a reason, and open questions are listed as decisions, not guessed
- [ ] lbbexley-build said the design is committed

## What just happened

- The duties come from the legal-duty skills: accessibility, data protection, equality, publicity and AI transparency. Each points to the compliance document in `docs/compliance/` it feeds.
- Every plan reads the requirements and this architecture, so you never explain the service again.

---

[← 06 Check the requirements](06-check-the-requirements.md) · [Next: 08 Plan the first story →](08-plan-the-first-story.md)
