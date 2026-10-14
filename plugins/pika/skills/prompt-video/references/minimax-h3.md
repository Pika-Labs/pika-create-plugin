# MiniMax H3 — Prompt Guide

H3 builds a complete audiovisual timeline — picture, action, dialogue, and sound — in a single pass. Its prompt is not free prose; it is a structured rewrite made of **three core fields** on the timeline, optionally preceded by a keyframe/reference instruction. It works from text alone, from a starting image (or first/last keyframes), and from full references (subjects, images, videos, audio). Write every detail so it corresponds to something visible or audible.

## The three core fields
Every prompt body contains these, in order:

```
integrated_multimodal_description: [Shot 1] ...

overall_soundscape: ...

non_diegetic_music: ...
```
- **integrated_multimodal_description** — the main body: visual style, composition, subjects, actions, shot changes, camera, speakers, dialogue/singing, and synchronized diegetic sound, developed along the timeline.
- **overall_soundscape** — 1–4 sentences summarizing ambient sound, physical-action sounds, and non-verbal human sounds across the whole video (wind, footsteps, fabric, impacts, breathing, laughter). Don't repeat dialogue/singing/diegetic music here. Use `N/A` only for deliberate full silence.
- **non_diegetic_music** — 1–3 sentences for score only the audience hears. Describe instrumentation, tempo, rhythm, and dynamics — not mood words. Music a character can hear (radio, phone, live instrument) is diegetic and belongs in the description. Use `N/A` when there is none.

## Modes and the opening instruction
The first line aligns any reference image(s) to the timeline; then one blank line, then the core fields.
- **Text → video (T2VA):** no instruction line; begin directly with the core fields. Build the whole timeline from text.
- **First frame → video (I2VA):** the image is the actual 0.00s frame of `[Shot 1]`. Establish its style, subjects, composition, and anchors first, then develop forward. Structure: *first-frame anchor → action onset → continuous development → result/reaction.* Keep identity, clothing, colors, key objects, and spatial relationships consistent.
- **First + last frame (FL2VA):** describe the *path* between the two frames (how the subject moves, poses change, objects are handled, composition and lighting transition) — not two static descriptions. Favor a single shot so the model interpolates continuously; the last frame must be reached at the end. Structure: *first-frame state → intermediate changes → narrowing differences → last-frame state.*
- **Last frame (L2VA):** the image is the final frame. Infer a plausible earlier state, then describe how everything converges onto it. Structure: *plausible preceding state → action/transition path → gradual convergence → last-frame landing.*

## Writing the description along the timeline
**Style opening.** Begin `[Shot 1]` with the overall style and initial composition — e.g. `Cinematic`, `live-action`, `2D-animated`, `3D CG`, `claymation`, `watercolor`, `vintage film`. For keyframe/reference tasks, derive the style from the image; for text, pick it from the brief.

**Shots and cuts.** `[Shot 1]` has no timestamp. Later shots start with a strictly increasing cut time inside the duration: `[Shot 2] At 00:03.500, the camera cuts to …`. Use `the camera cuts to` / `the shot cuts to` / `transitions to` / `changes to` / `switches to`; use cross-dissolve, fade, or wipe only when asked. A cut should introduce new information (subject, space, state, viewpoint, or time); if only distance or a slight angle changes, prefer camera motion instead.

**Camera motion = type + amplitude + speed**, written as natural action inside the shot (not stacked labels). Add amplitude/speed only when meaningful; medium amplitude and normal speed are omitted.

| Type | Meaning |
|---|---|
| Zoom In / Zoom Out | focal length changes, body still |
| Push In / Pull Out | camera moves forward / back |
| Pan Left / Pan Right | pivots horizontally in place |
| Truck Left / Truck Right | translates horizontally |
| Tilt Up / Tilt Down | pivots vertically in place |
| Pedestal Up / Pedestal Down | whole camera moves up / down |
| Arc Shot | arcs around the subject |
| Tracking Shot | follows a moving subject |
| Static Shot | position and lens still |
| Shake Slightly / Shake Strongly | slight / strong shake |
| POV | subject's point of view |
| Roll Clockwise / Counterclockwise | rolls around the lens axis |

Amplitude: `with small amplitude` / `with large amplitude`. Speed: `at slow speed` / `at fast speed`.
> "The camera pushes in with small amplitude at slow speed toward the folded letter in her hands."

**Speakers, dialogue, singing.** Give each vocalizing subject a stable ID — `(S1)`, `(S2)`, compound `(S1,S2)` for joint speech; a speaker keeps its ID across shots, and silent characters get none. On first appearance, establish identity (type, age, gender, on/off-screen, pitch, timbre, rate, accent). Keep the identifying phrase, ID, action, and delivery *outside* `<d>`; inside `<d>` put only a language tag and the exact spoken words, verbatim — never translate or rewrite.
> `The young woman with a quiet, breathy voice (S1) says: <d>[English] I get off at the next station.</d>`

For voiceover use the exact phrase `says in an off-screen voiceover`, and immediately note the on-screen character's lips stay closed. When a line crosses a cut, mark `<scenetrans>` at both connecting points and say the audio continues; use `<cutoff>` when speech is truncated by the video end.

**On-screen text.** Put any visible sign, banner, label, subtitle, or neon text in double quotes, verbatim, untranslated: `A red neon sign reading "营业中" glows above the doorway.`

## Full-reference mode (subjects, images, videos, audio)
When you supply references, the rewrite grows to **six sections in order**: `subject_definitions`, `summary`, `retention_analysis`, `detailed_description` (the main body here, replacing `integrated_multimodal_description`), `overall_soundscape`, `non_diegetic_music`. State the style in a sentence or two *before* `[Shot 1]`.

**Reference labels** (defined once in `subject_definitions`, reused everywhere):
- `<Subject N>` — reusable visible content (person, animal, object, scene, clothing, prop, style, action, pose). It's the content unit used in the target, not the file. One subject may draw from several assets: `<Subject 1> is the woman whose appearance comes from <Picture 1> and whose walking motion comes from <Video 1>.`
- `<Picture N>` — an image acting as a concrete frame (first/last/keyframe) or a storyboard anchor. If an image only defines a character/scene/style, cite it inside that subject instead of giving it its own line.
- `<Video N>` — whole-video relationships: editing a source, continuing from its end, or referencing its camera/cuts/rhythm/structure.
- `<Audio N>` — a copied or referenced audio signal (music style, voice timbre, dialogue/lyrics, beat). When it maps to a target speaker, reuse that speaker's ID: `<Audio 1> is the voice-timbre reference for <Subject 1> (S1).`

**`summary`** opens with a bracketed task-type prefix, combining types with ` + `: `keyframe completion`, `reference generation`, `video editing`, `video continuation`, `audio reuse`, `audio reference`. Mere presence of a video/audio doesn't create a type — camera/cuts/rhythm-only references are `reference generation`; use `video editing`/`video continuation` only when the source is actually edited or continued.

**`retention_analysis`** — one line per label, stating how it's kept. Visible content uses `fully_preserved` / `partially_preserved` / `attribute_transfer` / `weak_reference`; audio uses `fully_copy` / `partially_copy` / `reference` / `weak_reference`. New actions or backgrounds added in the target are not "losses" of fidelity.

**`detailed_description`** — normally 350–500 English words for generation tasks (dialogue-dense content fits the full spoken timeline rather than hitting a count). Introduce each important `<Subject N>` at its first clear appearance with its referenced traits, frame position, and current action; reuse the label after. Anchor frames naturally: `the shot begins from <Picture 1>`, `the shot ends on <Picture 3>`. When a referenced subject speaks, keep both labels: `<Subject 2> (S1) turns and says, <d>[English] …</d>`.

## Examples
**Text → video (compact):**
```
integrated_multimodal_description: [Shot 1] Live-action, cinematic, a medium-wide shot frames a baker opening the shutters of a small street bakery before sunrise. The camera pushes in with small amplitude at slow speed as the middle-aged baker with a calm, slightly raspy voice (S1) sets a fresh loaf on the counter and says: <d>[English] First batch of the morning.</d> [Shot 2] At 00:05.000, the camera cuts to a close-up of steam rising from the sliced bread while his final words carry over from the previous shot.

overall_soundscape: Wooden shutters scrape open over a quiet street as trays clink softly inside. A doorbell rings once, then light footsteps and the crisp sound of bread being sliced.

non_diegetic_music: A soft acoustic-guitar pattern at a moderate tempo, joined by sparse upright-bass notes and a gentle fade at the end.
```

**First frame → video (compact):**
```
For the target video, at 0.00 seconds into the target video, <Picture 1> (from [Shot 1]) is fully referenced.

integrated_multimodal_description: [Shot 1] Live-action, cinematic, the young woman shown in <Picture 1> stays beside the rain-covered train window, preserving her appearance, clothing, seat, and the carriage layout. The camera trucks right with small amplitude at slow speed as she lifts her gaze from a folded letter toward the passing city lights. The quiet, breathy young woman (S1) says: <d>[English] I get off at the next station.</d> She folds the letter along its existing crease.

overall_soundscape: The train wheels keep a steady metallic rhythm under a low ventilation hum; rain ticks on the glass and paper rustles in her hands.

non_diegetic_music: Sustained cello at a slow tempo with widely spaced piano tones, gradually decreasing in volume.
```
