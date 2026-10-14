# xAI Grok Imagine — Prompt Guide

Grok Imagine is xAI's Aurora-engine family for generating and editing images and video, with native audio synced into the clip in the same pass. The video engine reads the prompt autoregressively — left to right — and stops when the clip ends, not when your text ends. So the prompt is the script: the clearer the action, the cleaner the motion. Lead with what matters, keep prompts concise, and place every critical instruction in the first half of the string.

## Image prompting

**Formula:** `[Subject] + [style/mood] + [lighting] + [camera angle] + [finishing details]`

> "futuristic Tokyo street at 2am, rain-slicked asphalt, neon reflections, low-angle wide shot, cinematic fog, Blade Runner mood."

- **Be specific** — "a city at night" is weak; the prompt above is strong. Specificity beats vagueness on every axis.
- **Lighting is high-leverage** — "golden hour backlight", "overcast diffused light", and "hard rim light from the left" each produce completely different results.
- **Mood references beat adjectives** — "Blade Runner mood" or "Studio Ghibli feel" hands the model a rich visual library; "dark" or "soft" does not.
- **Keep the frame clean** — a clear subject against a defined background consistently beats a busy, crowded scene.
- **Editing (image-to-image)** — describe only the change you want, not the whole picture.

## Video prompting

The prompt is the script. Describe concrete physical actions, not moods. Instead of "cinematic and dramatic," write "she takes one step back, turns her head 30 degrees left, the coat hem catches the wind."

**Four elements, in priority order:**

1. **Motion verb** — what physically moves (the load-bearing element).
2. **Camera instruction** — one named move.
3. **Atmosphere** — environmental effects.
4. **Mood / audio** — one explicit audio cue.

Not all four are required every time. **Order matters:** the model weights elements that appear first, so lead with the motion verb or camera move and place atmosphere and audio at the end. Any instruction buried deep in a long prompt risks never executing before the clip ends.

**Camera / motion / atmosphere blueprint (image-to-video):**
`[subject core movement] + [camera trajectory / lens action] + [lighting shift / atmospheric transition]`

> "Man raises his coffee cup slowly, dolly zoom effect pushing toward his face, morning light intensifying to warm gold as steam rises."

- **Length scales with intent** — a short prompt (1–8 words) suffices for a strong source image ("the horse rears", "rain falls"); reach for a longer prompt (20–60 words) only to direct a color grade, lighting, or atmospheric effect the still lacks.
- **One action per clip.** Use video extension for longer sequences rather than cramming beats.
- **Multi-beat is comma-separated, max 2–3 beats.** For longer clips, structure with time markers: `[00:00] [00:04] [00:08]`.

### Motion
Name the specific motion verb rather than a generic "moves":
- **Humans** — turns, smiles, blinks, nods, walks, runs, jumps, lands, reaches, looks up/down, breathes, laughs.
- **Animals** — rears, bucks, leaps, prowls, shakes, stretches.
- **Objects** — falls, drifts, sways, spins, rises, flows, ripples, flickers, collapses.

Instead of "she moves," specify "she turns slowly toward camera."

### Camera
Name one explicit move: "slow dolly in", "static wide", "handheld follow from behind", "camera orbits the subject", "camera pans left" — over a vague "dynamic camera". Lead with camera intent for cinematic shots; placing the tracking or lens move early gives the engine time to establish framing before motion peaks.

To lock the frame, use the **negative instruction** "camera not moving" rather than "stable camera" — the negative form reliably locks the frame. Never stack contradictory camera instructions.

### Atmosphere
Stack a maximum of 2–3 environmental effects:
- **Dust** — "dust particles swirl around the subject"
- **Rain** — "rain falls in the foreground"
- **Fog** — "volumetric haze, low-lying fog"
- **Heat** — "heat shimmer rising from the ground"
- **Wind** — "the wind moves her hair and coat"

### Audio
Audio is native and synced in the same pass. It fires most reliably on:
- **Clear physical impacts** — "board clatter and crowd noise as the skateboarder lands"
- **Environmental / outdoor context**
- **Explicitly named audio** — "soft room tone, distant traffic, no music" lands better than "ambient sound"

Name dialogue lines, ambient layers, and SFX explicitly. Emotion-led prompts tend to return music-only, and lip-sync from a still is inconsistent.

## Working from a source image
When animating a still, the model already has the scene — it sees the subject, composition, color, and style. Don't re-describe what's in the image; supply only what the still cannot: motion, camera behavior, and atmospheric additions.

- **Start from a strong still.** Ensure the subject is clearly defined with clean edges and avoid compression artifacts — the composition locks as the first frame.
- **Never contradict the source.** Don't introduce subjects, environments, postures, or actions that conflict with what the image shows; contradiction collapses coherence immediately.
- **Compose the crop in the source.** For face fidelity, frame the shot in the source still rather than relying on the prompt alone.
- **Don't over-prompt a strong image.** Start short and add one element at a time.

## Testing and iteration
Run short 5–8s tests to validate structure before committing to longer hero clips. Iterate by adding one element at a time rather than rewriting from scratch.

## Common mistakes
- Redescribing the source image instead of directing the change.
- Aesthetic adjectives ("cinematic", "dramatic") without physical events.
- Contradictory camera instructions.
- Expecting guaranteed lip-sync from a still — use text-to-video for dialogue-driven content.
- Over-prompting a strong source image — start short.
- Burying a critical action deep in a long prompt, where it risks never executing.

## Examples
- **Portrait:** "She turns slowly toward the camera and smiles, soft window light, strands of hair drifting in a gentle breeze, shallow focus, quiet ambient room sound."
- **Product:** "The perfume bottle rotates slowly clockwise, soft studio light gliding across the glass, subtle reflections, faint ambient hum, camera locked."
- **Action:** "The skateboarder lands the jump, board clatter synced to impact, dust kicks up, low dynamic angle, camera not moving."
- **Nature:** "The leaves fall slowly through the autumn light, camera not moving, wind rustle sound."
- **Surreal:** "She's chewing, bored, camera not moving."
