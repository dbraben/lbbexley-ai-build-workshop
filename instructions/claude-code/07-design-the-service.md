# 07 Design the service (Claude Code)

*About 15 minutes · No dev environment needed*

`/lbbexley:architect` designs the service from your requirements: who uses it and how they reach it, which Power Platform components it needs and why, how data moves through it, which legal and accessibility duties apply and what the design does about each, and a diagram. It runs on Opus. Do this once per service, and again for a big change, not for every story.

## Steps

1. Check you're in plan mode and on the branch you made in exercise 06 (`git branch` shows it). You can keep the conversation or use `/clear`: the architect skill reads `docs/requirements.md` from the repository.
2. Run:

   ```text
   /lbbexley:architect
   ```

   It starts from `docs/requirements.md`.

3. Claude asks about anything the requirements leave open that changes the design: devices, a non-digital route, special category data, decisions about people, payments, other systems. Answer what you can. For the rest, say: *"Assume the simplest option and list it as an open decision."*
4. Read the architecture it proposes, then approve the plan so it saves `docs/architecture.md`.
5. Open `docs/architecture.md` and check:
   - each component has a reason. Push back if one hasn't earned its place: *"Why do we need Power Pages if only staff use it?"*
   - there's a non-digital route if residents use the service
   - the duties table covers accessibility and every other duty that applies, with what the design does about each
   - the risks and open decisions are listed, with who decides
   - the diagram is in a ```mermaid block. GitHub draws it; in VS Code, a Mermaid preview extension does
6. **Reconcile the configuration.** A design can change more than the component list. Ask Claude: *"Reconcile the configuration with docs/architecture.md, as the architect skill describes."* It brings the Microsoft plugins, the compliance documents, the accessibility test targets, the environment settings and "Built with" in `AGENTS.md` into line with the design, and tells you what it changed and what's still open. If there's no dev environment yet, that's expected: it records that the environment is still to be set up.
7. Commit it on your branch:

   ```bash
   git add docs/architecture.md AGENTS.md
   git commit -m "Design the service"
   ```

## Check

- [ ] `docs/architecture.md` exists, with users, components, how it works, duties, risks and a diagram
- [ ] Every component has a reason, and open questions are listed as decisions, not guessed

## What just happened

- The architect skill is pinned to Opus, so it uses the strongest model even outside plan mode.
- The duties table comes from the legal-duty skills: accessibility, data protection, equality, publicity and AI transparency. Each points to the compliance document in `docs/compliance/` it feeds.
- Every plan reads the requirements and this architecture, so you never explain the service again.

---

[← 06 Write the requirements](06-write-the-requirements.md) · [Next: 08 Plan the first story →](08-plan-the-first-story.md)
