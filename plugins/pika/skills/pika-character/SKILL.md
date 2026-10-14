---
name: pika-character
description: Use when the user wants a reusable character — a character reference sheet, persona or avatar saved to their Library — from a photo, a description or picked traits.
---

# Character reference sheet

1. Use the `character_creator` tool: it makes a five-view reference sheet and files it as a Library character. Every call needs a `name`.
2. Pick `mode` from what the user has:
   - `image`: one front-facing photo in `image_urls` (`upload_file` for a chat attachment, otherwise `show_upload` with `kind: "image"`), optional `backstory`;
   - `describe`: a `description` plus a `style`;
   - `traits`: `characterType`, `gender`, `origin`, `skin`, `eyes`, `age`, `fashion`; each defaults (human, female, european, tan, brown, adult, casual).
3. Style and trait values are preset ids. To show them, call `show_presets` for `character_creator` with the field's collection — it defaults to `voices`, so always pass one: `style` → `styles`, `characterType` → `types`, `gender` → `genders`, `origin` → `origins`, `skin` → `skin_tones`, `eyes` → `eye_colors`, `age` → `ages`, `fashion` → `fashion_styles`. One picker per turn; ask about the rest in words. `characterType` and `fashion` also take the user's own words.
4. Optional `voice`, stored on the character: `show_presets` with `collection: "voices"` shows the voices; pass the picked id.
5. `model` defaults to `nano-banana-edit` for `image` and `nano-banana-2.1` otherwise; others: `gpt-image-2`, `nano-banana`, `nano-banana-pro`, `ideogram-v4`, `seedream-5-lite`, `seedream-5-pro`.
6. Say in one line what you're running, then call `character_creator` with a fresh `request_id` and no `max_credits` and follow the quote's `next` (it applies the user's approval mode). Your line sits above the card, whose Create is the user's yes: don't ask for a yes or restate the price after it. The card runs the user's Create, edits and Take it further itself; once it reports a started job, don't call the tool again — use `get_job`. With no card, on a yes call it again with the same input, `request_id` and the agreed `max_credits`.
7. Offer follow-ups: use the sheet's output url as a reference image in `create_video`, or as a character in `swap-anything`.
