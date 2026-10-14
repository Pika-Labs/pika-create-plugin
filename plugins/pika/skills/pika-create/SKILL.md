---
name: pika-create
description: Use when the user asks Pika to make or edit an image, video, music, sound effect or voiceover and no more specific Pika skill fits.
---

# Make or edit media with Pika

1. **Go straight to the app.** Choose by the task, not the output type, and make its call first, before `get_account` or any listing:
   - a task in **Presets** below (headshot, photo effect, resize, swap, relight, color grade, product shot, camera move, talking head, extend, trim, upscale, motion transfer, World Cup, …) → `show_presets {app}` with the app its line names. That shows the user the app's choices, and its preset form collects their photo or clip, so don't call `show_upload` first; when they already gave you a photo or clip as a URL, pass it in `inputs` (`[{slot, value}]`) to prefill the form. When the user already gave everything, call `create_from_preset` with what you have;
   - an ad, podcast, character, voiceover, music or multi-shot video → `pika-ad`, `pika-podcast`, `pika-character`, `pika-speech`, `pika-audio` or `pika-video`;
   - anything else → `create_video` or `create_image`, which also fit when the user names a model (pass it as `model`).
   Call `list_apps` only when the request is unclear: it lists every app (id, name, what each makes) as data for you to suggest a few. When the user wants to look around, `show_apps` opens the app gallery.
2. **Gather inputs in one message.** Map what the user already said into the tool's fields. When you already have their `about` from `get_account`, fill what they didn't say from it: the aspect ratio for where they post, their brand, their style. For anything an app tool still needs (a preset's form collects its own):
   - their photo, clip or audio → `upload_file` for a file attached in chat (where offered), `prepare_upload` for a file where you can run commands, otherwise `show_upload` (pass `kind` when the field takes one kind, `app` with the app's id, and a short `purpose` such as "the photo becomes the first frame");
   - something they uploaded to Pika before → `list_jobs {filter: "uploads"}`, or `show_creations {filter: "uploads"}` to let them pick;
   - an earlier Pika result → `show_creations`;
   - a style, template, effect, voice or other choice the user picks → `show_presets` with the app (and `collection` when the field's description names one); it shows published presets and built-in choices. When you choose yourself, read them with `list_presets` with the same arguments instead, which shows the user nothing. An enum field's values are also its choices. A look the user describes works too.
   Open one card per turn, media first; show presets once the media is in.
   When they say they uploaded or picked, call `get_panel` with that card's `panel_id`.
3. **Price and run it.** Say in one line what you're running, then call it with the input and a fresh `request_id` and no `max_credits` and follow the quote's `next` (it applies the user's approval mode). Your line sits above the card, whose Create is the user's yes: don't ask for a yes or restate the price after it. The card runs the user's Create, edits and Take it further itself; once it reports a started job, don't call the tool again — use `get_job`. With no card, on a yes call it again with the same input, `request_id` and the agreed `max_credits`. The quote card shows the final prompt under "Sent to the model", where the user can still edit it.
4. **Follow `next`.** Each result names the next call, including when to wait on the job with `get_job`. When a run started from the card finishes, the result and its next steps are in the card; no need to describe them. A "Take it further with …" message from the card asks you to run that app on the named result. Otherwise offer the follow-ups the result suggests.

## Presets

A preset is one of Pika's curated presets: a ready-made run of an app with a few slots to fill. `show_presets {app}` shows the user an app's presets to pick from, and `show_preset {preset_id, inputs}` opens one preset's form with the slots you have filled in. When you need the data, without showing anything: `list_presets {app}` lists an app's presets, each with its `slots`: kind (`image`, `video`, `audio`, `text` or `choice`), whether required, how many, and the options; `list_preset_options {preset_id, slot}` lists a long option list; `get_preset {preset_id}` reads one preset with its `guide`, which you read before its first use. Run one with `create_from_preset` `{preset_id, inputs: [{slot, value}], request_id}`; a value is a media URL, text or an option id, and a slot repeats for several media. Price and run it as in step 3.

Pass what you already have. If required slots are missing it returns `needs_input` and the card's preset form collects the rest, so don't ask in text for choices the card shows. A preset needs no prompt guide; the prompt skills are for runs where you write the prompt.

Each task's app, for `show_presets {app}` (step 1):

- headshot from a photo → `headshot`;
- photo effect (squish, melt, inflate, …) → `pikaffects`;
- photo at a new aspect ratio or platform format → `smart-resize`, one ratio per run;
- replace the characters, outfits, location or products in a video → `swap-anything` (a `character_creator` sheet works as a character);
- add someone or something new to a video → `pikadditions`;
- new framing, angle or camera move for a clip → `camera-director` (see `pika-camera-director`);
- relight a photo or clip → `relight-media` (or `edit_image` for a photo);
- color grade a photo or clip, or copy a reference image's grade → `color-grading`;
- product shot from product photos → `product-shot`;
- longer video → `extend-video`; extend its output again for more, or plan a multi-shot video with `pika-video`;
- copy a clip's motion onto a photo → `motion-transfer`;
- sharper or higher resolution → `upscale` (see `pika-upscale`);
- cut a clip → `video-trim`; wait for it with `get_job`, then pass its output url to the next app. Cut a longer clip first for apps that take a short one (Camera Director, extend);
- talking head from a face and audio → `talking-head-studio`; a script is spoken with `create_speech` first, and its output passed once that job finishes;
- World Cup fan still → `world-cup`; anime World Cup clip → `anime-world-cup`.

## Other jobs

- an image from text or up to 10 references at up to 4K → `create_image` with model `seedream-4` (`1K`, `2K` or `4K`);
- sound effect, music, or a score for a clip → `create_audio` (see `pika-audio`);
- animate between a start and an end frame → `create_video` with model `pika`;
- new aspect ratio for a video → `create_video` with model `seedance-25`, the clip in `video_urls`, the target `aspect_ratio`, and a prompt to recompose the scene and extend its surroundings while keeping the subjects, action, timing and on-screen text;

To stop a running job the user no longer wants, call `cancel_job`. To find a job from earlier, call `list_jobs`; to show one, `show_creations` with its `job_id`.
