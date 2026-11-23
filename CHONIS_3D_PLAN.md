# Chonis 3D avatar integration

This branch prepares the existing Atlas Voice web app for a full-body, rigged 3D avatar. It does **not** claim the approved image sheet is already a rigged model.

## Approved character reference
- Adult human Chonis; tallish, slender, lightly toned, natural proportions.
- Long dark hair; West Coast black-and-gray floral and portrait sleeve tattoos.
- Ornamental neck tattoo; no “Chicana” chest lettering; no large back piece.
- Mini-skirt wardrobe variations; maintain one consistent face and body across poses.
- The latest approved image sheet is the visual source of truth; obtain a licensed model/texture and verify likeness before replacing the portrait.

## Asset contract
Place a legally usable, rigged glTF binary at `assets/chonis.glb`.
Prefer a humanoid skeleton with head, neck, spine, arm and leg bones, facial blendshapes, and mouth-open/viseme targets. Optimize for mobile: compressed textures, limited draw calls, and an appropriately sized mesh.

## Implementation phases
1. Add a responsive Three.js viewer that detects whether `assets/chonis.glb` exists and falls back to the existing portrait.
2. Load the model with GLTFLoader; fit camera to model bounding box and handle WebGL failure.
3. Add idle breathing, blinking, head turns, and restrained gestures using available rig controls.
4. Drive mouth blendshapes from speech events as an interim approximation; add audio/phoneme-driven visemes when a suitable audio source exists.
5. Test iPhone Safari microphone permissions, speech synthesis, playback, rendering, and reduced-motion behavior.

## Current state
The current `index.html` uses an image overlay to simulate lip movement and optionally plays `atlas-full-body.mp4`. It does not yet render a 3D character. Avoid replacing it until a working GLB is available.
