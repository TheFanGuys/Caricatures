# assets/avatars/

Rigged GLB characters. The app looks for these exact filenames:

- young-female.glb
- young-male.glb
- older-female.glb
- older-male.glb

If a file is missing, the app silently falls back to the built-in primitive
mesh for that character (the source pill shows "Placeholder mesh").

## Rig requirements
- A humanoid skeleton. Mixamo rigs work out of the box.
- The loader auto-detects anchor bones by name fragment (case-insensitive):
    Head / Face   -> bone containing "head"
    Chest / Back  -> "spine2" / "spine1" / "chest" / "spine"
    RightHand     -> "righthand" / "hand_r" / "rightwrist"
    LeftHand      -> "lefthand"  / "hand_l" / "leftwrist"
- If no matching bones exist, anchors fall back to estimated points on the
  model's bounding box so accessories still attach (just less precise).
- The model is auto-scaled to ~2.5 units tall and dropped to the floor.

## Optional: baked-in animations
Any AnimationClips packed inside the avatar GLB are auto-registered by clip
name (idle, chant, point, holdSign, record).
