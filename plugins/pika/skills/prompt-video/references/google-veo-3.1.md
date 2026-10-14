# Google Veo 3.1 — Prompt Guide

Google's Veo 3.1 generates video together with synchronized, spatially coherent audio — dialogue, sound effects, and ambient soundscapes — in a single pass. Prompt it the way a director briefs a shot, not the way you'd describe a finished scene: name the camera, the subject, and the action explicitly, then layer in context, style, and sound. Start with a simple prompt and add requirements incrementally; a lean, directed prompt often produces a better base than an overloaded one.

## Prompt structure
Google frames a strong prompt around five core elements:

1. **Subject** — the primary object, person, animal, or scene.
2. **Action** — what the subject is doing.
3. **Style** — creative direction keywords ("sci-fi", "film noir", a named animation style).
4. **Camera & composition** — the shot and any camera move ("aerial view", "close-up", "dolly shot").
5. **Ambiance** — color and lighting ("blue tones", "warm sunlight", "night").

Optional: focus and lens notes ("shallow focus", "macro lens").

**Cinematography-led formula:** `[Cinematography] + [Subject] + [Action] + [Context] + [Style & ambiance]`
> "Medium shot, a tired corporate worker, rubbing his temples in exhaustion, in front of a bulky 1980s computer in a cluttered office late at night. The scene is lit by the harsh fluorescent overhead lights and the green glow of the monochrome monitor. Retro aesthetic, shot as if on 1980s color film, slightly grainy."

You don't need every element every time. The strongest prompts break the shot into subject, action, scene/context, camera, visual style, audio, and negative prompt — but reach for only what the shot needs. Prompt like you're directing a shot, not just describing a scene.

## Camera, composition & lens
State camera motion explicitly — Veo won't infer a move you don't ask for.

- **Camera movement** — dolly shot, tracking shot, crane shot, aerial view, slow pan, POV shot, tracking drone view, worm's eye view.
- **Composition** — wide shot, close-up, extreme close-up, low angle, top-down shot, eye-level, two-shot.
- **Lens & focus** — shallow depth of field, wide-angle lens, soft focus, macro lens, deep focus.

Use adjectives and adverbs to paint a clear picture, and use "portrait" when the shot centers on a face. More descriptive detail yields a more refined result.

## Style & ambiance
Direct the aesthetic, mood, and lighting together — color palette, film stock, era, and light source, e.g. "shot as if on 1980s color film, slightly grainy" or "harsh fluorescent overhead lights and the green glow of the monochrome monitor."

## Audio, dialogue & sound
Veo 3.1 generates realistic, synchronized sound — including multi-person conversations and precisely timed sound effects — and the audio responds to on-screen events. Give each layer its own line:

- **Dialogue** — attribute the line to a speaker and give the exact words. Google's docs wrap speech in quotation marks (e.g. `A woman says, "We have to leave now."`), which targets speech and lip-sync cleanly. Note that showing the model written text can cause it to render that text on screen; when a clean frame matters more than tight lip-sync, write the colon form instead (`A woman says: We have to leave now.`) and add `(no subtitles, no captions, no on-screen text)`. Placing dialogue at the start of the prompt, before the visual description, further reduces caption burn-in. No single method is bulletproof — stacking them is the most reliable.
- **Sound effects** — describe them with clarity, e.g. `SFX: thunder cracks in the distance` or "tires screeching loudly, engine roaring".
- **Ambient** — define the background soundscape, e.g. `Ambient noise: the quiet hum of a starship bridge` or "a faint, eerie hum resonates in the background".

## Negative prompts
Refine output by describing what you want the scene to be, not by listing what to omit. Prefer "a desolate landscape with no buildings or roads" over "no man-made structures" — frame the exclusion as a positive description of the empty scene.

## Character & scene consistency
- **Reference images** — provide reference images of a scene, character, object, or style to hold a consistent look across multiple shots; this now includes audio generation. Veo preserves the referenced subject's appearance in the output.
- **First & last frame** — supply a start image and an end image to generate a natural transition between them, complete with audio.
- **Copy the description** — to keep a character consistent across scenes, copy and paste the entire, unchanged character description into every new prompt, modifying only the parts that describe the new action or setting.

## Timestamp prompting (multi-shot in one clip)
For a sequence of beats inside a single generation, tag each shot with a time range and direct it as its own shot — its own camera, action, emotion, and audio cues:

```
[00:00-00:02] Medium shot from behind a young female explorer with a leather satchel and messy brown hair in a ponytail, as she pushes aside a large jungle vine to reveal a hidden path.
[00:02-00:04] Reverse shot of the explorer's freckled face, her expression filled with awe as she gazes upon ancient, moss-covered ruins in the background. SFX: The rustle of dense leaves, distant exotic bird calls.
[00:04-00:06] Tracking shot following the explorer as she steps into the clearing and runs her hand over the intricate carvings on a crumbling stone wall. Emotion: Wonder and reverence.
[00:06-00:08] Wide, high-angle crane shot, revealing the lone explorer standing small in the center of the vast, forgotten temple complex, half-swallowed by the jungle. SFX: A swelling, gentle orchestral score begins to play.
```

## Examples
- **Retro office (five-part formula):** a medium shot of a tired 1980s corporate worker rubbing his temples at a bulky monochrome computer in a cluttered office late at night, lit by harsh fluorescents and the green monitor glow, shot as if on grainy 1980s color film.
- **Directed dialogue, clean frame:** a woman at a doorway — `A woman says: We have to leave now.` — with ambient rain, using the colon form to keep the frame free of burned-in captions.
- **Timestamped adventure sequence:** a four-beat jungle-explorer shot moving from a vine-push reveal, to an awe reaction close-up, to a tracking carving shot, to a wide crane reveal of the temple — each beat with its own camera, emotion, and SFX.
