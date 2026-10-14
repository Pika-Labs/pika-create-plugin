# OpenAI GPT Image 2 — Prompt Guide

GPT Image 2 generates and edits images from natural-language prompts. It accepts a wide range of prompt styles — minimal one-liners, descriptive paragraphs, JSON-like structures, instruction-style, and tag-based — so the winning move is a clear, skimmable template rather than clever syntax. It is strongest at precise, canvas-anchored editing (change one thing, keep everything else), at rendering literal text, and at photorealism when you ask for it directly.

## Prompt structure
Write prompts in a consistent order:

**background/scene → subject → key details → constraints**

- **State the intended use** — naming the deliverable (ad, UI mock, infographic) sets the "mode" and level of polish.
- **Break up complex requests** — use short labeled segments or line breaks instead of one long paragraph.
- **Prioritize a skimmable template** over clever prompt syntax; minimal prompts, descriptive paragraphs, JSON-like structures, and tag-based prompts can all work well.
- **Iterate in small steps** — start from a clean base prompt and refine with single-change follow-ups; long prompts can work, but debugging is easier when each change is isolated.

## Photorealism
- Put the word **"photorealistic"** directly in the prompt to strongly engage the model's photorealistic mode.
- Use **photography language** — lens, lighting, framing — and explicitly ask for **real texture**.
- Prompt the model **as if a real photo is being captured in the moment**.

## Specificity & style
- Be concrete about **materials, shapes, textures, and the visual medium** (photo, watercolor, 3D render).
- Add **quality levers only when needed** — film grain, textured brushstrokes, macro detail — rather than stacking them by default.

## Text in images
- Put literal text in **quotes or ALL CAPS**.
- Specify **typography as constraints** — font style, size, color, placement.
- For difficult words, **spell them out letter-by-letter** to improve character accuracy.
- Text placement and clarity are improved but still imperfect; for **small text, dense information panels, and multi-font layouts**, favor higher quality and compare before shipping.

## Editing
Surgical, preserving edits are a core strength.

- Use **"change only X"** plus **"keep everything else the same,"** and repeat the preserve list on every iteration.
- **State exclusions and invariants explicitly** — e.g. "no watermark," "no extra text," "no logos/trademarks."
- If the edit should be surgical, also say **not to alter** saturation, contrast, layout, arrows, labels, camera angle, or surrounding objects.
- **Masking is prompt-based guidance** — the model uses the mask as a hint and may not follow its exact shape precisely; transparent areas mark the region to edit, and the image and mask must share format and size.

## Multi-image references
- **Reference each input by index and description** — "Image 1: product photo… Image 2: style reference…".
- **Describe how they interact** — "apply Image 2's style to Image 1."
- For compositing, be explicit about **which elements move where** — "put the bird from Image 1 on the elephant in Image 2."

## Known limits to prompt around
- Placing elements precisely in **structured or layout-sensitive compositions** can be difficult.
- Maintaining visual consistency for **recurring characters or brand elements** may need reinforcement across iterations.
- All prompts and generated images are filtered in accordance with the content policy.

## Examples
- **Photorealistic capture:** lead with "photorealistic," name the lens/lighting/framing, and ask for real texture — as if a photo were taken in the moment.
- **Surgical edit:** "change only the man's tie to green; keep everything else the same — do not alter the pose, background, camera angle, saturation, or layout."
- **Text poster:** render the headline "URBAN EXPLORER" in bold white sans-serif, top-center, at higher quality for crisp small type.
- **Composite from references:** "Image 1: product photo. Image 2: style reference. Apply Image 2's style to Image 1."
