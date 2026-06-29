# assets/animations/

GLB animation clips (Mixamo exports work). The app lazy-loads one when you tap
an Animation button, by filename:

- idle.glb
- chant.glb
- point.glb
- hold-sign.glb
- record.glb

Each GLB should contain ONE AnimationClip as its first animation. It is played
on the avatar through THREE.AnimationMixer and cross-faded in.

Note: animation clips only drive GLB avatars. The primitive fallback uses its
own procedural motion, so the app still animates with zero asset files present.
