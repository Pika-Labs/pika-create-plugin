---
name: pika-ad
description: Use when the user wants a video ad, commercial or promo for a product or brand from a product photo, logo or screenshot.
---

# Product or brand ad

1. Use the `product_ad` tool: it makes the whole ad, up to 30 s, in one take.
2. Gather in one message:
   - the product photos as `product_image_urls` (1–8) via `upload_file` for a chat attachment, otherwise `show_upload` with `kind: "image"` — for a brand with no physical product, a logo or app screenshot works;
   - the user's `brief`, and the screenplay you write from it as `concept`: a `logline`, `beats` (each an `action`, with optional `timecode` and `voiceover`) and an optional `cta`, which needs `audio.voiceover` or `audio.talking` on;
   - `length_s` (`6`, `15` or `30`, default 15) and the tool's other fields, filled from what the user said;
   - optionally an on-screen character with a `character.name`: the user's photo as `character.image_url`, or a stock one the user picks from `show_presets` for `product_ad` with `collection: "characters"`, its id as `character.preset` (then leave out `image_url`);
   - optionally a look: a `looks` id from `show_presets` with `collection: "looks"`, or the user's own words, as `look`.
3. Say in one line what you're running, then call `product_ad` with the input and a fresh `request_id` and no `max_credits` and follow the quote's `next` (it applies the user's approval mode). Your line sits above the panel, whose Create is the user's yes: don't ask for a yes or restate the price after it. The panel runs the user's Create, edits and Take it further itself; once it reports a started job, don't call the tool again — use `get_job`. With no panel, on a yes call it again with the same input, `request_id` and the agreed `max_credits`.
4. Offer follow-ups: `create_audio` with `model: "pika/pika-audio/pika-soundtrack"` to score it, `upscale`, or `extend-video` for a longer cut. For a multi-scene spot, see `pika-video`.
