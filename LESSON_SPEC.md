# Lesson build spec — locked format

Every lesson in this atlas is a **single self-contained HTML file**. This spec is the
contract: any new lesson (human- or AI-built, in chat or in Claude Code) must satisfy
all of it before it ships.

## Required elements (all mandatory)

1. **Real formulas, every term explained.** KaTeX-rendered, at genuine formal depth —
   not toy versions. Each display formula is followed by a glossary list (`.glo`)
   explaining every symbol.
2. **A derivation / "precise statement" theorem box** (`.theorem`) stating the result
   rigorously, in serif voice.
3. **Live interactive controls that visibly recompute.** At least one substantial
   interactive (SVG/canvas) where dragging a slider or clicking visibly changes the
   mathematics. Verified numerically before shipping (see Verification).
4. **A "twist" rigour beat** (`.twist`) — the surprising/deeper fact that upgrades the
   standard telling.
5. **A "Why this matters · volarixs" panel** (`.vol`) connecting the lesson to the
   user's quant/vol-derivatives platform and markets work.
6. **Deferred-validation MCQs.** 5 questions (6+ for long applied lessons). Selecting
   an answer only highlights it; validation happens ONLY on an explicit "Check answers"
   button. After checking: correct answer green, wrong pick red, feedback paragraph
   shown per question, score displayed.
7. **Education-level badge** in the header: US level + French equivalent (see
   Calibration).
8. **Progress persistence.** On check, write
   `window.storage.set('mfs:lessonNN', JSON.stringify({done:true, retrieval:'k/n', ts:Date.now()}), false)`.
   On load, read the same key and show a "completed · k/n" chip if present.
9. **Storage shim** at the top of the inline script so the file works both as a Claude
   artifact (window.storage) and on the web (localStorage):

```js
/* storage shim: window.storage (Claude artifacts) or localStorage (web) */
if(!window.storage){window.storage={async get(k){const v=localStorage.getItem(k);if(v==null)throw new Error('missing');return{key:k,value:v}},async set(k,v){localStorage.setItem(k,v);return{key:k,value:v}},async delete(k){localStorage.removeItem(k);return{key:k,deleted:true}},async list(p){const ks=[];for(let i=0;i<localStorage.length;i++){const kk=localStorage.key(i);if(!p||kk.startsWith(p))ks.push(kk)}return{keys:ks}}};}
```

10. **Forward pointer.** The completion banner names the next lesson in the wing.

## Content preferences

- **Finance-anchored examples wherever possible** (locked preference, Aug 2026):
  indices, FX, commodities, derivatives. E.g. backprop = all Greeks in one adjoint
  pass; convex portfolio variance because Σ ⪰ 0; reparameterization = pathwise vs
  likelihood-ratio Greeks; log-loss of a directional forecast; entropy of a
  regime-probability vector. The volarixs panel should reference the user's own
  primitives (Cross-Matrix cells, pca_factors, regime HMM, sign_stability) where
  they genuinely connect — never invent connections.
- Cross-reference earlier lessons by number ("the XᵀX from Lessons 6–7"). The atlas is
  a web, not a list.
- English prose. Serif for theorem voice, mono for numbers/code, paper/ink theme.

## Education-level calibration (locked)

Calibrate by **content actually taught, NOT year-name** — French labels run ~1 year
higher than US for the same material (prépa effect). Reference points:
UG core / prépa MPSI (L6) · UG intro→int / L2–L3 (L1) · adv UG / L3–M1 · ENSAE 1A (L2)
· Sr UG→grad / M1 · ENSAE 2A (L3, L11, L13) · adv UG→grad / M1–M2 · ENSAE 2A–3A
(L4, L8, L9, L15) · Grad / M2 · ENSAE 3A (L5, L7, L10, L14, L17) · Grad / M2–PhD
(L12 and most of wings V–IX) · PhD / M2 advanced (L25, L40, L43). Reserve the top
tier for genuinely graduate material.

## Visual theme (all lessons share it)

- Palette: `--paper:#FAFAF6 --ink:#1A1C22 --accent:#24507A --series:#B07A2E`
  with a `prefers-color-scheme: dark` variant. Copy the `:root` block from any
  existing lesson.
- KaTeX 0.16.9 from cdnjs. Fonts: system sans for prose, Iowan/Palatino serif for
  theorem voice, ui-monospace for numbers.
- Layout container `max-width:750px`. Section rules `.sec` in small-caps mono.

## File conventions

- Filename: `lesson-NN-short-slug.html` (two-digit NN matching the atlas number).
- Storage key: `mfs:lessonNN`.
- After building a lesson, **add it to `index.html`**: set `built:1`, add
  `id:"lessonNN"` and `f:"<filename>"` on its row in the `WINGS` array.

## Verification ritual (before a lesson is "done")

1. **Syntax**: extract the inline `<script>` and parse it with
   `new Function(...)` in node (stub `document`/`window`). Zero tolerance.
2. **Numerics**: re-implement the lesson's core computation standalone in node and
   check it against theory (e.g. cosine std ≈ 1/√d; Strassen == naive product;
   backprop == finite differences; H(p,q) == H(p)+KL to machine precision).
3. **MCQ audit**: every correct answer index matches its feedback text.

## Remaining build queue (L16–L47)

Wing III: L16 information bottleneck.
Wing IV: L17 attention (softmax, Q/K/V) · L18 RoPE · L19 residual stream +
LayerNorm/RMSNorm · L20 superposition.
Wing V: L21 scaling laws · L22 double descent · L23 grokking · L24 emergence ·
L25 NTK/lazy regime.
Wing VI: L26 diffusion/score SDEs · L27 flow matching · L28 VAE/ELBO · L29 GAN minimax.
Wing VII: L30 MDP/Bellman · L31 REINFORCE · L32 actor-critic · L33 PPO/KL ·
L34 MCTS · L35 RLHF/Bradley-Terry · L36 DPO & GRPO closed forms.
Wing VIII: L37 SSM/Mamba · L38 MoE routing · L39 test-time compute · L40 ICL as
implicit optimization · L41 mech interp / linear representation · L42 AlphaProof.
Wing IX: L43 PAC/VC/Rademacher · L44 deep bias–variance · L45 manifold hypothesis ·
L46 geometric DL / SE(3) · L47 optimal transport / Wasserstein.
