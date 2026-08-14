# CLAUDE.md — build instructions for this repo

## What this is
The Atlas of Frontier-AI Mathematics: self-contained interactive HTML lessons on
the maths behind frontier AI, finance-anchored throughout. `index.html` is the
map/tracker. **`LESSON_SPEC.md` is the contract — read it in full before touching
any lesson.** `lesson-08-svd.html` is the v2 exemplar: match its structure, depth,
vocabulary-upfront block, interactive quality, and tone.

## The job (two queues, in order)

1. **Retrofit L1–L15 to v2 format.** L8 is done (it is the exemplar). Order:
   L1, L2, L3, L4, L5, L6, L9, L10, L11, L12, L13, L14, L15, then L7 as a light
   pass only (it is already applied/finance-native). The per-lesson finance
   mapping is in LESSON_SPEC.md ("Retrofit queue"). Retrofits KEEP their existing
   filename and storage key.
2. **Build L16–L47** in numeric order (Wing III → IX), per the spec's build queue
   and finance mappings — unless Daniel reorders.

## Non-negotiables (per lesson)
- Single self-contained HTML file; no build step; only external dep is KaTeX
  0.16.9 from cdnjs. Storage shim included (copy from L8). Storage key
  `mfs:lessonNN` — never rename existing keys.
- All v2 spec elements: plain-words vocabulary upfront (no named theorem met
  cold), tight theorem box, 2 interactives where possible (3D with a
  concept-control where it illuminates), finance-first re-application beat,
  5+ deferred-validation MCQs, level badge, volarixs panel only if genuinely
  relevant, forward pointer.
- **Verification ritual before any commit** (spec §Verification): (1) node-parse
  the inline script; (2) re-implement the core numerics standalone in node with
  the SAME seeded LCG and call order, and check every quantitative claim in the
  copy against the output; (3) audit each MCQ answer index against its feedback.
  A lesson whose on-screen numbers contradict its prose is broken.
- Register every finished lesson in `index.html`'s `WINGS` array
  (`built:1`, `id:"lessonNN"`, `f:"<filename>"`).

## Working style
- Batches of 3–5 lessons; re-read LESSON_SPEC.md between batches to prevent
  format drift.
- Commit per lesson (`"L03 v2 retrofit: MLE on index returns, profile-likelihood
  interactive"`), push per batch — GitHub Pages redeploys from main.
- If the spec and the exemplar conflict, the spec wins; note the conflict in the
  commit message. If the spec is genuinely ambiguous, ask Daniel; otherwise
  don't ask.
- Do not touch `.nojekyll`, README deploy instructions, or existing storage data
  semantics.
