# ByteDance Seedream — Prompt Guide

Seedream is ByteDance's image model family (4.0 → 4.5 → 5.0-lite). It generates natively high-resolution images and follows natural-language prompts for text-to-image, reference-based generation, and multi-image work. Compared with the older 3.0, the newer versions understand prompts more strongly — they reach the intended image from *less* description and no longer wash out — so **concise, precise prose beats stacking ornate vocabulary.** Write the prompt as a coherent sentence or two, not a comma-salad of keywords. Prompting is fully bilingual: English and Chinese are both first-class, and on-image text can be requested in many languages.

## Prompt structure
The maker's core recipe is one flowing natural-language description of **subject + action + environment**, with style cues added only when aesthetics matter:

1. **Subject** — who/what, described concretely (age, clothing, expression, material).
2. **Action / pose** — what the subject is doing.
3. **Environment** — the scene and setting.
4. **Aesthetic layer (optional)** — style, color, lighting, composition, camera. Add these when the look matters; skip them when it doesn't.

**Formula:** `[Subject] + [Action] + [Environment] (+ [Style / color / lighting / composition])`

Write it as prose, not a tag list:
> Recommended: "A girl in a lavish dress walking under a parasol along a tree-lined path, in the style of a Monet oil painting."
> Avoid: "Girl, umbrella, tree-lined street, oil painting texture."

For complex scenes, describe every element thoroughly — Seedream renders dense, multi-object compositions faithfully when each element (and its relationship to the others) is spelled out, so a longer, well-organized paragraph is productive here. Keep the whole prompt under roughly 600 words; past that, information scatters and the model starts dropping details.

## Guiding principles
- **Concise over ornate** — say what you want plainly; repeating grand adjectives ("beautiful", "masterpiece", "ultra high quality") does less than one precise clause.
- **State the purpose** — if the image has a job, name it. Say "Design a logo for a gaming company…" or "Create an infographic showing…", not just "an abstract image of…". Declaring the image type and use case sharpens the result.
- **Frame positively** — describe what should be present rather than listing what to exclude.
- **Describe relationships, not just objects** — for multi-element scenes, spell out how things sit together (position, foreground/background, who does what) so nothing gets dropped.
- **Use technical terms for factual visuals** — for formulas, diagrams, or educational illustrations, use precise terminology and name the desired layout, format, and style; the model turns knowledge into high-density visual content but needs the exact concepts stated.

## Composition, camera & lighting
Add cinematographic detail in the aesthetic layer when the look matters: name the shot (medium full shot, extreme close-up, wide-angle), the lens and depth of field (shallow depth of field, sharp focus on the eyes), the lighting source and quality (dramatic studio lighting, soft side-backlighting, warm interior light against cold exterior), and a color/genre reference (editorial magazine-cover aesthetic, cinematic sci-fi palette). You can also request an aspect ratio or image shape in plain language inside the prompt ("a 3:2 poster", "a tall portrait") and let the model map it.

## Style & materiality
Name styles and materials precisely rather than gesturing at them: "picture-book style", "children's book illustration", "felt wool figure", "transparent clear glass instead of silver metal". A specific style keyword (or a reference image, when available) lands far better than a vague "artistic" or "stylish".

## Text rendering
Seedream renders on-image text, and 4.5 markedly improved it — more accurate spelling, multi-line layouts, and varied font styles.

- **Quote the words** — put the exact string in **double quotation marks** so it's treated as literal.
  > Recommended: `Generate a poster with the title "Seedream 4.5".`
  > Avoid: `Generate a poster titled Seedream 4.5.`
- **Keep strings short** — a few words render most reliably; long paragraphs or dense text layouts come out inconsistent.
- **Say where and how** — describe placement ("title centered at the top") and typography ("bold sans-serif", "elegant script") as part of the same sentence.
- **Decide the wording first** — lock the exact final text before generating; the model sets what you quote, not what it infers.
- **Multilingual text** — on-image text works across many languages (the newest generation adds native rendering for Russian, Arabic, Thai, Turkish, Korean, Malay, Spanish, Portuguese, Indonesian, French, German, Vietnamese, Japanese, and more); write the prompt in EN or CN and quote the target-language string you want drawn.

## Reference-based prompts
When you supply a reference, split the prompt into two explicit halves so the model knows what to keep versus what to invent:

- **Reference target** — name exactly what to extract and preserve from the reference (character identity, artistic style, product material, layout).
- **Generated scene** — describe the new scene, layout, and specifics you want built around it.

For multiple references, label each one by index and give it a job: "Replace the subject in Image 1 with the subject from Image 2, and render it in the style of Image 3." When turning a sketch, wireframe, or floor plan into a finished image, supply a clean source, state the main subject and fidelity ("a high-fidelity UI", "a photorealistic living room"), and pin the consistencies that must match the reference (furniture placement, spatial layout) while telling it to drop the sketch lines.

## Editing prompts
For edits (add / remove / replace / modify), use concise, unambiguous instructions that name the exact target and the exact change — avoid vague pronouns like "that one". If other elements must stay put, say so explicitly.
> Recommended: "Dress the tallest panda in a pink Peking Opera costume and headgear, keeping its pose unchanged."
> Avoid: "Put that one in pink clothes."

Change one thing at a time rather than piling several edits into a single instruction, and quote any text you're replacing: `Change "Old Text" to "New Text" while preserving the font, color, and styling.`

## Series & consistency
Seedream can produce a coherent set of images that hold character continuity and a unified style — good for storyboards, comics, icon sets, brand kits, or emoji packs. Trigger a series by asking for one in plain language: "a series", "a set", or by stating the number of frames, then describe each frame or the through-line that unifies them.

## Resolution
Seedream outputs at native high resolution and optimizes differently at higher settings, so request the resolution that fits the job rather than upscaling afterward. Reach for the higher tiers for hero images and for anything where fine text or fine detail must stay crisp — more pixels give letterforms and textures room to hold.

## Examples
- **Dense scene (t2i):** "A cluttered office desk: an open laptop showing green code, a mug reading \"Developer\" with steam rising, an open book showing a gray/blue/green Venn diagram, a sticky note with a three-level mind map, a fountain pen with its cap beside it, a phone showing a new-message notification, a small succulent in the corner, a blurred bookshelf behind, sunlight from the right casting shadows across the desk."
- **Purpose-stated logo:** "Design a logo for a gaming company. The logo features a dog playing with a game controller. The company name \"PITBULL\" is written on it."
- **Editorial portrait:** "Vibrant close-up editorial portrait, model with a piercing gaze wearing a sculptural hat, rich color blocking, sharp focus on the eyes, shallow depth of field, Vogue-cover aesthetic, medium format, dramatic studio lighting."
- **Reference figure:** "Based on the character in the reference image, create an anime figure on a desk; behind it a birthday gift box printed with the character's image, a book beneath it, and a round base in front for the figure to stand on. Indoor, photorealistic, cinematic feel; keep the overall style consistent with the reference."
- **Series:** "Generate four film storyboard frames: astronauts repairing a spacecraft, a sudden asteroid-belt attack, an emergency evasive maneuver, and a narrow injured return — one cohesive cinematic sci-fi style across all four."
