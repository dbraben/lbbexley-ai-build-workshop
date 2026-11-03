# 07 Design the service (GitHub Copilot)

*About 15 minutes · No dev environment needed*

The **lbbexley-architect** skill designs the service from your requirements: who uses it and how they reach it, which Power Platform components it needs and why, how data moves through it, which legal and accessibility duties apply and what the design does about each, and a diagram. Use it with the **lbbexley-plan** agent, which prefers the strongest model. Do this once per service, and again for a big change, not for every story.

## Steps

1. Check you're on the branch you made in exercise 06 (`git branch` shows it), and start a new chat.
2. Choose the **lbbexley-plan** agent and ask:

   ```text
   Use the lbbexley-architect skill to design the service from docs/requirements.md.
   ```

3. Copilot asks about anything the requirements leave open that changes the design: devices, a non-digital route, special category data, decisions about people, payments, other systems. Answer what you can. For the rest, say: *"Assume the simplest option and list it as an open decision."*
4. Let it save `docs/architecture.md`.
5. Open `docs/architecture.md` and check:
   - each component has a reason. Push back if one hasn't earned its place: *"Why do we need Power Pages if only staff use it?"*
   - there's a non-digital route if residents use the service
   - the duties table covers accessibility and every other duty that applies, with what the design does about each
   - the risks and open decisions are listed, with who decides
   - the diagram is in a ```mermaid block. GitHub draws it; in VS Code, a Mermaid preview extension does
6. If the design changed what you're building, choose **lbbexley-build** (the plan agent only writes in `docs/`) and ask: *"Update 'Built with' in AGENTS.md to match the architecture."*
7. Commit it on your branch:

   ```bash
   git add docs/architecture.md AGENTS.md
   git commit -m "Design the service"
   ```

## Check

- [ ] `docs/architecture.md` exists, with users, components, how it works, duties, risks and a diagram
- [ ] Every component has a reason, and open questions are listed as decisions, not guessed

## What just happened

- The duties table comes from the legal-duty skills: accessibility, data protection, equality, publicity and AI transparency. Each points to the compliance document in `docs/compliance/` it feeds.
- Every plan reads the requirements and this architecture, so you never explain the service again.

---

[← 06 Write the requirements](06-write-the-requirements.md) · [Next: 08 Plan the first story →](08-plan-the-first-story.md)
