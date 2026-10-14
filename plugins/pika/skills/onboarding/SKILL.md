---
name: onboarding
description: Run right after Pika is installed or when the user chooses Set up for Pika — signs in, says what Pika makes, learns what the user makes to suggest where to start, and sets how Pika asks before spending credits. Skippable.
---

# Set up Pika

Pika works only through the tools of the Pika MCP server this plugin installs (`pika`, or `pika-staging` for the staging plugin): creation tools (`create_video`, `create_image`, `product_ad`, …), `create_from_preset` for Pika's curated presets (headshots, photo effects, camera moves, …), plus `show_presets`, `show_preset`, `list_presets`, `get_preset`, `show_upload`, `get_job`, `get_account` and the rest. Never stand in for them with built-in image, video or audio generation.

Setup is a short conversation, not a form: a few lines per message, one question at a time, no headings. Never mention these steps or say why you stop; tell the user only what they need next. If you have a tool for multiple-choice questions, use it for the choices below. Whenever the user wants to skip ("just start", "skip", or they ask for something), stop setup and go to **Jump in**.

1. **Sign in.** If there are no Pika tools in your tool list, Pika isn't connected or signed in. Tell the user how to sign in, then stop:
   - Codex CLI: run `codex mcp login pika` (`codex mcp login pika-staging` for staging; `codex mcp list` shows the server's name and whether it's logged in).
   - Codex or ChatGPT app: sign in to Pika from the plugin's settings, then start a new chat.
   - Claude Code: run `/mcp` and sign in to Pika.
2. **Account.** Call `get_account` with `{}`.
   - If it fails with a sign-in error (`SIGN_IN_REQUIRED` or "Sign in to Pika to continue"), the user isn't signed in yet. Most apps show their own sign-in prompt for it (a sign-in sheet in ChatGPT and Codex, a Connect card in Claude); ask the user to finish signing in there, then call `get_account` again. Where no prompt appears, use the steps in step 1.
   - If the user installed Pika in the middle of a task, go to **Jump in**.
   - If `about` is saved and an approval mode is chosen, they have set up before: welcome them back in a line and ask what they'd like to make, or whether to redo setup.
3. **Welcome.** In one message:
   - what Pika is, in a sentence or two, for example: "Pika makes and edits video, images, music and voice right here: 40+ models (Seedance, Kling, Veo, Nano Banana, GPT Image, ElevenLabs and more), apps built for jobs like product ads, studio headshots, lip-synced talking heads and short films, and 150+ presets for effects, styles and looks.";
   - their credit balance, in a few words;
   - the choice: a minute of setup so you can suggest where to start, or jump straight in.
4. **About them.** If you already know something about the user from your memory, earlier chats or files you can read, don't make them repeat it: say in a line what you'd use and ask whether you may. Otherwise ask one open question: what they make and where it goes, with a few short examples ("TikToks for my bakery", "ads for clients", "music videos", "just exploring").
   Then play back what you'll keep in one line ("You make … for … on …"). Once they confirm, save it with `set_preferences` as `about`. Keep only what helps creative suggestions (what they make, who for, where it's posted, brand and style) and nothing sensitive. Tell them they can ask you to change or clear it any time.
5. **Where to start.** Suggest three Pika apps that fit them, one line each: the app's title and a first idea in their terms, for example for a candle shop on TikTok, "Product Ad: your candle in a 9:16 cozy-evening spot". Suggest only apps you have a tool or preset for. Run nothing yet.
6. **Approvals.** If an approval mode is already chosen, go to step 7. Otherwise say that before the first run they choose how Pika asks before it spends credits, and call `show_settings` with `{}`:
   - When it opens the settings panel, point them to it in one line and end your turn. Don't list the modes. This settings panel saves the pick and posts it in the chat, so don't call `set_preferences` for it, and open no other Pika view this turn: it would replace the panel.
   - When it lists the modes as text instead, show them one line each and save the reply with `set_preferences` (autopilot also needs `auto_approve_credits`).
7. **First creation.** Once a mode is set (acknowledge a new pick in a few words), ask which idea to start with, or anything else they have in mind; continue with the `pika-create` playbook. If they'd rather look around, call `show_apps` to open the app gallery.

**Jump in.** Ask nothing more about setup. Continue their task with the `pika-create` playbook, straight to the app for it. If they have none yet, call `list_apps`, offer a few apps in a line each, or ask them to just describe what they want. Leave the approval mode unset: the first quote asks for it in its panel, which saves the pick without posting in the chat.
