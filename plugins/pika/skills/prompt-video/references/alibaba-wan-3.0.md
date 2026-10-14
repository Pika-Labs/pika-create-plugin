# Alibaba Wan 3.0 — Prompt Guide

The prompt describes the content and motion of the video — it's how you control what appears on screen. Wan 3.0 can generate a complete video from a single sentence, but the more complete, precise, and detailed the prompt, the higher the quality and the closer it aligns with your intent. The guide gives proven formulas per use case; treat them as starting points and build on them.

## Basic formula — for exploration
Simple, open-ended prompts leave the model more room and often produce more imaginative results.
> **Subject + Scene + Motion**
- **Subject** — the main focus (person, animal, plant, object, or an imagined entity).
- **Scene** — the environment (background and foreground; real or fictional).
- **Motion** — the subject's specific movement and the general motion in the scene, from stillness and subtle moves to large-scale dynamic action.

## Advanced formula — for control
Add richer detail to raise quality, vividness, and storytelling.
> **Subject + Setting + Motion + Aesthetic Control + Stylization + Sound**
- **Subject description** — appearance in adjectives/short phrases (e.g. "a black-haired Miao girl in ethnic minority clothing").
- **Scene description** — the environment in adjectives/short phrases.
- **Motion description** — amplitude, speed, and effect ("violently swaying", "slowly moving", "shattering glass").
- **Aesthetic control** — light source, lighting environment, shot size/framing, camera angle, lens, camera movement.
- **Stylization** — the visual style ("cyberpunk", "line-drawing illustration", "post-apocalyptic").
- **Audio** — background SFX, music, dialogue, narration; voice qualities are directable too (e.g. a deep blended voice, a cute voice).

## Image-to-video formula
The source image already sets the subject, scene, and style — so the prompt should focus on motion and camera.
> **Motion description + Camera movement**
- **Motion** — how the elements move ("running", "waving hello"); use adverbs ("quickly", "slowly") for pace and intensity.
- **Camera movement** — "dolly in", "pan left", etc.; to hold the camera, say "static shot" / "fixed shot".

## Sound formulas
Wan renders native audio, so voices, effects, and music can be directed precisely. A sound description details the audio and how it changes over time so it aligns with the visuals.
- **Voice** = the spoken line + emotion + intonation + speech rate + timbre + accent.
  > *A man talks about his insomnia. He says, "love is not getting but giving." Relaxed tone, moderate pace, bright clear voice, American English.*
- **Sound effects** = sound-source object + action + ambient sound.
  > *A piece of glass falls from the table onto a wooden floor with a "shatter" sound, in a quiet indoor environment.*
- **Background music** = BGM + style.
  > *On a rainy night, in a gloomy narrow corridor with a window at the end, suspense-style background music plays.*

## Reference-to-video formula
Wan 3.0 generates from the main character(s) in a reference input — appearance, motion, and voice. The character can be a person, cartoon, pet, or prop; **up to 2 characters per video.**
> **@Reference subject + Action + Dialogue**
- **@Reference** — use `@` to cite source materials, listed in order (`@Image 1`, `@Video 2`, `@Audio 1`); mention a reference multiple times to control exactly how it's applied.
- **Action** — the reference's movement and state: stillness, facial expressions and emotional shifts, body movement, reactions to force, position changes.
- **Dialogue** — what the reference says (monologue or multi-character); you can borrow a specific timbre ("use the voice from @Audio 1").
- **Video-timeline reference** — cite timeline elements to inherit, e.g. the camera-movement style of `@Video 1`.
- **Clay-render reference** — for a 3D preview clip: "Transform this 3D preview video into a final render, replacing the … in the preview with … characters."

> *A whimsical fairy-tale scene. @Image 1 bounces and plays on the grass while @Image 2 plays the piano under an apple tree. An apple falls on @Image 2's head. Using the voice from @Audio 1, @Image 1 happily points at @Image 2 and says, "You're going to be a scientist!"*

## Multi-shot formula
Generate coherent multi-shot narratives with control over shot structure, camera positions, and timing; subjects, scenes, and atmosphere stay consistent across shots. (A "Smart Multi-Shot" mode can build multi-shot videos from simple prompts.)
> **Overall description + Shot number + Timestamp + Shot content**
- **Overall description** — a brief overview: theme, narrative style, main emotion, or core event.
- **Shot number** — number each shot to organize structure.
- **Timestamp** — the time range for each shot, so content aligns to the timeline.
- **Subject behavior** — per shot, the specific actions, speech, expressions, and postures.

> *Third-person short play about losing and regaining hope.*
> - *Shot 1 [0–3s]: the character sits alone at the edge of the playground, looking down at a letter, then sighs, eyes confused and sad.*
> - *Shot 2 [4–6s]: hard cut, fixed camera, close-up on the eyes glistening with tears.*
> - *Shot 3 [7–10s]: hard cut to a simple classroom; a second character stands with a gentle, determined gaze and walks toward the first.*

## Video editing formulas
Combine text, image, video, and audio inputs as control conditions to modify shot composition, story direction, local details, or timing.
> **Editing target + Editing action**
- **Element editing** — plainly state the change: add ("the man puts on a red hat"), replace ("replace the cat with a dog"), remove ("remove the cat from the grass"). With image references, point to a specific object ("change the man's clothing to the red jacket in the image"); with several images, cite by order ("wear the clothing from @Image 1 and the pants from @Image 2").
- **Global editing (style / lighting / color / weather)** — "change to an overcast day", "warm color palette", "convert to 2D cartoon style" (optionally "…shown in the image"); add "keep everything else the same" to hold the rest.
- **Temporal editing** — change actions or dialogue over time ("have the man pick up the cup and take a sip"); to change a line while keeping the voice, "maintain the character's timbre and tone, and change the girl's dialogue to: 'Hello World.'"
- **Video extension** — content/style/composition are set, so describe what changes next ("the man continues walking, then suddenly falls to the ground").

## Other controls
- **Shots** — the model infers camera movement and may produce single or multiple shots. To control count and timing, write `Shot 1 [0–3s]: … Shot 2 [3–6s]: …`. To force one take, say "generate a single shot" / "one continuous take."
- **Dialogue** — a described line (`X says: "…"`) is preserved verbatim; with no dialogue described, the model may add its own. To suppress it: "No dialogue throughout the entire video."
- **Background music** — with none described, the model adds BGM to fit the content. To suppress it: "No background music."
