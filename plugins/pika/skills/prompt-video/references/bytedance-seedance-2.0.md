# ByteDance Seedance 2.0 — Prompt Guide

Seedance 2.0 natively generates joint audio + video in a single pass and reads text, images, video, and audio references together. ByteDance frames it as a "multimodal AI director": internally it splits your instruction into a **spatial layer** (what is in the frame) and a **temporal layer** (how things change over time). So a good prompt is not descriptive copywriting — it's an engineering-style instruction that tells the model *who*, in *what scene*, doing *what action*, with *what camera move*, in *what order*. Multimodal references do the heavy lifting for identity, style, motion, and voice, which lowers how much you have to spell out in text.

## Prompt structure
For reference-driven work, pick a base formula by task type, then layer in the advanced formula for complex shots.

**Reference-based tasks — base patterns:**
- **Multimodal reference** (pull elements from assets into a brand-new video): `Reference <Subject_N> in <Image_N> to generate…` / `Reference <Action/Camera_movement/Style/Sound_effect> in <Video_N> to generate…` / `Reference the timbre in <Audio_N> to generate…`
- **Video editing** (modify an existing video; unmentioned parts stay unchanged): add = describe `<element features> + <timing> + <location>`; modify = `Strictly edit <Video_N>, change <original characteristic> to <new characteristic>`; delete = name the element to remove and re-state what must stay.
- **Video extension** (continue along time, keeping style/subject/narrative consistent): `Extend <Video_N> forward/backward to generate…`
- For edit/extend, refer to the clip directly as `<Video_N>` — do **not** say "reference <Video_N>", or the model mistakes it for a fresh reference task.

**Advanced formula (complex shots):**
> precise subject + action details + scene/environment + lighting & color tone + camera movement + visual style + image quality + constraints

Lock *who* is *doing what* first, then *where* and *what atmosphere*, then *how to shoot it*, and finally tighten with style, image quality, and constraints.

## 1 — Define the subject
When an image holds several subjects, bind the one you mean explicitly, or the model may grab the wrong element.
- Pattern: `Define [core subject features] in <Image_N> as <Subject_N>` — e.g. "Define the woman in a red dress and straw hat in Image 1 as Subject 1" (or give her a name, "…as Zhang Hong").
- Use **2–3 stable static features** (clothing, hairstyle, appearance, category) — enough to uniquely identify, no more.
- **Re-name on every mention.** For undefined subjects use `<Subject_N>@<Image_N>` each time ("Zhang San@Image 1"); for pre-defined subjects reuse the exact same label throughout ("police officer" vs "thief").
- Prefer expressing spatial relationships through the reference image rather than long text. Keep descriptions concise; avoid contradictory features for the same subject.

## 2 — Shot sequencing (storyboard the timeline)
Because space and time are decoupled internally, the ideal form for a complex video is a timeline storyboard: break it into shots and describe each in event order.
- Organize with `Shot 1 / Shot 2 / Shot 3`, primary action first, secondary later.
- Per shot, order the info as: **camera move / transition → subject action & expression → position or spatial change → audio.**
- Do **not** hard-pin per-shot durations. Precise timing (e.g. "0–3s") is unstable and can break generation; let the model pace the plot naturally.
- Negative: *"A man runs nervously down the street, very cinematic."* Positive: *"Shot 1: Side shot of an alley; the man starts running, breathing hard. Shot 2: he knocks over a fruit stand; camera shakes, close-up of his frightened face. Shot 3: he climbs a low wall and vanishes; camera pulls back and freezes on the empty street."*

## 3 — Action description
- **Refine by body part + quantify degree.** Specify hands, legs, head, shoulders, back, plus range/speed/force: "slowly raise a hand", "quickly turn the head", "slightly lower the head".
- **Prefer slow, gentle, continuous small movements.** Avoid high-burst large motion (sprinting, big jumps, violent rolls) — it destabilizes.
- **Bridge actions with inertia:** "use the inertia of turning around to naturally raise a hand" keeps motion coherent.
- **Externalize emotion as physical detail**, not abstract words. Instead of "very sad": *lowering the head, shoulders trembling slightly, eyes reddening, fingers clutching the corner of clothing, tears welling but not falling.* Same for joy (mouth corners rising, light steps, humming), anxiety (checking watch, tapping fingers, darting eyes), anger (clenched fists, tense jaw, words squeezed through gritted teeth).

## 4 — Camera movement
The model understands standard camera terms directly — "medium shot, close-up, wide shot, slow push-in, smooth lateral tracking, fixed shot". Use **one** camera move per shot; asking for push + pull + pan + track at once increases instability.

## 5 — Image quality, style & constraints
- **Image quality** — "HD, rich details, cinematic texture, natural colors, soft lighting".
- **Style** — set one overall tone: "cyberpunk cool blue-purple tone", "retro film", "fresh Japanese style". If the reference is realistic but you want anime, say so explicitly ("2D Japanese anime style", "3D Chinese-style comic"), or the video drifts back to live-action.
- **Constraints** — highly load-bearing for avoiding flaws: "keep it subtitle-free" / "avoid generating any text or subtitles"; "do not generate a logo"; "do not generate a watermark". To reduce spurious subtitles, prefer landscape output (portrait subtitles are more common).

## Native audio, dialogue & text
Seedance renders dialogue, ambience, SFX, and music jointly with the picture. Punctuation signals the audio type — keep dialogue in one language (no Chinese/English mixing except proper nouns):

| Type | Symbol | Example |
|---|---|---|
| Music | `（ ）` | （fast-paced rock music in the background） |
| Sound effect | `< >` | < a dog barking in the distance > |
| Dialogue | `{ }` | {Hello, world} — mark non-CN/EN: *says in Japanese {こんにちは}* |
| Subtitle | `【 】` | 【Chapter One: Departure】 |

- **On-screen text** works for slogans, subtitles, and speech bubbles. Formula: `[text] + [timing] + [position] + [entrance style], [color/font]`. Prefer common characters; avoid rare glyphs and special symbols.
- **Subtitles:** "Render as subtitles at the bottom-center, perfectly synchronized with the audio rhythm."
- **Speech bubbles:** `[Character] says "[line]." Speech bubbles appear around the character containing the spoken text.`
- **Voice reference:** describe the timbre in words alongside the audio ref — "use the low, thick, warm, finely grainy middle-aged male voice of @Audio 1 to say…".

## Reference roles & asset strategy
Give every asset one job. ByteDance groups assets into four functional roles: **character anchoring** (lock appearance), **scene tone-setting** (lock environment/style), **camera-movement reference** (lock shot language and rhythm), **rhythmic atmosphere** (audio locks emotion and timbre).
- **Use few references, not many.** Recommended total is ~4–5: 1–2 character images (a face close-up + a full body) + 1 scene image + 1 camera-move video + 1 audio clip. Overloading references makes the model unable to judge priority and causes style conflicts and blurry identity.
- **Order matters.** Upload assets in the sequence you want them applied; the more precisely an asset must be followed, the earlier it goes in the prompt.
- **Character identity:** a **headshot + full-body** pair is enough. A clean face-only headshot (no expression, minimal neck/shoulders/background) carries identity; the full body carries wardrobe and pose. Avoid multi-view/three-view character sheets — the model may read the angles as *different people*, worsening ID drift and spawning duplicates.
- **Reference role phrasing:** `<Subject 1> facial features → Image 1 (headshot), makeup and styling → Image 2 (full body)`.
- **Continuous take vs stitched cuts:** extend (one long take) suits single-scene dialogue and emotional progression for an immersive feel; stitching independent clips suits plot turns and fast action (chases, fights, montages). Production usually combines both.

## Reference-mapping patterns
- **Image / subject:** `Refer to / Extract / Combine / Use the [subject] from [Image N] to generate [scene], maintaining consistent [subject] features.`
- **Multi-element compositing:** name each element's source per clause — *"The scene is set in the restaurant from Image 4. The girl from Image 1, wearing the clothes from Image 2, organizes the counter. The boy from Image 3 approaches. The logo from Image 5 stays in the bottom-right throughout."*
- **Motion transfer:** `Refer to the [motion] from [Video N] to generate [scene], keeping the motion details consistent.`
- **Camera-motion transfer:** `Refer to the [camera movement] from [Video N] to generate [scene], keeping the scene consistent.` — a reference clip doesn't *describe* a move, it *contains* it.
- **Effects transfer:** `Refer to the [special-effects description] from [Video N] to generate [scene], keeping the effects consistent.` For finicky effects (e.g. a countdown), a reference video beats text.
- **Multi-panel / storyboard:** upload a panel sheet and instruct "present all frame compositions from Image 1 in strict predefined order", then describe the action that follows.
- **Editing verbs:** add = `At [timing] and [location] of [Video N], add [element].` remove = `Remove [element] from [Video N], keeping the rest unchanged.` modify = `Replace [element] in [Video N] with [element], preserving original motion and camera.`
- **Extension:** `Generate the content after/before [Video N]: [description]` — original frames aren't re-generated, so continuity holds.

## Worked example (dialogue-focused short)
Assets: `@Image 1` female-lead half-body; `@Image 2` dorm scene reference; `@Video 1` indoor dialogue camera move; `@Audio 1` room ambience.

> Use the girl in @Image 1 as the main character, @Image 2 as the dormitory scene reference, and refer to the camera movement in @Video 1.
> Shot 1: At dusk, girl @Image 1 walks briskly to the dorm entrance @Image 2. Camera follows steadily in a medium shot; warm sunlight spills through the window. She pauses at the doorway, takes a deep breath, looks slightly nervous.
> Shot 2: She pushes the door open and enters. Cut to an indoor medium shot. Roommates look up from their books; one smiles and asks {How did the exam go? Did you pass?}. Camera cuts slowly between half-body close-ups.
> Shot 3: She lowers her head, dejected (close-up), then raises it, can't hold back a smile, laughs and says {I was kidding}. The roommates chase and play-fight; camera pulls back and freezes on a wide shot of the laughing dorm.
> High-definition cinematic documentary style, warm tones, soft light. Face stable without deformation; motion natural and smooth. Ambient sound blends with @Audio 1.

## Other examples
- **Product 360 (multi-image):** "Use the cameras from Image 1, 2, 3. Replace the background with white, place them on a white table. Focus in close-up, then rotate 360° showing front, sides, and back of each."
- **Logo formation:** floating lanterns flood a neon-futurist sky and converge at frame center to form the logo from Reference Image 1, in a 3D cyberpunk style.
- **Effects transfer:** "Refer to the golden particle effects in Video 1, so that when the character in Image 1 plays the flute, the same particles surround their body."
