# Black Forest Labs FLUX 3 Video — Prompt Guide

FLUX 3 turns prompts into clips and renders **synchronized audio with the video** in the same pass. Direct it like a scene, not a list of objects: state clearly what happens, how subjects move, how the camera behaves, and the overall atmosphere. It accepts anything from a short phrase to a long structured brief — start short to explore, then lengthen to lock in the details that matter (length alone isn't the goal).

## Choose the workflow
- **Text-to-video (t2v)** — generate a new scene from a prompt.
- **Image-to-video (i2v)** — animate a still: pin a **startframe** (exact opening frame, prompt drives motion), a **start + end frame** (FLUX fills the motion between), or **keyframes** (three or more ordered stills the shot moves through).
- **Video continuation (v2v)** — feed an existing clip and continue it without a cut; the original sets the motion, subjects, and look, and the prompt guides how the shot keeps unfolding.

## What a strong video prompt includes
- **Subject & action** — who/what moves, and exactly what happens.
- **Camera direction** — static, slow push-in, handheld follow, overhead drift, rapid pan.
- **Scene & atmosphere** — environment, lighting, weather, time of day, mood.
- **Motion qualities** — slow, abrupt, weightless, chaotic, precise, cinematic, documentary.
- **Continuity constraints** — what must stay stable across the clip (crucial for continuation).

## Short vs long prompts
A short prompt (`A red fox leaping through fresh snow, telephoto.`) hands framing, motion, and mood to the model — great for fast exploration and happy accidents. A long prompt lets you direct scene, camera, pacing, and audio — better for specific shots and a consistent look, but over-stuffing makes motion less coherent. Add camera, motion, and atmosphere only where they improve control.

## Prompt formats (pick by how much control the shot needs)
- **Natural-language one-liner** (the best default): one flowing sentence with a consistent shape so you can revise one part without touching the rest —
  `[camera] shot of [subject] [action] in [environment]. [supporting visual & motion details].`
- **Structured / labeled fields** — when you need tighter control, break it into explicit levers you can tweak in isolation: `Camera shot:` / `Subject + action:` / `Depth of field:` / `Lighting + palette:` / `Motion:` / `Style:`.
- **Timestep prompting** — for action that must land on time, write a short timeline; keep it to two or three beats for a ~5-second clip, and mark a hard cut where the angle changes:
  `0.0–1.5s — locked wide of a still harbor at dawn` · `1.5–3.0s — slow push-in as gulls lift off` · `3.0–5.0s — the sun breaks the horizon`.

## Multi-shot schema (for a look and story that must hold across shots)
Fill six elements with concrete nouns and verbs the camera can see, then assemble them:
1. **Core summary** — one line stating the whole sequence (who, where, the arc), so every later choice has context.
2. **Scene** — per shot: setting, light quality, depth of field.
3. **Subject description** — a fixed description repeated identically across shots, so identity stays consistent.
4. **Dynamic narrative** — per shot, timecoded (`Shot 2 [2.5s–5.0s]: …`): the camera move and the subject's action. Camera language lives here.
5. **Audio** — per shot: the soundscape, rendered synchronized to the frames.
6. **Style & color** — the global look tying the shots together: realism level, palette anchors, grain.

The schema is one option, not a requirement — reach for it only when a multi-shot look and story has to hold together; use a one-liner, labeled fields, or timesteps otherwise.

## Image-to-video specifics
All i2v runs through one ordered set of pinned frames:
- **Startframe (one image):** the exact opening frame; the prompt animates forward. The most literal way to bring a single photo or render to life — first-frame fidelity is preserved exactly.
- **Start + end frame (two images):** the first and last frame; FLUX fills the motion between. Use when both ends matter (a reveal that resolves on a set composition, a defined before/after, a loop). Keep the two frames related (same subject/scene/camera) so the path is plausible; the wider the gap, the more unpredictable.
- **Keyframes (three or more, or `[seconds, image]` pairs):** ordered waypoints the shot passes through in turn, spread evenly or pinned to exact timestamps. Order is read as a timeline; keep the look consistent across frames so it reads as one take. Timestamped or 3+ keyframe shots need an explicit duration.

## Video continuation
The source clip sets motion, subjects, and look; describe how the shot keeps unfolding without a cut, and state what must remain stable.

## Audio & speech
FLUX renders audio with the video — a scene that clearly implies sound may be enough, but when sound matters, describe it as part of the shot. Four layers you can name (you don't need all four):
- **Speech** — who speaks, the exact words (in quotes), and how they say it.
- **Ambience** — the sound of the place (name specific sources: "rain against a metal awning" beats "moody ambience").
- **Effects** — sounds tied to visible actions ("the mug clicks against the saucer").
- **Music** — style, pace, and where it sits in the mix ("a sparse piano cue under the scene, low in the mix").

**Dialogue.** Put the exact words in quotes and name who delivers them. Give a visible speaker a face to lip-sync, or explicitly call an off-screen line a **voiceover** — otherwise a quoted line may render as on-screen text. When you don't want captions, add "no on-screen text, no subtitles."

**Direct the speaker** with concrete anchors instead of "professional/warm/engaging" (which all produce the same polished read): person (age/accent when it matters), register (low, bright, rough…), recording (close and dry, across a room, phone mic, PA), delivery (lightly amused, hesitant, practical), and a guardrail ("no announcer delivery, no sales voice"). Use only the details that change the read — stacked personality adjectives fight each other.

**Write sayable dialogue** — read it aloud first: use contractions, cut setup the viewer can already see, avoid a slogan at the end of every line, give the speaker a reason to say it to someone, keep punctuation simple. **Leave room for the line** — a short line in a longer clip is safer; if the last word cuts off, shorten it or lengthen the clip. Don't force several speakers and a long script into a short clip.

**Languages & accents.** FLUX speaks many languages and can switch within one performance. Label each language beside its line, keep the intended order, and say the same speaker continues across a switch. Provide dialogue in native script, romanized, or as a plain-language instruction naming the target language; treat an accent as part of a character (pair it with pace, projection, emotion, and who they're speaking to). To reuse a voice across clips, repeat the full voice direction and change only the script — treat it as casting direction, not a guaranteed identical performer.

## Camera language
Reach for real cinematography terms — the doc's reference vocabulary you can drop straight into prompts:
- **Shot size:** macro, extreme close-up, close-up, medium, cowboy, full, wide, establishing, two-shot.
- **Angle:** eye level, low, high, aerial, bird's-eye top-down, worm's-eye, over-the-shoulder, Dutch, POV, profile.
- **Composition:** leading lines, center framing, rule of thirds, symmetry, negative space, frame-within-frame, foreground occlusion, silhouette, reflection.
- **Movement:** pan, tilt, dolly in, tracking, orbit/arc, crane/boom, pedestal, trucking, handheld, Steadicam, whip pan, dolly zoom, push-through, locked-on.
- **Focus & optics:** shallow/deep focus, rack focus, split diopter, tilt-shift; wide-angle, telephoto compression, fisheye, macro, anamorphic flares, halation, vignette.
- **Time:** slow motion, speed ramp, timelapse, long-exposure trails, bullet time, freeze frame, fast motion, cinemagraph.
- **Lighting:** rim, chiaroscuro, golden hour, neon practicals, volumetric/god rays, hard noir light, haze, spotlight.
- **Transitions:** match cut, whip transition, foreground wipe, jump cut, object portal, pass-through, quick cuts.
- **Format:** 21:9 cinemascope, 9:16 vertical, 4:3 vintage, split screen — plus VFX (double exposure, morphing, kaleidoscope, datamosh) and looks (stop-motion, pixel art, kinetic typography) when you want them.

**The rule that matters:** start with **one framing term, one movement term, and one clear subject action**. Stacking many camera instructions in a single sentence makes the shot less readable — lead with the subject and action, then add the camera language that earns its place.

## Iterate
The first prompt is a starting point, not the final one. Review each result and refine — add context, remove ambiguity, shift the emphasis, or change direction. Small adjustments move the result a lot.
