# Google Gemini Omni 1.1 Flash — Prompt Guide

Gemini Omni Flash generates and edits video by instruction: describe what you want, or connect a clip and name the change, and the model applies it while preserving everything else. Two registers apply — for generation, write prompts with details like scene description, camera movement, lighting and mood; for editing, keep prompts simple, because overly descriptive edit prompts lead to unintended changes.

## Prompt structure
For generation, include scene description, camera movement, lighting and mood for best results.

For editing, state only the change:
- "Make this video anime"
- "Put a fashionable hat on this person"
- "Change the lighting to be more dramatic"
- "Change the text on the sign to say 'Omni Flash'"

Add "Keep everything else the same" to hold visual consistency when targeting one element:
- "Add a cat that jumps onto his lap, he begins to pet it. Keep everything else the same."
- "Make the phone invisible. Keep everything else the same."

## Single scene
The model may cut between shots unless you prompt for a single scene explicitly:
- "In a single unbroken scene"
- "In a single continuous shot"
- "No scene cuts"

> "Continuous, unbroken handheld shot of a fluffy tabby cat sitting on a sunny windowsill, looking out into a leafy garden. The cat's tail twitches slowly, and its ears rotate slightly toward ambient noises. Sunbeams illuminate dust motes in the air. Sound design: Gentle breeze, distant bird chirps. No dialogue."

## Negative prompts
If the generated video contains things you don't want, include simple negative prompts inside the regular prompt to avoid them: "No dialogue", "No embellishments", "No extra sound effects".

## Image-to-video
Use high-resolution images and provide specific motion descriptions. Vague prompts like "make it move" produce less compelling results than detailed descriptions of the camera movement, subject motion, and environmental effects.

## Audio & music
The model generates appropriate audio by default. Describe the type of audio you want in the prompt — this is especially important if you want music:
- "Include calm background music"
- "The video has a high energy techno beat"
- "The audio is a low tinny radio broadcast in the background, playing a song"

Voice editing and uploaded audio references are unsupported.

## Timing events
Direct when things happen in natural language:
- "After 3 seconds, a woman enters the scene."
- "At 5s the chorus starts in the background audio."
- "Every 2s cut to a new frame."
- "In a rapid fire sequence, every half a second change the scene."

Or use timecode syntax, one beat per line:

```
[0-3s] A person is walking
[3-6s] They stop and turn around
[6-10s] They start running
```

## Text in video
You can prompt to include text in your video and Omni will render it correctly and readably. Specify what street signs, storefronts, or license plates should say, and describe how text should animate on screen:
- "One word on the screen at a time: 'did, you, know, that, Omni, can, do, awesome, text?'"

## Meta prompting
Ask for general qualities rather than enumerating them yourself:
- "Consider micro-detail, expression and timing to create richness"
- "Be extremely detailed in descriptions of characters and environments"
- "Include plenty of appropriate detail in background elements"
- "Make a rapid fire video that shows a different rare [thing] every 1s"

## Extending video
Extend a clip with a simple instruction — "Extend this video", "The scene continues" — in 10-second increments up to 40 seconds total. In extension prompts:

- Describe audio changes explicitly, e.g. "The music continues into the chorus".
- Say whether the scene continues or cuts to a new scene; "Show the same characters in the next scene" carries the cast forward.
- Timestamps restart at 0s for the extended section.
- You can include reference images or videos to introduce new elements.

## Media role tags
When passing images or videos alongside the prompt, tag each one's role. Simple tags (recommended):

- `<FIRST_FRAME>` — starting frame
- `<LAST_FRAME>` — final frame (must be used together with `<FIRST_FRAME>`)
- `<IMAGE_REF_N>` — reference image
- `<VIDEO_REF_N>` — reference video

> `<FIRST_FRAME> <LAST_FRAME> a woman is walking`

For multiple media, use explicit source/reference declarations:

- `[# Sources <FIRST_FRAME>@Image1]`
- `[# Sources <FIRST_FRAME>@Image1 <LAST_FRAME>@Image2]`
- `[# References <IMAGE_REF_0>@Image1]`
- `[# References <VIDEO_REF_0>@Video1]`

> `[# Sources <FIRST_FRAME>@Image1] [# References <IMAGE_REF_0>@Image2] a woman <IMAGE_REF_0> is walking...`

You can pair tags with guiding instructions such as "Use this image as the starting frame." or "Use the given image(s) as references for video generation."

## Examples
- **Single-scene generation:** the continuous handheld tabby-cat windowsill shot above — camera style, subject micro-motion, light, sound design, and "No dialogue" in one prompt.
- **Simple motion:** "A marble rolling fast on a chain reaction style track, continuous smooth shot."
- **Timecoded multi-reference sequence:** "[0-3s] A studio fashion sequence. Starting with woman <IMAGE_REF_0>, she is holding <IMAGE_REF_1> [3-6s] Then we see the man <IMAGE_REF_2> holding <IMAGE_REF_3> [6-10s] And finally another woman <IMAGE_REF_4> who is holding <IMAGE_REF_5> while walking."
- **Instruction edits:** "Make this video anime" · "Change the text on the sign to say 'Omni Flash'" · "Make the phone invisible. Keep everything else the same."
