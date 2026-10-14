# Kling v3 — Prompt Guide

Kling generates video from a text prompt, and optionally from a starting image. It rewards clear, structured, naturally-written descriptions over keyword spam. Keep prompts focused on a few strong ideas, describe motion and physics explicitly so subjects move with real weight, and use camera language and negative prompts to steer stability. Kling 3.0 puts extra emphasis on action physics, material texture, and — when audio is on — spoken dialogue with lip-sync.

## Prompt structure
Kling's official text-to-video formula:

**Subject + Subject Description + Subject Movement + Scene + Scene Description + (Camera Language + Lighting + Atmosphere)**

The bracketed camera / lighting / atmosphere block is optional, but strongly improves cinematic results.

> "A young woman wearing a flowing red dress, sprinting joyfully across a sunlit meadow. Flowers sway in the gentle breeze and birds soar overhead. Wide aerial shot, soft golden light, dreamy atmosphere."

For Kling 3.0, a complementary master formula foregrounds motion mechanics and texture:

**[Camera Movement] + [Subject & Action Physics] + [Environment/Lighting] + [Texture & Details] + [Audio/Emotion]**

## Guiding principles
- **Keep it concise** — the best results come from short prompts (roughly 40–50 words). Long run-on sentences and stacked style keywords confuse the model and produce muddled visuals.
- **Limit to 2–4 main ideas** — don't overload a single shot; keep each part concise but descriptive.
- **Write naturally** — use vivid, plain language, not keyword lists.
- **Be explicit, not vague** — replace words like "cinematic" with concrete camera terms such as "slow dolly-in".
- **Specify camera when it helps** — call out a camera style when it enhances the scene, and otherwise let it be.

## Camera language
Name the move directly rather than implying it. Common vocabulary:
- Handheld shoulder-cam with subtle sway
- FPV drone with 360° rolls
- Tracking shot; dolly in / dolly out; push-in / pull-out
- Over-the-shoulder; macro close-up with slow dolly-in
- Orbit; crane / jib up or down; whip pan

Keep camera-move magnitudes modest for smooth, cinematic motion without distortion.

## Action & physics
Kling 3.0 rewards spelling out the mechanics of motion so subjects don't float or slide:
- Describe weight transfer, e.g. "each foot landing heel-first, then rolling forward with visible weight transfer".
- Anchor hands to the objects they touch.

## Texture & detail
To avoid a plastic, over-smooth look, name real-world surface detail: film grain, skin pores, sweat, fabric creases, condensation.

## Dialogue & audio
When audio is on, format spoken lines so the model can lip-sync with the right emotion:

**[Character: Description, Voice Tone]: dialogue**

## Negative prompts
Kling tends to introduce drifting cameras, extra movement, and small frame-to-frame changes, so negative prompts matter most for stability and consistency. Use them to prevent sliding feet, extra fingers, and unwanted morphing during complex motion.

> "blur, distort, low quality, shaky camera, cartoon, anime, text, watermark, deformed face, extra limbs."

## Prompt adherence
Kling's prompt-adherence control runs from loose to strict: low values give the model maximum creative interpretation, the midpoint is balanced, and high values force strict adherence with less variation. A moderately high setting tends to produce the most consistent professional results.

## Starting images
When animating from an image, use a clean, well-lit starting frame; a clear frame with a matched, unobstructed pose is the single biggest factor in a good result. Recommended input sizes are 1024×1024, 1280×720, 1920×1080, or 1080×1920, with a minimum of 300×300.

## Examples
- **Official t2v:** a young woman in a flowing red dress sprinting across a sunlit meadow, flowers swaying and birds overhead — wide aerial shot, soft golden light, dreamy atmosphere.
- **Physics-forward (3.0):** a runner on a wet street, each foot landing heel-first with visible weight transfer, cold rim light, film grain and rain condensation on the lens, tense determined mood.
- **Dialogue (audio on):** [Woman: weathered, warm]: a single line delivered to camera in a quiet room, soft key light, subtle handheld sway.
