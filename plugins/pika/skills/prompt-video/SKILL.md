---
name: prompt-video
description: Use when writing or improving the prompt for a Pika video run — text-to-video, image-to-video, references, a multi-shot video or a video edit — before running it. Routes each model to its maker's own prompt guide.
---

# Video prompts

Each video model has its own idea of a good prompt. Find the model below, read its guide in `references/`, and write the prompt the way that guide describes. If you switch models, switch guides.

## Model guides

| Model (`create_video`) | Guide |
| --- | --- |
| `seedance-25` | `references/bytedance-seedance-2.5.md` |
| `seedance`, `seedance-mini` | `references/bytedance-seedance-2.0.md` |
| `minimax-h3` | `references/minimax-h3.md` |
| `kling` | `references/kling-v3.md` |
| `veo`, `veo-fast` | `references/google-veo-3.1.md` |
| `gemini-omni` | `references/google-gemini-omni-1.1-flash.md` |
| `flux-3` | `references/black-forest-labs-flux-3-video.md` |
| `grok`, `grok-15` | `references/xai-grok-imagine.md` (video sections) |
| `wan-3` | `references/alibaba-wan-3.0.md` |
| `pika` | `references/pika-2.5.md` |

Apps that render on Seedance 2.5 (`product_ad`, `podcast_creator` and `swap-anything`) use its guide wherever they take free text for the video.

## In Pika

- The prompt goes in the tool's `prompt` field or the preset's `prompt` slot. Some apps build the prompt from other fields; fill those instead.
- Keep the user's intent and words. Expand a described look ("more cinematic", "like a perfume ad") into the concrete craft the guide asks for; don't invent a different idea.
- References are named by kind and position — `@image1`, `@video1`, `@audio1` — in the order of `image_urls`, `video_urls`, `audio_urls`. Where a guide says "the first image" or "Image 1", use these handles.
- Duration, aspect ratio, resolution and audio on/off are fields, and their descriptions give each model's limits. Keep them out of the prompt.
- A guide may mention a control the tool doesn't expose, such as a negative prompt or a seed. Restate a negative as the wanted result inside the prompt, or leave it out.
- `minimax-h3`: send a first frame (`image_url`, optional `end_image_url`) or a reference set (`image_urls`, `video_urls`, `audio_urls`), not both. Reference audio needs an image or clip alongside it.
- Multi-shot (`seedance-25`, up to 30 s): one line per shot, timecoded and consecutive, each with its own framing, action and end point, ending in "Hard cut.": `Shot 1 (0–6 s): … Hard cut.` One camera move per shot. Describe each character, product and place identically in every shot.

## Defaults when a guide is silent

- Write prose, not keyword lists.
- Describe what you want in frame, not what to avoid ("steady camera", not "no shake").
- Be concrete: subject, action, setting, camera, light, style; add audio where the model renders it.
- For image-to-video and edits, describe only what moves or changes, and name what must stay the same.
- Fit the action to the duration: a 5 s clip holds one beat.
- Put dialogue in the format the model's guide expects.
