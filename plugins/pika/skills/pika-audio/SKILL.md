---
name: pika-audio
description: Use when the user wants music, a song with lyrics, a sound effect, or a soundtrack scored to a video clip.
---

# Music, sound effects and soundtracks

1. To score a video, use `create_audio` with `model: "pika/pika-audio/pika-soundtrack"`: the clip as `video` (an earlier output url, an earlier upload from `list_jobs {filter: "uploads"}`, `upload_file` for a chat attachment, otherwise `show_upload` with `kind: "video"`) and an optional `instruction` (blank scores the picture on its own). Skip to step 4.
2. Otherwise pick another `model` (default `pika/pika-audio/pika-music`); its values are the choices, listed here:
   - Music: `pika/pika-audio/pika-music` (`prompt`, `duration` 10–360 s in 5 s steps, default 30, optional `lyrics`) · `minimax/minimax-music-3.0/text-to-audio` (`prompt` and/or `lyrics`, `is_instrumental`; an instrumental needs a prompt) · `sonilo/sonilo-v1.1-music/text-to-music` (`prompt`, `duration` 5–360 s in 5 s steps) · `google/lyria-3-pro/text-to-audio` and `google/lyria-2/sound-effects` (`prompt` only).
   - Sound effects: `pika/pika-audio/pika-sfx` (`prompt`, `duration` 1–20 s, default 10) · `elevenlabs/eleven-text-to-sound-v2/sound-effects` (`text` up to 450 chars, `duration_seconds` 1–30, default 5, `prompt_influence` 0–1) · `sonilo/sonilo-v1.1-sfx/sound-effects` (`prompt`, `duration` 1–180 s).
   - Other: `bytedance/seed-audio-1.0/text-to-audio` (`prompt` up to 3000 chars).
3. Describe genre, mood, instruments and tempo for music; the source, action and space for a sound effect.
4. Say in one line what you're running, then call the tool with a fresh `request_id` and no `max_credits` and follow the quote's `next` (it applies the user's approval mode). Your line sits above the card, whose Create is the user's yes: don't ask for a yes or restate the price after it. The card runs the user's Create, edits and Take it further itself; once it reports a started job, don't call the tool again — use `get_job`. With no card, on a yes call it again with the same input, `request_id` and the agreed `max_credits`.
5. To lay it under a video, add it to the project with `add_clips` as an `a2` clip, the score lane, with `at: 0, duration: "to_end"`. To put the user's own video or audio on the timeline, upload it (`upload_file` for a chat attachment, `prepare_upload` where you can run commands), `add_media` it into the project, then `add_clips` with the returned `source`.
