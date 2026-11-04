# 02 Create your service repository

*About 10 minutes · Both tracks · No dev environment needed*

Every Bexley service has its own repository, made from the app template. You make yours for your project, in your own GitHub account, and find where it refers to the standards.

## Steps

1. **Choose a name.** Use `lbbexley-` followed by a short, plain-English name for your service, in lower case with hyphens. For example `lbbexley-room-bookings` or `lbbexley-tree-works-requests`. Name it after what the service does for people, not the technology.
2. **Create it.** Sign in to GitHub, then open [lbbexley-app-template](https://github.com/dbraben/lbbexley-app-template). Select the green **Use this template** button at the top right, beside **Star**, then **Create a new repository**. The button only shows when you're signed in. If you can't find it, [this link](https://github.com/dbraben/lbbexley-app-template/generate) opens the same page.
   - Owner: your own account (or your team's, if you have one)
   - Repository name: the name you chose
   - Visibility: **Private**. Check it, because the page may start on Public

   Select **Create repository**.

3. **Clone it, go into its folder, and open it in VS Code**, replacing the parts in angle brackets:

   ```bash
   git clone https://github.com/<your-account>/<your-repository>.git
   cd <your-repository>
   code .
   ```

   Run every later command in this folder. VS Code's terminal starts there.

4. When VS Code asks whether you trust the authors of the files in this folder, choose **Yes, I trust the authors**. Install the recommended extensions if you haven't already.
5. **Run the standards check** on the whole repository, in VS Code's terminal. It needs no installation:

   ```bash
   npm run check:all
   ```

   It reports `No problems found`.

6. **Find the four places your repository refers to the standards:**

   | # | Where | What it does |
   |---|---|---|
   | 1 | `.claude/settings.json`: `extraKnownMarketplaces` and `enabledPlugins` | Claude Code installs the Bexley plugin from the standards repository |
   | 2 | `.github/workflows/quality.yml`: the `uses:` line and `standards-ref` | Every pull request is checked by the standards repository's workflow, pinned to a release such as `v0.3.0` |
   | 3 | `.github/skills/lbbexley-*`, `.github/agents/lbbexley-*`, `.github/instructions/lbbexley-*`, `.claude/rules/lbbexley-*`, `.github/hooks/lbbexley.json` and `.lbbexley/standards/` | Copies of the standards at the same release, for GitHub Copilot, for `npm run check`, for the transcript cleaner and for the accessibility tests. Never edit these by hand |
   | 4 | `package.json`: the `standards:update` script | Fetches a new release of the standards and moves the pin in `quality.yml` |

7. **Open `docs/discovery/README.md`.** It's where your requirements start, in exercise 05.

## Check

- [ ] Your repository exists on GitHub, under your account, and is private
- [ ] `npm run check:all` finds no problems
- [ ] You can point to all four references to the standards

## What just happened

- Your repository started as an exact copy of the template, including the synced Bexley files at the template's release.
- It follows that release of the standards until you choose to update it, in a pull request of its own. A new rule never changes your checks without warning.

---

[← 01 How the harness works](01-how-the-harness-works.md) · Next: 03 Turn on the standards, for [Claude Code →](claude-code/03-turn-on-the-standards.md) or [GitHub Copilot →](github-copilot/03-turn-on-the-standards.md)
