---
name: prompt-image
description: Use when writing or improving the prompt for a Pika image run — create, edit or restyle an image — before running it. Routes each model to its maker's own prompt guide.
---

# Image prompts

Each image model has its own idea of a good prompt. Find the model below, read its guide in `references/`, and write the prompt the way that guide describes. If you switch models, switch guides.

## Model guides

| Model (`create_image`, `edit_image`) | Guide |
| --- | --- |
| `gpt-image-2` | `references/openai-gpt-image-2.md` |
| `nano-banana` (default), `nano-banana-edit`, `nano-banana-2`, `nano-banana-2.1`, `nano-banana-pro` | `references/google-gemini-image.md` |
| `seedream-5-lite`, `seedream-5-pro`, `seedream-4` | `references/bytedance-seedream.md` |
| `grok-imagine`, `grok-imagine-quality` | `references/xai-grok-imagine.md` (image sections) |

Models without a guide here (`ideogram-4`, `ideogram-45`) follow the defaults below.

## In Pika

- The prompt goes in the tool's `prompt` field (`instructions` in `edit_image`). A template or preset field may replace it; send one or the other.
- Keep the user's intent and words. Expand a described look into the concrete detail the guide asks for; don't swap in a different idea.
- Aspect ratio, resolution, quality, transparent background and output format are fields. Keep them out of the prompt.
- References go in `image_urls` (`reference_urls` in `edit_image`); name them in that order ("image 1", "image 2") and give each one a job.
- A guide may mention a control the tool doesn't expose, such as a negative prompt or a seed. Restate a negative as the wanted result inside the prompt, or leave it out.

## Defaults when a guide is silent

- Write prose, not keyword lists, and leave out empty praise ("stunning, masterpiece, 8K").
- Describe what you want, not what to avoid ("an empty street", not "no cars").
- Be concrete: subject, composition, light, style, materials.
- Put on-image text in quotes, with its placement and lettering.
- For edits, name the one change and list what stays: face, pose, product shape, label, background, camera angle. Make one change per run.
