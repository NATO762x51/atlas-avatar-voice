# Atlas 2.0 — Animation plan

## Current baseline (verified)
- `index.html` is a single-page web app with an Atlas portrait and a browser speech-synthesis greeting.
- Mouth animation is a CSS overlay repeating on a timer; it is not phoneme-based lip sync.
- An optional `atlas-full-body.mp4` can play if the file is hosted. This is a prerecorded clip, not an interactive animated character.
- There is no `package.json` at the repository root.

## Goal
Preserve the existing Atlas visual identity while replacing the flat portrait mouth effect with a natural, responsive avatar that works in mobile browsers and can later be packaged for Windows.

## Implementation phases
1. **Non-destructive prototype**: keep `index.html` unchanged. Add a separate `atlas2/` prototype and a feature flag or explicit preview link. Validate iPhone touch and audio playback.
2. **Avatar assets**: obtain a licensed, rigged GLB/VRM character with face blendshapes (visemes, blink, smile, brows) and skeletal body bones. Use the reference video for visual direction; a video alone is not a rigged 3D model.
3. **Runtime**: evaluate Three.js with VRM support or standard GLTF animation. Load a compressed character with adjustable resolution and motion quality.
4. **Speech animation**: map audio/phoneme or timed viseme cues to facial blendshapes. Use speech start/end events only as a fallback, not as accurate lip-sync timing.
5. **Behavior**: add independent blinking, gaze, breathing, head motion, posture shifts and context-aware hand gestures. Blend motions smoothly and allow reduced motion.
6. **Packaging**: validate the web prototype on iPhone and Alienware; consider Tauri/Electron desktop packaging after runtime performance is measured.

## Acceptance criteria
- Original `index.html` remains functional.
- Atlas mouth shape changes with speech content rather than only opening and closing at a fixed rate.
- Eyes, brows, head, shoulders and hands move naturally without constant exaggerated motion.
- Graceful low-power mode for mobile devices.
- Assets are licensed and tracked; no secrets committed.

## Open inputs
- GPU model and available VRAM on Alienware (can wait).
- Licensed rigged avatar asset; reference footage helps define appearance but is not sufficient by itself.
- Speech source and whether audio/viseme timestamps can be obtained.
