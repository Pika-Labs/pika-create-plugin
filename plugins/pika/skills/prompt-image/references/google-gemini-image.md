# Google Gemini 3 Image (Nano Banana) — Prompt Guide

Google's Gemini 3 image models generate and edit images from natural-language prompts. They "think" through the prompt before rendering — reasoning about light, proportion, and text placement first — which makes them strong at long/complex text rendering, multi-image reference fusion, and multi-character consistency. Write prompts as confident narrative prose, not keyword lists.

## Prompt structure
Google's five essential elements, plus editing intent:

1. **Subject** — be specific (e.g. "a stoic robot barista with glowing blue optics").
2. **Composition** — frame the shot (extreme close-up, wide shot, low angle).
3. **Action** — what is happening (e.g. "brewing a cup of coffee, casting a magical spell").
4. **Location** — the scene and setting details.
5. **Style** — the overall aesthetic (3D animation, film noir, watercolor).
6. **Editing instruction** (when editing) — be direct and specific (e.g. "change the man's tie to green").

**Text-to-image formula:** `[Subject] + [Action] + [Location/context] + [Composition] + [Style]`
> "[Subject] A striking fashion model wearing a tailored brown dress, sleek boots, holding a structured handbag. [Action] Posing with a confident, statuesque stance, slightly turned. [Location] A seamless, deep cherry red studio backdrop. [Composition] Medium-full shot, center-framed. [Style] Fashion magazine editorial, shot on medium-format analog film, pronounced grain, high saturation, cinematic lighting."

**With reference images:** `[Reference images] + [Relationship instruction] + [New scenario]`
> "Using the attached napkin sketch as the structure and the attached fabric sample as the texture, transform this into a high-fidelity 3D armchair render. Place it in a sun-drenched, minimalist living room."

## Guiding principles
- **Be specific** — concrete detail on subject, lighting, and composition beats vague description.
- **Frame positively** — describe what you want, not what you don't ("an empty, deserted street" beats "no cars").
- **Control the camera** — use photographic and cinematic terms ("low angle", "aerial view", "wide-angle", "macro").
- **State the intent** — leading with "A photo of…" / "generate an image of…" keeps the model from replying in text.
- **Iterate conversationally** — refine with follow-up prompts rather than rewriting from scratch.

## Composition, camera & lighting
- **Lighting** — direct it like a cinematographer: "three-point softbox setup" for product; "chiaroscuro lighting with harsh, high contrast"; "golden-hour backlighting creating long shadows".
- **Lens** — "low-angle shot with shallow depth of field (f/1.8)"; wide-angle for scale; macro for fine detail.
- **Camera hardware** — evoke a look through the device: GoPro for immersive distorted action; Fujifilm for authentic color science; a cheap disposable camera for a raw nostalgic flash aesthetic.
- **Color grading / film stock** — "as if on 1980s color film, slightly grainy"; "cinematic color grading with muted teal tones".

## Style & materiality
Name materials precisely — don't ask for "a suit jacket", ask for "navy blue tweed"; "ornate elven plate armor, etched with silver-leaf patterns". Specific materiality drives realism.

## Text rendering
- **Quote the words** — enclose the exact text in quotes ("Happy Birthday", "URBAN EXPLORER").
- **Specify the type** — describe the typography or name a font ("bold, white, sans-serif font", "Century Gothic").
- **Localize** — write the prompt in one language and specify the target language for the on-image text.
- **Concept the text first** — the models render text best when you decide the exact final wording before asking for the image.

## Reference images
Clearly define the role of each input image, then refer to each by a short handle. Give every reference a job — structure, texture, character identity, location — so the model knows what to preserve from which image.

## Factual visuals
For diagrams, infographics, or data-driven images, ask for "scientifically accurate" or "historically accurate" results, and verify the output.

## Examples
- **Editorial fashion (t2i):** a fashion model in a tailored brown dress on a deep cherry-red seamless studio backdrop, medium-format film grain, editorial lighting.
- **Reference fusion:** a napkin-sketch (structure) + fabric swatch (texture) fused into a 3D armchair render in a sunlit minimalist room.
- **Character subject:** "a stoic robot barista with glowing blue optics" brewing a cup of coffee.
