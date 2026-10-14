---
name: pika-podcast
description: Use when the user wants a video podcast, talk show, interview, debate or solo episode with on-camera hosts, or asks which podcast sets or voices exist.
---

# Video podcast

1. Use the `podcast_creator` tool. It renders one segment per call; an episode of `length` seconds (`auto`, `10`, `15`, `30`, `45`, `60`, `120`, `180`) has `ceil(length / 30)` segments, and `auto` is one segment the model sizes itself.
2. Gather in one message: the topic or the user's own script (`own_script: true` when verbatim), `format` (`conversation`, `interview`, `debate`, `solo`), host and guest names, personas and voices, and optional host and guest photos (`upload_file` for a chat attachment, otherwise `show_upload` with `kind: "image"`; without photos it is text-to-video).
3. Set: call `show_presets` for `podcast_creator` with `collection: "sets"` for the user to pick, and pass the picked id as `set` (default `modern`).
4. Voices: `show_presets` with `collection: "host-voices"` or `"guest-voices"`, passing the pick as `host.voice` or `guest.voice`. A lowercase name also works (`adam`, the host default; `rachel`, the guest default; `sarah`, `george`, `brian`, …). A solo episode ignores the guest.
5. Write the dialogue per segment as `Host: …` / `Guest: …` lines, about 2.4 words per second of segment (a segment is the episode length divided evenly, at most 30 s), or the speech comes out rushed. Optional: `layout` (`16:9`, `9:16`, `1:1`), `quality` (`720p`, `1080p`), `scene_notes`, up to 8 `reference_urls`.
6. For more than one segment, `create_project` first and pass its `project_id` on every call. A new project is 1080x1920 and calls take its aspect unless you pass `layout`, so for `16:9` or `1:1` set its `width` and `height` with `update_timeline` first. Use one `continuity_id` for the episode and `segment_index` 0, 1, … with the same host, guest, set and length.
7. Quote each segment: call `podcast_creator` with its own fresh `request_id` and no `max_credits`. Sum the quotes into one episode total and follow the quotes' `next` with that total as the plan. A segment the card reports as started (the user pressed Create) is running: don't call it again; use `get_job`. On a yes, call each other segment again with the same input and `request_id` and its quoted `max_credits`, keeping a running total within the agreed one.
8. When the segments are finished, read the `revision` with `get_project` (`show_projects` with the `project_id` opens its timeline for the user) and `add_clips` them in segment order (`duration` = the segment's seconds) with a one-line `note` saying what you placed, then `export_project` with a fresh `request_id`.
