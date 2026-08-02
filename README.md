# 20 Units of Russian — course site

Starter repo for a 20-unit Russian course, built with the same pipeline as
[nevmenandr/WLA](https://github.com/nevmenandr/WLA): write in Obsidian → build with
MkDocs → deploy to GitHub Pages via GitHub Actions.

## How this is organized

```
russian-course/
├── .github/workflows/deploy.yml   # auto-builds & deploys on every push to main
├── docs/                          # PUBLIC vault — this is what gets published
│   ├── index.md                   # landing page
│   ├── get-full-course.md         # sales page → Gumroad link
│   ├── Free Preview/
│   │   ├── Unit 01.md             # full free units, published on the public site
│   │   └── Unit 02.md
│   └── assets/audio/              # audio files for the free preview units
├── full-course-source/            # PRIVATE — Units 3-20 live here, gitignored
│   ├── Unit 03.md ... Unit 20.md  # not published; not pushed to GitHub
│   └── assets/audio/
├── mkdocs.yml                     # site config, theme, nav
└── requirements.txt               # mkdocs + plugins for the build
```

**The split matters:** anything in `docs/` gets built into the public website.
`full-course-source/` is listed in `.gitignore`, so it never reaches GitHub or
the public site — it's just where you keep working on Units 3-20 in Obsidian.
When the full course is ready to sell, zip that folder (with its audio) and
upload it as the product file on Gumroad, or ask Claude to help you fold it
into a gated Cloudflare Pages setup later if you want a live paid site instead
of a download.

## One-time setup

1. Create a new **public** repo on GitHub named `russian-course` (or whatever
   you like).
2. Push this folder's contents to it (`docs/`, `mkdocs.yml`, `requirements.txt`,
   `.github/`, `.gitignore`, `README.md` — NOT `full-course-source/`, which
   .gitignore already excludes).
3. In the repo's **Settings → Pages**, set the source to the `gh-pages` branch
   (GitHub Actions will create this branch automatically the first time the
   workflow runs).
4. Edit `mkdocs.yml` — replace `YOURUSERNAME` and the repo URL with your real
   GitHub username and repo name.
5. Push again. Check the **Actions** tab to watch the build; once it's green,
   your site is live at `https://YOURUSERNAME.github.io/russian-course/`.

## Day-to-day workflow

1. Open the `russian-course` folder as an Obsidian vault (or open `docs/` and
   `full-course-source/` as two separate vaults, if you'd rather keep them
   fully apart).
2. Write/edit a unit's note: paste the text, drop the audio file into the
   matching `assets/audio/` folder, fill in the grammar section, write the
   conversation prompts.
3. Save, then `git add`, `git commit`, `git push` from the `docs/`-containing
   repo. The site rebuilds automatically within a minute or two.
4. Units in `full-course-source/` never need to be pushed — just keep them
   written and ready for when you package the full course.

## Video (optional, per unit)

Each unit's note now has a **Video** section (below Audio) for students who
want to relisten with visuals. Default approach: upload the video as
**unlisted on YouTube** (free, no file-size limit, doesn't bloat the repo),
then paste its video ID into the `YOUR_VIDEO_ID` placeholder in the iframe
embed. Unlisted means it won't show up in search or on your channel — only
people with the direct link (i.e. people on your course page) can see it.

If you'd rather keep video files locally instead of on YouTube, there's an
`assets/video/` folder ready in both `docs/` and `full-course-source/` — just
be aware GitHub blocks files over 100MB and warns above 50MB, so this only
works for short/compressed clips. For anything longer, YouTube-unlisted is
the easier path.

Leave the Video section out entirely on units where you don't have footage —
it's optional, not required for every unit.

## Selling the full course

Simplest path (Option A from your plan with Claude): once all 20 units are
written, zip `full-course-source/` (plus its audio) and upload it as a
Gumroad product. Point the "Get the Full Course" button on the site
(`docs/get-full-course.md`) at your Gumroad product link.

If you later want buyers to get a live, always-updated *website* instead of a
download, that's Option B — deploying the full 20-unit site to Cloudflare
Pages with Cloudflare Access gating everything past Unit 2. Ask Claude to set
that up when you're ready; it reuses this same `docs/` structure, just with
all 20 units included and access rules layered on top.
