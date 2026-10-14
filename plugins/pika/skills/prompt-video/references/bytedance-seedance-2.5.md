# ByteDance Seedance 2.5 — Prompt Guide

Seedance 2.5 generates video from text alone or from image, video, and audio references, and it can also edit and extend existing videos. Start by stating what you want to generate, then add reference materials, event progression, visual treatment, and audio as needed. Its defining skill is **reference control** — telling the model exactly what each material contributes, and which materials belong to which scene.

## Core prompt formula
Combine these flexibly; omit any you don't need:

> **Subject + Action/Event + Scene & Environment (opt) + Visual Style (opt) + Camera Movement/Cut (opt) + Audio (opt)**

- **Subject + Action/Event** — who/what is doing what. The foundation.
- **Scene & Environment** — location, time, weather, spatial relationships, background state.
- **Visual Style** — lighting, color, materials, image texture, overall mood.
- **Camera** — shot size, angle, movement, focus subject, transitions.
- **Audio** — dialogue, voice characteristics, ambience, sound effects, music.

Basic shape:
```
<Subject> performs <primary action/event> in <scene>.
The visuals feature <visual style>.
Use <shot size, angle, camera movement, or cuts>.
Audio includes <dialogue, ambience, sound effects, or music>.
```

## Define every reference's role
When you supply references, name exactly what each one contributes, and add **exclusions** whenever a material's people, background, or composition might leak into the output. Write the mappings *in the prompt* — don't rely on labels drawn inside images, and don't make the model guess which material is which.

```
@Image 1 defines <subject>'s <appearance, clothing, structure, or material>. Do not use the image background.
@Video 1 defines <motion, camera movement, or pacing>. Do not use the person's identity or scene.
@Audio 1 defines <character/sound>'s <voice, dialogue, ambience, or music>.
```
- **Multiple views of one subject:** say so explicitly — "@Image 1…4 all define one folding desk lamp; the output must contain only one lamp." Separate view images are more stable than a collage.
- **When a reference video already carries the motion/camera/sequence**, state only which attributes to inherit; re-describing the motion can conflict with the reference.
- Prefer a modest number of distinct subjects per image set for stability; you can push higher, but stability drops as materials grow.

## Audio & text syntax
Natural language works, but to separate layers explicitly:

| Content | Syntax | Example |
|---|---|---|
| Music | `( )` | `(Soft, rhythmic piano music plays in the background)` |
| Sound effects | `< >` | `<A bell rings in the distance>` |
| Dialogue | `{ }` | `{Hello, welcome back.}` |
| Subtitles | `【 】` | `【Chapter One: Departure】` |

**Dialogue language reinforcement** — when speech isn't Chinese, or you need a specific variety, state it before the line:
`Dialogue language: American English. The girl says in natural, conversational American English: {I thought you weren't coming.}`

## Many references → map before you write
With lots of materials the goal isn't to cram every reference into one sentence — it's to define relationships. Work in this order:

**Define roles → map subjects → group by type → subject profiles → select by scene.**
1. **Map each subject individually:** `<Character A> corresponds to @Image 1. Use only the appearance, hairstyle, and clothing.` Never write "@Images 1–4 define four characters respectively" — it doesn't say which is which.
2. **Group by type** with headers like `[Characters]`, `[Props]`, `[Scenes]`, `[Motion and Audio]`; add "do not interchange appearances/clothing/actions/dialogue."
3. **Subject profiles** for a character reused across scenes — collect its appearance image, fixed props, locations, motion refs, and a "do not" list in one block.
4. **Select references by scene** — per scene, list which subjects/props/scene/motion to *use*, the single event, and the **end state** (positions, prop ownership, what's visible). The aim is to help the model pick the right materials for the current scene, not show everything at once.

## Long / multi-event videos: stages + end states
Divide the story into consecutive **stages**, each with **one primary state change** and an explicit, directly-visible **end state**.
```
[Stage 1]
Initial state: <characters, props, scene>.
Primary event: <one action/event>.
End state: <positions, prop ownership, visible scene state>.
[Stage 2]
Continue from the previous stage: <what must stay unchanged>.
...
[Maintain Consistency]
Keep <identities, count, clothing, prop ownership, spatial direction, audio relationships> consistent.
```
**Timestamps & pacing** — use stages by default. Reach for time only to control a critical beat: **time ranges** (`0–3s… 3–7s…`, consecutive and non-overlapping) budget pacing; an **exact point** (`At 5 seconds, whip-pan left`) pins one key event; **relative timing** (`Three seconds after she presses the button…`) sets a delay. Ranges are budgets, not edit points — don't demand "three actions in one second."

## Editing an existing video
Define the source as the **sole editing master**, then the edit scope, the target material, and what to preserve.
```
[Edit Goal] Edit @Video 1. Within <whole video or time range>, <add/remove/replace/adjust> <object, region, or audio category>.
[Source Video Role] @Video 1 is the sole editing master. It defines <characters, scene, actions, composition, camera, occlusion, audio, event order>.
[Target Material Role] @Image 1 / @Audio 1 defines <attributes of the target>.
[Edit Scope] Modify only <object/region/time range/audio category>.
[Content to Preserve] Keep <what must not change> from @Video 1.
```
- **Subject replacement:** the new subject *inherits every appearance, motion, occlusion, and exit* of the original, including timing/path/speed.
- **Background replacement:** modify only outside the subject silhouette; keep identity, features, clothing, expression, position, size, and motion.
- **Audio editing:** dialogue, language, voice, music, and SFX can be changed separately — name the target sound, the change, and which sounds stay.
- Editing preserves the source's framing and roughly its length; keep event order intact.

## Extending a video
Align the **boundary frame** first, then describe new content.
- **Forward (after):** the extension's first frame continues from the source's last frame — restate that continuous state (pose, props, background, camera, lighting, motion direction), *then* add the new action.
- **Backward (before):** describe what happens before the source, then define the source's first frame as the explicit **end state** of the extension; keep later characters/effects from entering the preceding segment too early.
- Boundaries connect naturally, not pixel-identically — inspect both sides plus the whole new segment.

## Keyframes, storyboards & blockouts
- **First & last frames:** state `@Image 1 is the first frame` and `@Image 2 is the last frame` (same aspect ratio — mismatched ratios stretch the last frame); extra images may define subjects/props/scene without changing either composition. Describe one continuous action from first to last.
- **Multi-keyframe sequence:** "Use @Image 1 through @Image N as keyframes in this order," then the key state each represents. Separate images align better than a combined grid; they control stage order and key states, not every frame.
- **Storyboard grid:** one image conveys shot order and rough composition (prefer ≤15 panels, clean line art, minimal text). State the reading order, then each panel's subject/shot/style/audio; don't inherit the grid's line-art style or labels.
- **Blockouts:** decide first whether it's a **coarse blockout** (grey geometry giving action paths, blocking, camera, cuts, lighting, sound rhythm — map each shape to its final subject and add appearance images) or a **fine blockout** (a complete clean model you re-render for materials/colors/scene/style — remove path lines, axes, camera frustums). Preserve structure/action/camera; define what to re-render.

## One-click video
Turn a set of images (optionally a style-reference video) into a packaged edit — never just "make these into a video."
> **Material roles → image order → motion amount → editing style → visual treatment → audio.**
Name each image's job, whether order is fixed or model-chosen, how much motion each image gets (subtle parallax/push-in vs local action), what stays stable, and the edit rhythm/transitions/color/audio. A style-reference video should contribute *only* rhythm/transitions/subtitle style/music — not its identities or scenes.

## Seamless transitions
Generate bridge content between two clips.
> **Before video → after video → trigger action → camera movement → visual transformation → arrival state → audio.**
Identify the before/after clips and what to keep stable in each; describe the trigger (dive, character rotation, foreground occlusion, object morph, push/pull), how shape/material/light/space transforms into the next clip's opening, and how the audio crosses over. It's continuity, not a pixel-identical splice.

## Emotional direction
Emotion words ("tense," "warm") set direction but leave the acting loose. For stable performance, add **2–4 observable cues** — eye movement, brow tension, mouth, breathing, gaze direction, hand movement.
- **Single transition:** starting emotion → triggering event → immediate reaction → gradual change in specific cues → final restrained/explicit behavior.
- **Multi-stage:** progress through triggering events, each with its observable reaction.

## Cinematography terms
- **Basic** (usable directly): shot sizes (extreme wide → extreme close-up), moves (push in, pull out, pan, lateral, follow, orbit, dive, dolly out, tilt up, handheld shake), positions (low angle, overhead, first-person).
- **Popular techniques** (one-take, dolly zoom, aerial, FPV, bullet time, handheld, bounce speed ramp): also say which subject the camera follows/orbits, and where the move begins and ends.
- **Uncommon or ambiguous terms:** keep the term but translate it into a directly observable change — `Rack focus: shift focus from the foreground leaves to the person behind; leaves blur as the face sharpens.` Numeric aperture/focal values are fine, but the intended visible result is clearer than the number.

## Pre-submission checklist
- Subject and primary action/event stated clearly.
- Every reference states what to use **and** what not to use; each distinct character/product/prop is named and bound.
- References selected by scene, not all forced to appear at once.
- Each long-video stage has one primary change and a clear end state; identities, counts, clothing, prop ownership, and spatial relationships stay consistent.
- Editing defines the sole master, edit scope, target quantity, and what to preserve.
- Abstract emotions and uncommon camera terms paired with observable cues.
- First/last frames and keyframes carry one role per image; first and last images share an aspect ratio.
- For extension, the boundary frame, motion trend, and audio continuity are checked.
