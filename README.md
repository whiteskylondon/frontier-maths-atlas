# The Atlas of Frontier-AI Mathematics

An explorable atlas of the mathematical machinery behind frontier AI — every core
idea rendered as a self-contained interactive HTML lesson: real formulas with every
term explained, live controls that visibly recompute, a rigorous theorem statement,
a "twist" that deepens the standard telling, finance-anchored examples, and
deferred-validation quizzes with progress tracking.

**Entry point: [`index.html`](index.html)** — the atlas map. 15 of 47 lessons built
(wings 0–II complete, wing III opened). Each built lesson links from the map.

## Run locally

No build step — plain static HTML.

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

## Deploy on GitHub Pages

```bash
gh repo create frontier-maths-atlas --public --source . --push
```

(or create an empty repo on github.com, then `git remote add origin <url> && git push -u origin main`)

Then: repo **Settings → Pages → Deploy from a branch → main / (root)**.
The site appears at `https://<user>.github.io/frontier-maths-atlas/`.

## Progress tracking

Each lesson stores completion + quiz score under the key `mfs:lessonNN`. Inside
Claude this uses the artifact storage API; on the web it falls back to
`localStorage` (per browser, per site). The two environments keep separate trackers.

## Building the remaining lessons

The locked format, calibration rules, verification ritual, and the full L16–L47
queue live in [`LESSON_SPEC.md`](LESSON_SPEC.md). Any session — chat or Claude
Code — should build against that spec and register each new lesson in
`index.html`'s `WINGS` array.
