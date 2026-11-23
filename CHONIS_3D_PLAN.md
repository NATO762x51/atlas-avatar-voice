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


## Repository research (2026-11-22)
- **Three.js GLTFLoader**: https://threejs.org/docs/pages/GLTFLoader.html — browser rendering of glTF/GLB; suitable for realistic PBR meshes.
- **pixiv/three-vrm**: https://github.com/pixiv/three-vrm — VRM humanoid skeleton, expressions, and look-at support; useful if character is exported as VRM rather than plain GLB.
- **three-vrm examples**: https://github.com/pixiv/three-vrm/tree/dev/packages/three-vrm/examples — bones, expressions, animation, Mixamo retargeting examples.
- **Google MediaPipe Face Landmarker**: https://developers.google.com/edge/mediapipe/solutions/vision/face_landmarker — 52 expression blendshape scores from camera input; optional face-performance capture, NOT text-to-speech lip sync.
- **DanielSWolf/rhubarb-lip-sync**: https://github.com/DanielSWolf/rhubarb-lip-sync — derives timed 2D mouth cues from recorded audio; useful for pre-rendered lines, not a direct live browser TTS solution.

### Recommended architecture
Use Three.js + GLTFLoader for a realistic GLB first. If the selected asset is VRM, use @pixiv/three-vrm. Preserve the existing speechSynthesis/SpeechRecognition controls and portrait fallback. Add AnimationMixer for bundled skeletal animations and a morph-target mapping layer for mouth and facial expressions. Do not call the current word-boundary mouth approximation phoneme-accurate. Test mobile Safari and licensing before adopting any third-party model.

### Selection gates
A candidate character must match the approved lean proportions and facial design, support body rigging and facial morph targets, have an explicit redistribution/use license, and render acceptably on iPhone. No candidate model has yet been acquired or approved. Do not ship a mismatched placeholder as Chonis.
