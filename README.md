# Reyes Tham — Portfolio

Hey, I'm Reyes. This is my personal portfolio site, and this repo is the whole thing — I built it as plain HTML, CSS and vanilla JavaScript with no frameworks and no build step, so it runs for free on GitHub Pages and I can edit everything with nothing but a browser and a text editor.

**Live site:** https://reyes-tham.github.io/portfolio/

---

## Why I built it this way

I wanted a portfolio that leads with *what I build* — AI agents, automation and full-stack tools — instead of just a big page with my name on it. I also wanted to be able to update it in two minutes without touching code, so I wrote myself a small CMS (`admin.html`) that edits everything and exports a single JSON file.

## What's in here

```
portfolio/
├── index.html     # The site itself — reads everything from data.json
├── admin.html     # My private CMS — edit content, export a new data.json
├── data.json      # Every word, image and link on the site lives here
├── assets/        # Large media (e.g. the hackathon demo video) referenced by data.json
└── README.md      # You're reading it
```

There's no server and no database. `index.html` fetches `data.json` at load time (with the same data embedded inline as a fallback, so the site still works if I open it straight from a folder).

## Site features

- **Featured work cards** — my selected projects, each with a summary, an outcome line, a tech stack, and a media strip that can hold **image cards and video cards** for mockups (YouTube/Vimeo embeds, `.mp4` links or repo-relative paths like `assets/hackathon-demo.mp4`, or uploaded files).
- **Project archive** — the rest of my projects in a compact list under the featured work.
- **Capability groups** — grouped skills (AI/ML, automation, full-stack, data) instead of a marquee of logos.
- **Custom cursor** — it expands and shows **"VIEW"** over clickable case studies, inverts over imagery, gently grows over links, and disappears over text so the native caret takes over. On touch devices it gets out of the way entirely.
- **CCAs & achievements** — photo/video carousels for my clubs, plus an expandable awards list.
- **Contact section** — email, [LinkedIn](https://www.linkedin.com/in/reyes-tham) and GitHub, all pulled from `data.json`.

## How I update the site

1. Open `admin.html` in a browser and enter my password. On the live site it always fetches the latest `data.json` automatically; if I'm working offline (or want to continue from a file I just exported), I hit **Import data.json** and pick the file so I'm editing current data, never a stale snapshot.
2. Edit whatever I need. New entries are **first in, last out** — anything I add goes straight to the top, so the most recent stuff always leads.
3. For featured work I can upload multiple images/videos at once or paste a video URL; for CCAs there's no upload limit — I just multi-select files.
4. Hit **Save & Export JSON** — it downloads a fresh `data.json`.
5. Replace `data.json` in this repo, commit, push. GitHub Pages picks it up automatically.

```bash
git add data.json
git commit -m "Update portfolio content"
git push
```

## Notes to self

- The admin stores only a SHA-256 **hash** of my password (in `admin.html`), never the password itself, so it can't be read from the source. To change it: open the admin page, run `await newPassHash('myNewPassword')` in the DevTools console, and paste the printed hash over `PASS_HASH`. It's still a soft lock — this is a client-side static site — but nothing sensitive lives behind it anyway.
- Uploaded files are stored as data URIs inside `data.json`, so I keep videos short and images compressed to stop the file from ballooning. Anything genuinely large goes in `assets/` instead and gets referenced by path, or gets hosted off-repo and referenced by URL — see `assets/README.md` for the options and the ffmpeg recipe.
- Case-study videos loop and autoplay muted by default, pause while off screen, and drop the autoplay for visitors who prefer reduced motion. `"loop": false` on a media item gives a plain player instead.
- The inline fallback data in `index.html` and `admin.html` should be refreshed occasionally so offline viewing stays in sync with `data.json`.
