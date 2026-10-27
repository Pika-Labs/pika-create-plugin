---
name: pika-video
description: Use when the user wants a video with more than one shot — a film, story, trailer, montage, explainer or multi-scene ad.
---

# Multi-shot video

Seedance 2.5 renders up to 30 s with its own cuts from one timecoded prompt, so a multi-shot video is one `create_video` call per 30 s.

1. **Agree the shots.** With the user, settle each shot: what happens, the camera, and any lines. No stills are needed first. Use images only when the user brings them or asks for a look or recurring character: pass them in `image_urls` and refer to them as `@image1`, `@image2`… in that order.
2. **Write the prompt.** Follow `prompt-video` and its Seedance 2.5 guide: one prompt with a timecoded line per shot (`Shot 1 (0–6 s): … Hard cut.`). Describe each character, place and look the same way in every shot.
3. **Up to 30 s.** Say in one line what you're running, then call `create_video` with `model: "seedance-25"`, the prompt, `duration`, `aspect_ratio` and `resolution`, a fresh `request_id` and no `max_credits` and follow the quote's `next` (it applies the user's approval mode). Your line sits above the card, whose Create is the user's yes: don't ask for a yes or restate the price after it. The card runs the user's Create, edits and Take it further itself; once it reports a started job, don't call the tool again — use `get_job`. With no card, on a yes call it again with the same input, `request_id` and the agreed `max_credits`.
4. **Longer than 30 s.** Split it into consecutive parts of at most 30 s, each its own `create_video` call. Describe characters, places and look identically in every part, and pass the same reference image in each part for a recurring character or product. Quote every part, show the parts and one total, and get one yes the way the user's approval mode asks. Then run each part with its quoted `max_credits`, except a part the card reports as started: wait on that one with `get_job`.
5. **Show what is sent.** The quote card shows the exact prompt and settings under "Sent to the model", and the user can edit the prompt there. Where no card shows, show the user each call's full prompt and settings before asking.
6. **Assemble parts.** `create_project`, then `add_clips` with the parts in order on `v1`. To put the user's own file on the timeline, upload it (`upload_file` for a chat attachment, `prepare_upload` where you can run commands), `add_media` it into the project, then `add_clips` with the returned `source`. To score it, make music with `create_audio` (`pika/pika-audio/pika-soundtrack` scores a clip) and add it on `a2`. Titles, captions and shapes go over the video with `set_overlays`. Then `export_project`; `get_project` shows the export link.

Offer `create_audio` with `model: "pika/pika-audio/pika-soundtrack"` to score a single-call video, or `upscale` for a sharper cut.
