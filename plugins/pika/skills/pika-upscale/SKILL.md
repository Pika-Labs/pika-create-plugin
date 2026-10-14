---
name: pika-upscale
description: Use when the user wants a photo or video sharper or at higher resolution — upscale, enhance, 4K, print size.
---

# Upscale

1. Open `show_presets {app: "upscale"}`, with the photo or clip in `inputs` when you have it (an earlier output url, an earlier upload from `list_jobs {filter: "uploads"}`, or leave it out and the preset form takes the upload; where there is no card, `upload_file` for a chat attachment or `prepare_upload`). It reads a photo or a clip from the media itself.
2. Say in one line what you're running, then call `create_from_preset` with a fresh `request_id` and no `max_credits` and follow the quote's `next` (it applies the user's approval mode). Your line sits above the card, whose Create is the user's yes: don't ask for a yes or restate the price after it. The card runs the user's Create, edits and Take it further itself; once it reports a started job, don't call the tool again — use `get_job`. With no card, on a yes call it again with the same input, `request_id` and the agreed `max_credits`.
