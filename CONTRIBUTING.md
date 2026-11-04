# Changing this workshop

The Digital Team owns this workshop. Change it whenever something didn't work in a session, the harness has a new release, or a tool changes how it works.

## How changes are made

1. Open a branch, make the change, and open a pull request.
2. Try every step you changed, on both tracks, with the harness release this workshop names in its README, on a project of your own.
3. Ask someone who wasn't involved to follow the changed exercise from the instructions alone.

## Keep the two tracks in step

Exercises 00, 01, 02, 05 and 13, and the optional page on using a Teams transcript, are shared. Exercises 03, 04 and 06 to 12 exist twice, in `instructions/claude-code/` and `instructions/github-copilot/`, with the same numbers, names, steps and checks wherever the tools allow.

- A change to what attendees produce or check goes into **both** tracks.
- A change to how a tool works goes into that tool's track only.
- Something both tracks do identically belongs in a shared exercise.
- Keep the file names, the exercise list in `instructions/README.md` and the table in the root `README.md` matching.

## No set scenario

Attendees work on their own projects. That's the point of the workshop, so keep it that way:

- **Never** ask attendees to build a given service, copy files from this repository, or run a script that fills their repository with someone else's issues or data.
- Write prompts with `<placeholders>` for what attendees fill in, and say what goes in each.
- Examples are short, labelled "for example", and vary from page to page, so no example becomes the thing everyone builds.
- Examples are invented, and never contain real people's names or details. Made-up names use the formats in the data-protection skill's `test-data.md`.
- If an exercise needs something to practise on, it uses the attendee's own work: see exercise 10, where they ask the assistant to break a rule in what they built.

## When the harness has a new release

1. Read the standards repository's CHANGELOG for that release.
2. Update the version this workshop names: in `README.md` ("These instructions match") and in exercise 02's table, which gives an example release.
3. Run through every exercise on both tracks, and fix anything that changed: command names, skill names, handover buttons, messages, the requirements questions and the answers table's first line (exercise 05), and what the transcript cleaner prints (the transcript page).
4. Update the facilitator guide's common problems.

## Writing style

The same as the harness: plain British English, short sentences, numbered steps that each do one thing, bullet points for lists of things to check, the exact words people will see in **bold**, and a "Check" list at the end of each exercise. No emoji. Use GitHub's callouts (`> [!NOTE]`, `> [!TIP]`, `> [!IMPORTANT]`, `> [!WARNING]`) sparingly.
