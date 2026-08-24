# assets

Media files referenced by `data.json` that are too large to sit inline as data URIs.

| File | Used by |
| --- | --- |
| `hackathon-demo.mp4` | The **Beat by Beat** card in Featured Work (`caseStudies[0].media[0].src`) |

Drop the file in here with exactly that name, then commit it:

```bash
cp "~/Desktop/spatialhack 2026/Hackathon_Demo.mp4" assets/hackathon-demo.mp4
git add assets/hackathon-demo.mp4
git commit -m "Add Spatial Hack AI 2026 demo video"
git push
```

Keep clips short — GitHub Pages serves them straight from the repo, and anything
over ~50 MB will be slow for visitors (GitHub warns above 50 MB and blocks at 100 MB).
