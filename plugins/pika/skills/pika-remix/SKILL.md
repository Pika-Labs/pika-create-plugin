---
name: pika-remix
description: Use when the user wants to continue from an earlier Pika result — redo, vary, edit, extend, upscale, animate or score something Pika already made.
---

# Continue from an earlier result

1. **Find the result.**
   - Made in this conversation: use its `job_id` and `outputs[].url`.
   - @-mentioned as `pika://creation/<id>`: read that resource for its outputs.
   - Made earlier or elsewhere: call `show_upload` with `source: "creations"`, or `show_creations` and read the pick with `get_panel`, or `list_jobs` when the user names it clearly enough to find without a gallery. Something they uploaded to Pika before: `list_jobs {filter: "uploads"}`, or `show_creations {filter: "uploads"}` to let them pick.
2. **Pick the tool.** Redo or vary → the same tool or preset with a changed `prompt`; edit an image → `edit_image`; animate an image → `create_video`; longer video → `extend-video`; sharper → `upscale`; new lighting → `relight-media`; new outfit or object → `swap-anything`; music → `create_audio` with `model: "pika/pika-audio/pika-soundtrack"`. These apps run as presets (see `pika-create`).
3. **Pass the result as media.** Put the earlier output's URL in the field or slot that takes that media. Keep the settings the user didn't ask to change.
4. Say in one line what you're running, then call it with the input and a fresh `request_id` and no `max_credits` and follow the quote's `next` (it applies the user's approval mode). Your line sits above the card, whose Create is the user's yes: don't ask for a yes or restate the price after it. The card runs the user's Create, edits and Take it further itself; once it reports a started job, don't call the tool again — use `get_job`. With no card, on a yes call it again with the same input, `request_id` and the agreed `max_credits`. If the original was part of a project, pass the same `project_id`.
