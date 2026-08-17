# Setup Checklist

Everything needed to get this profile README live on `github.com/Tan0610`.

---

## 1. Create the special repo

- Create a **public** repo named exactly `Tan0610` under the user `Tan0610`.
  The repo name **must match the username character-for-character** — that is what makes GitHub
  treat it as the profile repo. A repo named `tan0610`, `Tan0610-profile`, or anything else will not work.
- Push `README.md` to the default branch (`main`).
- GitHub then renders `README.md` at the top of `https://github.com/Tan0610`.

```bash
git init
git add README.md SETUP.md .github/workflows/snake.yml
git commit -m "feat: add profile README"
git branch -M main
git remote add origin https://github.com/Tan0610/Tan0610.git
git push -u origin main
```

If the repo is private, the profile README will not show. Make it public.

---

## 2. Fill in every placeholder

The README ships with **zero real facts** — every slot is a `[bracketed]` placeholder.
Find them all:

```bash
grep -n "\[" README.md
```

(On Windows PowerShell: `Select-String -Path README.md -Pattern "\[" | Select-Object LineNumber, Line`)

Work top to bottom and replace each one. Nothing should still contain `[` when you publish,
except the markdown link syntax `[![LinkedIn](...)](...)` in the contact block — leave those
brackets, but do replace `[linkedin-handle]` and `[you@email.com]` inside the URLs.

Placeholders to fill:

| Section | Placeholders |
| --- | --- |
| Header | `[Your Name]`, `[Role]`, `[Focus area]`, `[Notable credential]` |
| About Me | `[Degree]`, `[College]`, `[Branch/Major]`, `[Month Year]`, `[Role]`, `[Company]`, `[Award]`, `[Event]`, `[project-name]`, `[metric]`, `[opportunity type]` |
| Experience | `[Role]`, `[Company]`, `[Month Year]`, `[Thing you built]`, `[metric]`, `[System or integration]`, `[Collaboration or ownership]` |
| Achievements | `[Award / Placement]`, `[project-name]`, `[Event]`, `[Month Year]` |
| Featured Projects | `[project-name]`, `[Stack]`, `[distinguishing technical concept]`, `[outcome]`, `[constraint]` |
| Let's Connect | `[linkedin-handle]`, `[you@email.com]` |

Also: delete the second Experience block if you only have one role, or duplicate it (instructions
are in the HTML comment above it) if you have more.

---

## 3. Snake animation

The workflow is at `.github/workflows/snake.yml`. It uses `Platane/snk@v3` to render the
contribution grid as a snake game, and `crazy-max/ghaction-github-pages@v4` to push the
generated `dist/` folder to a branch called `output`.

Steps:

1. Push the workflow file to `main`.
2. Go to the repo's **Actions** tab. On a fresh repo GitHub asks you to enable workflows —
   click **"I understand my workflows, go ahead and enable them"**.
3. Check **Settings → Actions → General → Workflow permissions** and make sure
   **"Read and write permissions"** is selected. Without it the push to `output` fails with a 403.
4. Select the **Generate Snake** workflow in the sidebar and click **Run workflow**
   (this is the `workflow_dispatch` trigger). Run it against `main`.
5. When it goes green, confirm a branch named `output` now exists and contains
   `github-snake.svg`, `github-snake-dark.svg`, and `github-snake.gif`.
6. Reload your profile. The `<picture>` block in the README will now resolve.

Until step 5 completes, the snake images **404** — that is expected, not a broken README.

After that the workflow re-runs every 12 hours on a cron, plus on every push to `main`.
Note that GitHub disables scheduled workflows on repos with no activity for 60 days;
a single commit re-enables them.

---

## 4. Swap the placeholder tech stack

The badges under **🛠️ Tech Stack** are a plausible generic stack (C++, Python, TypeScript, Java,
React, Next.js, Node.js, Tailwind, PostgreSQL, MySQL, Docker, Git, TensorFlow, PyTorch,
scikit-learn, OpenAI). **These are placeholders too.** Replace them with the real stack.

Badge URL shape — keep it identical for every badge:

```
https://img.shields.io/badge/<Label>-<HEX>?style=for-the-badge&logo=<simple-icons-slug>&logoColor=white
```

Rules:

- `style=for-the-badge` always. Every badge has a `logo=`.
- Find the `logo=` slug at **https://simpleicons.org** — search the tech, and use the icon's
  slug (e.g. `nodedotjs` for Node.js, `nextdotjs` for Next.js, `scikitlearn` for scikit-learn).
  simple-icons is also where the accurate brand hex comes from.
- A literal hyphen in the **label** must be doubled: `scikit-learn` → `scikit--learn`.
- A space in the label must be URL-encoded: `Tailwind CSS` → `Tailwind%20CSS`.
- An underscore renders as a space; use `_` for spaces if you prefer it to `%20`.

### Contrast note

GitHub's brand hex is near-black, which nearly disappears against GitHub's dark canvas (`#0D1117`).
The contact badge uses **`181717`** (simple-icons' official GitHub hex) rather than `100000` —
it is one shade lighter and stays readable in both themes with `logoColor=white`.
The Next.js badge has the same issue (`000000`); if it reads as a black hole on your profile,
bump it to `181717` as well.

---

## 5. Style rules to preserve when editing

The README follows a deliberate flat, left-aligned, text-first style. If you extend it:

- **Never** add `align="center"`, `<div align="center">`, or `<p align="center">`.
- Every top-level section is `## <emoji> <2-3 word title>` followed by content, then a `---` divider.
- Every bullet follows `- <emoji> **Bold lead-in** — plain explanation`.
- No typing-SVG banner, no capsule-render header, no github-readme-stats / streak / activity-graph /
  trophy cards, no skill-icons tiles, no visitor counter. The snake is the only generated widget.
- Markdown tables use no alignment colons — GitHub's default (centered header, left body) is the look.

---

## Final check before publishing

- [ ] `grep -c "align=\"center\"" README.md` returns `0`
- [ ] No `[bracketed]` placeholder remains outside of markdown link syntax
- [ ] Repo is public and named exactly `Tan0610`
- [ ] `Generate Snake` has run once and the `output` branch exists
- [ ] LinkedIn and Gmail badges point at real destinations
