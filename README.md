# Russian Course — course site

Starter repo for a Russian course organized into 11 thematic modules (2 days
each, 22 days total), built with the same pipeline as
[nevmenandr/WLA](https://github.com/nevmenandr/WLA): write in Obsidian → build
with MkDocs → deploy to GitHub Pages via GitHub Actions.

## Modules

| # | Theme | Access |
|---|---|---|
| 0 | Geography and Environment | **Free** |
| 1 | Social Issues | Paid |
| 2 | Customs and Traditions | Paid |
| 3 | Education and Employment | Paid |
| 4 | Healthcare and Benefits | Paid |
| 5 | Crime and Security | Paid |
| 6 | History and Military | Paid |
| 7 | Science and Technology | Paid |
| 8 | Trade & Economy | Paid |
| 9 | Internal and Foreign Affairs | Paid |
| 10 | Literature and Culture | Paid |

## Day structure

Each **day** follows the same 7-part template:

1. Topic Preview & Warm-Up
2. Listening Comprehension — Passage 1 (vocab → comprehension check → audio/video/transcript → discussion)
3. Reading Comprehension — Passage 1 (vocab → comprehension check → reading → discussion)
4. Listening Comprehension — Passage 2 (same structure as #2)
5. Reading Comprehension — Passage 2 (same structure as #3)
6. Topical Discussion (synthesizing questions)
7. Vocabulary Review (info-gap + translation)

Two days make up a module.

## How this is organized

```
russian-course/
├── .github/workflows/deploy.yml   # auto-builds & deploys on every push to main
├── docs/                          # PUBLIC vault — this is what gets published
│   ├── index.md                   # landing page
│   ├── get-full-course.md         # sales page → Gumroad link
│   ├── Free Preview/
│   │   └── Module 0_ Geography and Environment/
│   │       ├── Day 1.md           # full free day, published on the public site
│   │       └── Day 2.md
│   └── assets/
│       ├── audio/                 # audio files for Module 0's passages
│       └── video/                 # optional local video files (see Video section below)
├── full-course-source/            # PRIVATE — Modules 1-10 live here, gitignored
│   ├── Module 1_ Social Issues/
│   │   ├── Day 1.md
│   │   └── Day 2.md
│   ├── Module 2_ Customs and Traditions/ ... Module 10_ Literature and Culture/
│   └── assets/audio/, assets/video/
├── mkdocs.yml                     # site config, theme, nav
└── requirements.txt               # mkdocs + plugins for the build
```

**The split matters:** anything in `docs/` gets built into the public website.
`full-course-source/` is listed in `.gitignore`, so it never reaches GitHub or
the public site — it's just where you keep working on Modules 1-10 in
Obsidian. When the full course is ready to sell, zip that folder (with its
audio) and upload it as the product file on Gumroad, or ask Claude to help
you fold it into a gated Cloudflare Pages setup later if you want a live paid
site instead of a download.

## One-time setup

1. Create a new **public** repo on GitHub named `russian-course` (or whatever
   you like).
2. Push this folder's contents to it (`docs/`, `mkdocs.yml`, `requirements.txt`,
   `.github/`, `.gitignore`, `README.md` — NOT `full-course-source/`, which
   .gitignore already excludes).
3. In the repo's **Settings → Pages**, set the source branch to `gh-pages`
   (GitHub Actions creates this branch automatically the first time the
   workflow runs).
4. Edit `mkdocs.yml` — replace `YOURUSERNAME` and the repo URL with your real
   GitHub username and repo name.
5. Push again. Check the **Actions** tab to watch the build; once it's green,
   your site is live at `https://YOURUSERNAME.github.io/russian-course/`.

## Day-to-day workflow

1. Open the `russian-course` folder as an Obsidian vault.
2. Open a day's note (e.g. `Free Preview/Module 0_ Geography and
   Environment/Day 1.md`, or a module folder inside `full-course-source/`)
   and fill in each of the 7 sections: warm-up, listening passages, reading
   passages, discussion, vocab review. Drop matching audio files into the
   module's `assets/audio/` folder.
3. Save, then in GitHub Desktop: write a commit summary, **Commit to main**,
   **Push origin**. Only changes inside `docs/` trigger a rebuild — edits in
   `full-course-source/` never get pushed at all.

## Video (optional, per listening passage)

Each listening passage has a **Video (optional)** block. Default approach:
upload the video as **unlisted on YouTube** (free, no file-size limit),
then paste its video ID into the `YOUR_VIDEO_ID` placeholder in the iframe
embed. Unlisted means only people with the direct link can see it.

If you'd rather keep video files locally instead of on YouTube, there's an
`assets/video/` folder ready in both `docs/` and `full-course-source/` — just
be aware GitHub blocks files over 100MB and warns above 50MB, so this only
works for short/compressed clips.

Delete the Video block entirely on passages where you don't have footage —
it's optional, not required for every passage.

## Selling the full course

Simplest path (Option A from your plan with Claude): once all 11 modules are
written, zip `full-course-source/` (plus its audio) and upload it as a
Gumroad product. Point the "Get the Full Course" button on the site
(`docs/get-full-course.md`) at your Gumroad product link.

If you later want buyers to get a live, always-updated *website* instead of a
download, that's Option B — deploying the full course site to Cloudflare
Pages with Cloudflare Access gating everything past Module 0. Ask Claude to
set that up when you're ready; it reuses this same `docs/` structure, just
with all 11 modules included and access rules layered on top.
