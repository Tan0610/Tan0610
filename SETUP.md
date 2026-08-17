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
git add README.md SETUP.md .github/workflows/profile-3d.yml
git commit -m "feat: add profile README"
git branch -M main
git remote add origin https://github.com/Tan0610/Tan0610.git
git push -u origin main
```

If the repo is private, the profile README will not show. Make it public.

---

## 2. Keeping the README current

Every slot is filled with real details — no `[bracketed]` placeholder is left. This section is
about where to edit when something changes.

| Change | Where to edit |
| --- | --- |
| New role or fellowship | **💼 Experience** — add a `### <emoji> Role — Company (Month Year – Present)` block, newest first, with a one-line summary and the usual bullets. |
| New award or placement | **🏆 Achievements** — add a row: award, project, event. |
| New project | **📌 Featured Projects** — add a row: project name linked to its repo, stack in backticks, and what it does with the one distinguishing technical concept in bold. |
| New technology | **🛠️ Tech Stack** — add a badge to whichever of the four labelled groups fits (Languages, Frontend & Backend, Databases & Tools, AI & Web3). Badge URL shape and the simpleicons.org slug lookup are in section 4. |
| Changed contact details | **📫 Let's Connect** — the LinkedIn, Gmail and GitHub badge link targets. |

Whatever you add, keep the heading, bullet and divider conventions in section 5 intact.

---

## 3. 3D contribution calendar

The workflow is at `.github/workflows/profile-3d.yml`. It uses
`yoshi389111/github-profile-3d-contrib@v0.9.3` to render the contribution grid as an isometric
3D calendar, then commits the generated SVGs into a `profile-3d-contrib/` directory **on `main`**.
There is no separate output branch.

Steps:

1. Push the workflow file to `main`.
2. Go to the repo's **Actions** tab. On a fresh repo GitHub asks you to enable workflows —
   click **"I understand my workflows, go ahead and enable them"**.
3. Check **Settings → Actions → General → Workflow permissions** and make sure
   **"Read and write permissions"** is selected. The workflow needs `contents: write` to commit
   the SVGs back to `main`; without it the commit fails with a 403.
4. Select the **GitHub Profile 3D Contrib** workflow in the sidebar and click **Run workflow**
   (this is the `workflow_dispatch` trigger). Run it against `main`.
5. When it goes green, confirm `profile-3d-contrib/` exists on `main` and contains
   `profile-night-view.svg` and `profile-season-animate.svg` — the dark and light images the
   **🧊 Contribution Calendar** section points at via raw URLs on `main`.
6. Reload your profile. The `<picture>` block in that section will now resolve.

This has already run successfully, so the SVGs are on `main` today. On a fresh clone, until
step 5 completes the calendar images **404** — that is expected, not a broken README.

After that the workflow re-runs daily at 18:00 UTC on a cron (`0 18 * * *`), plus on every push
to `main`. Note that GitHub disables scheduled workflows on repos with no activity for 60 days;
a single commit re-enables them.

### Self-hosted stats widgets

The **📊 GitHub Stats** card and the **🏅 Trophy Case** do not use the public upstream instances —
they point at personal Vercel deployments, both already configured:

| Widget | Deployment | Required env vars |
| --- | --- | --- |
| github-readme-stats | `https://github-readme-stats-six-lake-40.vercel.app` | `PAT_1` |
| github-profile-trophy | `https://github-profile-trophy-eight-kohl.vercel.app` | `GITHUB_TOKEN1`, `GITHUB_TOKEN2` |

The runbook for both lives at `D:\github\vercel-widgets\DEPLOY.md`.

The stats card currently reports roughly **188 total commits** rather than the full history:
the configured PAT carries `public_repo` scope only. Granting it full `repo` scope would pull
private-repo commits into the count as well.

---

## 4. Tech stack badges

The badges under **🛠️ Tech Stack** are the real stack, split across four labelled groups —
Languages (TypeScript, Python, Java, C++), Frontend & Backend (React, Next.js, Node.js, Fastify,
Spring Boot), Databases & Tools (PostgreSQL, Supabase, Prisma, Docker, Git) and AI & Web3
(OpenAI, Solidity, Hardhat, IPFS, Ethereum). Add new ones to the group they belong to.

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
- Every top-level section is `## <emoji> <2-3 word title>` followed by content, then a gradient
  divider — not a `---` rule:
  `![divider](https://capsule-render.vercel.app/api?type=rect&color=gradient&customColorList=0,2,5,30&height=3&section=header)`
- Every bullet follows `- <emoji> **Bold lead-in** — plain explanation`.
- Generated widgets currently in play: the capsule-render banner, the readme-typing-svg header,
  the self-hosted stats / top-langs / streak / activity-graph / summary cards, the trophy case,
  the 3D contribution calendar, and the komarev profile-views counter at the bottom. No
  skill-icons tiles — the tech stack is shields.io `for-the-badge` badges in four labelled groups.
- Markdown tables use no alignment colons — GitHub's default (centered header, left body) is the look.

---

## Final check before publishing

- [ ] `grep -c "align=\"center\"" README.md` returns `0`
- [ ] No `[bracketed]` placeholder remains outside of markdown link syntax
- [ ] Repo is public and named exactly `Tan0610`
- [ ] `GitHub Profile 3D Contrib` has run once and `profile-3d-contrib/profile-night-view.svg`
      and `profile-3d-contrib/profile-season-animate.svg` exist on `main`
- [ ] LinkedIn and Gmail badges point at real destinations
