---
name: pika-speech
description: Use when the user wants text spoken aloud — a voiceover, narration or text-to-speech clip — or asks which Pika voices exist.
---

# Speech and voiceover

1. Use the `create_speech` tool. Pick `model` (default ElevenLabs Multilingual v2); each takes different fields:

   | `model` | Script field (max chars) | Voice field |
   | --- | --- | --- |
   | `pika/pika-audio/pika-speech` | `script` (15000) | `voice_preset`, default `calm_documentary_narrator` |
   | `elevenlabs/eleven-multilingual-v2/text-to-speech` | `text` (10000) | `voice_id`, default Rachel; `stability` 0–1, default 0.5 |
   | `elevenlabs/eleven-turbo-v2-5/text-to-speech` | `text` (40000) | same as Multilingual |
   | `minimax/minimax-speech-02-hd/text-to-speech` | `text` (50000) | `voice_id`: any MiniMax voice id, free text, default `Wise_Woman` |
   | `minimax/minimax-speech-02-turbo/text-to-speech` | `text` (50000) | same as HD |
   | `bytedance/seed-audio-1.0/text-to-audio` | `prompt` (3000) | `voice`, optional; omit and the model picks |

2. To let the user pick a voice, call `show_presets` for `create_speech` with the model's collection (`list_presets` with the same arguments when you choose yourself) and pass the pick in its field: `pika-voices` → `voice_preset` (76 stock voices, e.g. `deep_trailer_bass`, `polished_news_anchor`, `cozy_grandpa_storyteller`), `elevenlabs-voices` → `voice_id`, `seed-voices` → `voice`. MiniMax has no list; any MiniMax voice id works.

   ElevenLabs ids: `21m00Tcm4TlvDq8ikWAM` Rachel · `pNInz6obpgDQGcFmaJgB` Adam · `EXAVITQu4vr4xnSDxMaL` Sarah · `ErXwobaYiN019PkySvjV` Antoni · `AZnzlk1XvdvUeBnXmlld` Domi · `IKne3meq5aSn9XLyUdCD` Charlie · `JBFqnCBsd6RMkjVDRZzb` George · `TX3LPaxmHKxFdv7VOQHJ` Liam · `pFZP5JQG7iQjIQuC4Bku` Lily · `nPczCjzI2devNBz1zQrb` Brian · `cgSgspJ2msm6clMCkdW9` Jessica

3. Say in one line what you're running, then call `create_speech` with a fresh `request_id` and no `max_credits` and follow the quote's `next` (it applies the user's approval mode). Your line sits above the panel, whose Create is the user's yes: don't ask for a yes or restate the price after it. The panel runs the user's Create, edits and Take it further itself; once it reports a started job, don't call the tool again — use `get_job`. With no panel, on a yes call it again with the same input, `request_id` and the agreed `max_credits`.
4. Offer follow-ups: `talking-head-studio` to lip-sync a face to it (see `pika-create`), or `create_audio` for music under it.
