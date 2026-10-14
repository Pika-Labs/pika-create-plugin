---
name: pika-camera-director
description: Use when the user wants to reshoot or reframe a video with a new camera angle, framing or move, or asks what Camera Director can do / its presets.
---

# Camera Director

1. The video: an earlier output url, an earlier upload from `list_jobs {filter: "uploads"}`, or one the user gave; otherwise leave it out and the preset form takes the upload (where there is no card, `upload_file` for a chat attachment or `prepare_upload`). It must be one shot of 4–30 seconds; cut a longer clip with `video-trim` first and pass its output url.
2. Unless the user named the move, let them pick it: `show_presets {app: "camera-director"}`, with the video in `inputs` when you have it. When they name the shot in words, or no card shows, map their words to options from `list_preset_options`. An invalid framing, angle and motion combination is refused before any price with the allowed values; pick one of them and retry.
3. Say in one line what you're running, then call `create_from_preset` with a fresh `request_id` and no `max_credits` and follow the quote's `next` (it applies the user's approval mode). Your line sits above the card, whose Create is the user's yes: don't ask for a yes or restate the price after it. The card runs the user's Create, edits and Take it further itself; once it reports a started job, don't call the tool again — use `get_job`. With no card, on a yes call it again with the same input, `request_id` and the agreed `max_credits`.
4. Offer follow-ups: another camera move, `extend-video` to continue the shot, or `create_audio` with `model: "pika/pika-audio/pika-soundtrack"` for music.
