# Caricature Lab

A single-file, satirical 3D avatar creator. Runs in Safari, deploys on GitHub
Pages. `index.html` is the whole app — no build step.

## What changed in this version
The avatar is no longer modeled from scratch in code. It now **loads external
GLB characters** through `GLTFLoader`, with the old primitive mesh kept as an
automatic **fallback** when a GLB is missing. All clothing, props and
accessories attach to **named anchor points**, and animation runs through
`THREE.AnimationMixer` so Mixamo-style clips can be dropped in later.

## Folder layout
```
index.html
assets/
  avatars/      young-female.glb, young-male.glb, older-female.glb, older-male.glb
  clothing/     GLB clothing for anchors (placeholder geometry ships now)
  props/        GLB hand/back props (placeholder geometry ships now)
  animations/   GLB clips: idle / chant / point / hold-sign / record
  decals/       PNG art for tattoos / signs / patches
```
Each folder has its own README with exact filenames and requirements.

## How loading works
1. Pick a base character. The app instantly builds the primitive fallback so
   there's never a blank screen.
2. It then tries to load the matching GLB from `assets/avatars/`.
   - Found  -> the GLB replaces the primitive; the source pill turns green.
   - Missing-> it stays on the primitive; the pill says "no GLB found".
3. Accessories are rebuilt onto the new avatar's anchors either way.

## Anchor points
Every accessory mounts to one of these, so the same code works on a GLB rig or
the primitive body:

`Head` · `Face` · `Chest` · `Back` · `LeftHand` · `RightHand`

On a GLB, anchors snap to detected skeleton bones (Mixamo names supported);
if a bone isn't found, the anchor falls back to a point on the bounding box.

Drop a real GLB onto any anchor at runtime:
```js
attachGLB('RightHand', 'megaphone.glb');   // from assets/props/
attachGLB('Chest',     'activist-vest.glb');// from assets/clothing/
```

## Animation
- Tap an Animation button -> on a GLB avatar the app lazy-loads the matching
  clip from `assets/animations/` and cross-fades it in via `AnimationMixer`.
- No clip file yet? The primitive fallback plays built-in procedural motion, so
  the app animates even with an empty `assets/` folder.

## Design guardrails (kept intentionally)
- The radicalization meter only adds **political behavior** — expression,
  buttons, sign, megaphone, phone, activist vest, boots, chanting. It never
  touches hair, identity/style items, causes, tattoos or piercings.
- Style items (rainbow, dress, pride pin) are decoupled self-expression.
- Cause patches are **fictional only** — no real national flags or movements.

## Archetype packs
`ARCHETYPES` at the top of the script holds the packs. `left` is filled in;
`right`, `corporate`, `influencer`, `conspiracy` are stubbed and locked. Copy
the `left` shape to build a new one — the accent color themes the whole UI.

## Deploying on GitHub Pages
Commit the whole `caricature-lab/` folder (or its contents) to your Pages repo.
Because the app pulls Three.js from a CDN, the first load needs a connection,
then the browser caches it.
EOF
