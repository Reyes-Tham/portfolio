# assets

Media referenced by `data.json` that is too large to sit inline as a data URI.

| File | Used by |
| --- | --- |
| `hackathon-demo.mp4` | The **Beat by Beat** card in Featured Work (`caseStudies[0].media[0].src`) |

## Where the demo video should live

GitHub blocks any file over 100 MB and warns above 50 MB, so the raw screen
recording usually cannot go in the repo untouched. In rough order of preference:

### 1. Compress it and keep it here

Almost always the right answer — a demo recording is mostly static UI and
compresses hard. Nothing external to depend on, and the card plays inline.

```bash
ffmpeg -i "Hackathon_Demo.mp4" \
  -vf "scale='min(1600,iw)':-2" \
  -c:v libx264 -crf 28 -preset slow -profile:v high \
  -c:a aac -b:a 96k -movflags +faststart \
  assets/hackathon-demo.mp4
```

`-crf` is the quality dial: raise it to 30–32 to shrink further, drop it to 24
for a crisper picture. `+faststart` matters — it moves the index to the front of
the file so the video starts playing before it has fully downloaded. Trim to the
good part first with `-ss 00:00:05 -t 00:00:40` if the clip is long.

Aim for under ~25 MB. Then just commit it:

```bash
git add assets/hackathon-demo.mp4 && git commit -m "Add demo video" && git push
```

### 2. Attach it to a GitHub release

Release assets take files up to 2 GB, do not bloat the repo or count against
Pages bandwidth, and give a permanent direct URL. Create a release in the repo,
drag the file in, copy the asset link, and put it in `src`:

```
"src": "https://github.com/Reyes-Tham/portfolio/releases/download/v1/hackathon-demo.mp4"
```

### 3. YouTube (unlisted)

Free and unmetered, and it does the transcoding. The card renders it as an
embed and adds the loop parameters automatically. Paste the ordinary watch URL:

```
"src": "https://www.youtube.com/watch?v=VIDEOID"
```

Note that YouTube only loops a single video when it is also passed as a
one-item playlist — `index.html` handles that, so a plain watch URL is enough.

### 4. Object storage (Cloudflare R2, Bunny, Cloudinary)

A direct `.mp4` URL with no third-party player or branding. Worth it only if
the above do not fit; it means another account to keep alive.

## Looping

Video media items loop and autoplay (muted) by default. The site pauses them
while they are off screen, leaves them alone once a visitor touches the
controls, and skips autoplay entirely for visitors who have asked for reduced
motion. To turn looping off for one video, untick **Loop & autoplay** in the
admin CMS, or set it in `data.json`:

```json
{ "type": "video", "src": "…", "caption": "…", "loop": false }
```
