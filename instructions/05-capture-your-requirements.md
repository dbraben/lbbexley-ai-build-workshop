# 05 Capture your requirements

*About 20 minutes, or before the session · Both tracks · No dev environment needed*

Requirements come from the people who run and use the service, in their own words. Some of those words you've already given the assistant, in exercise 04. In this exercise you decide what to add, and put it into `docs/discovery/` in your repository, ready for the requirements skill in exercise 06. Choose one or more routes:

| Route | Use it when | You'll end up with |
|---|---|---|
| **C. Reuse what you've already told the assistant** | You described the service in exercise 04. This is the quickest route, and needs nothing more | Nothing extra: the set-up saved your answers to `docs/discovery/service-introduction.md`. Check it, and remove anything that shouldn't be there |
| **A. A Teams meeting transcript** | You've recorded, or can record, a conversation with the people who run the service. The best source | `docs/discovery/transcript-1.md`: the conversation with roles instead of names |
| **B. Your own requirement prompt** | You know the project well, or want to add what the meeting didn't cover | `docs/discovery/requirement-prompt.md`: your project in your own words |

> [!IMPORTANT]
> Git ignores everything in `docs/discovery/`, so it's never committed or pushed. But that doesn't make it private from AI: approved AI tools may still read and process its contents. So only cleaned material ever goes there. Never put an original transcript, a recording or a roles file in your repository.

## Route A: a Teams meeting transcript

### 1. Hold the conversation (skip if you've already recorded one)

- **Who:** two or three people who run the service day to day, and the service owner if you can. Thirty minutes is enough.
- **Before you start recording**, say why you want to record and transcribe it, who will see the transcript, and that you'll delete it once the requirements are agreed. Ask people to describe how the service works, not particular residents: "if you need an example, make one up".
- **Start transcription:** in the meeting, select **More actions**, then the option to transcribe: **Transcribe**, or **Record and transcribe** then **Start transcription**, depending on your version of Teams. Everyone sees a notice that the meeting is being transcribed.
- **Questions that work well:**
  - What does the service do, and who for?
  - Walk me through what happens now, from the moment someone gets in touch to when it's finished.
  - Where does it go wrong? What takes longest? What do people complain about?
  - How many requests a week, and when are the busy times?
  - What rules do you follow? Where are they written down?
  - What information do you collect about people, and what happens to it?
  - Which systems, forms or spreadsheets do you use?
  - If this worked perfectly a year from now, what would be different?
  - What must it never do?

### 2. Download the transcript

1. In Teams, open **Chat** and select the meeting's chat.
2. Select **Recap**, then **Transcript**.
3. Select the arrow next to **Download**, and choose the **.vtt** file type.
4. Save it in your **Downloads** folder. Not in your repository.

Only the meeting's organiser and co-organisers can download the transcript. If that isn't you, ask the organiser to download it, or to make you a co-organiser.

### 3. Clean it

Run the transcript cleaner yourself, in VS Code's terminal in your repository's folder. Never ask the assistant to run it: it reads the original. (Claude Code isn't allowed to run it.) Replace `<transcript file>` with the file's name, and keep the quotes, because Teams puts spaces in file names:

```bash
npm run transcript:clean -- "$HOME/Downloads/<transcript file>.vtt"
```

The same command works in PowerShell and in a Mac or Linux terminal. You'll see something like this:

```text
Cleaned: 3 speakers, 41 paragraphs.
Saved: docs/discovery/transcript-1.md (Git ignores docs/discovery/, but approved AI tools may still read it, so keep it clean)
Removed: 2 email addresses, 1 phone number.
3 speakers are still called "Speaker" and a number. To use roles instead, such as "Service manager", edit this file and run this again:
  /Users/<you>/Downloads/<transcript file>.roles.json
```

What it did:

- wrote a cleaned copy to `docs/discovery/transcript-1.md`, with each speaker called "Speaker 1", "Speaker 2" and so on, including where people said each other's names
- removed email addresses, phone numbers, full postcodes, and National Insurance, NHS, card and reference numbers
- dropped the timestamps, and joined each person's lines into paragraphs
- wrote a **roles file** next to the original, in Downloads. It's the only place the names are kept

It never prints a name. If it says it couldn't find who said what, download the transcript again as `.vtt` and clean that.

### 4. Name the speakers by role

Open the roles file from your Downloads folder in VS Code (**File**, then **Open File**). Change each `"Speaker"` value to the person's role, and save it:

```json
"speakers": {
  "<first speaker's name>": "Service manager",
  "<second speaker's name>": "Contact centre adviser",
  "<third speaker's name>": "Team leader"
}
```

Use a role only: the cleaner stops if a role includes part of the person's name. Then run the same command again. The cleaned copy now uses the roles. Do this before you edit the cleaned copy by hand: after that, the cleaner won't replace it unless you add `--force`.

### 5. Read it through, and fix what no tool can find

Open `docs/discovery/transcript-1.md` and read it from start to finish. Remove or replace:

- names of anyone who wasn't speaking: residents, colleagues, councillors, suppliers. Use a role ("a resident", "the finance team") or a made-up example
- addresses, and anything else that points to where someone lives
- details of anyone's case or situation: health, family, money, complaints, enforcement
- opinions about named colleagues, and anything said in confidence
- small talk and anything off-topic

Keep how the service works, the problems people described, volumes, deadlines, rules and decisions.

For example, the cleaner leaves this line from a speaker alone, because it can't recognise a resident's name or circumstances:

```text
**Contact centre adviser:** Last week Sam Example from Belvedere rang three times about her husband's
medication, because nobody had called her back.
```

You change it to keep the point and lose the person:

```text
**Contact centre adviser:** Residents often ring several times because nobody calls them back.
```

### 6. Look after the original

Leave the original transcript and the roles file in Downloads until the service owner has agreed the requirements, then delete both. Your team's records rules may say to keep them longer: if so, move them somewhere the council's policy allows, never into a repository.

## Route B: your own requirement prompt

1. Copy the template into your discovery folder. On a Mac or Linux:

   ```bash
   cp .github/skills/lbbexley-requirements/requirement-prompt.md docs/discovery/requirement-prompt.md
   ```

   In PowerShell:

   ```powershell
   Copy-Item .github/skills/lbbexley-requirements/requirement-prompt.md docs/discovery/requirement-prompt.md
   ```

2. Open `docs/discovery/requirement-prompt.md` and write under each heading, in your own words. The grey comments say what goes where. Leave a heading empty if you don't know: the requirements skill asks about it.
3. Tips:
   - Describe the need, not the solution: "officers need to see which requests are overdue", not "a red column in a table".
   - Give numbers if you have them: how many requests, how often, how long things take now.
   - Write down rules exactly, with where they come from: "We must reply within 10 working days (complaints policy)".
   - Say what's out of scope. It stops the design growing.
   - Name people by role only, and include nobody's details.
4. To see the level of detail that helps, open `.github/skills/lbbexley-requirements/requirement-prompt-example.md`. It's for an invented project: don't copy it, describe yours.

## Check

- [ ] `docs/discovery/` has what you chose: `service-introduction.md` (from exercise 04), a cleaned `transcript-1.md`, a `requirement-prompt.md`, or a mix
- [ ] Every speaker is named by role, and you've read the transcript through and removed anything that could identify someone
- [ ] `git status` doesn't list anything in `docs/discovery/`
- [ ] The original transcript and the roles file are in Downloads, not in your repository

## What just happened

- The cleaner removed what a tool can find reliably, and kept the names outside your repository, where the assistant won't look. Your read-through covered what only a person can spot.
- Nothing you put in `docs/discovery/` will be committed or pushed. What gets committed is the requirements document you write from it in the next exercise, which holds no personal data.

---

Previous: 04 Set up your service, for [Claude Code](claude-code/04-set-up-your-service.md) or [GitHub Copilot](github-copilot/04-set-up-your-service.md) · Next: 06 Write the requirements, for [Claude Code →](claude-code/06-write-the-requirements.md) or [GitHub Copilot →](github-copilot/06-write-the-requirements.md)
