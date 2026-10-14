# Pika plugin

Make and edit images, video, music, sound effects and voice with [Pika](https://pika.art)'s creation apps, from Claude Code, Codex and ChatGPT.

The plugin connects your agent to Pika's MCP server (`https://mcp.pika.art/mcp`) and adds task skills for ads, headshots, multi-shot video, camera moves, podcasts, voiceover, music, upscaling and prompt writing. Generations use the credits on your Pika account.

## Install

### Claude Code

```
/plugin marketplace add Pika-Labs/pika-create-plugin
/plugin install pika@pika
```

Then run `/mcp` and sign in to Pika.

### Codex

```sh
codex plugin marketplace add Pika-Labs/pika-create-plugin
```

Then install **Pika** from the plugin list. Installing signs you in to Pika and runs the `onboarding` skill.

## Contents

```
plugins/pika/plugin.json            plugin manifest (Agent Plugins layout)
plugins/pika/.claude-plugin/        Claude Code manifest
plugins/pika/mcp.json               the Pika MCP server
plugins/pika/skills/                task skills
.claude-plugin/marketplace.json     Claude Code marketplace
.agents/plugins/marketplace.json    Codex and ChatGPT marketplace
```

## Support

Questions and account issues: [pika.art/support](https://pika.art/support). See the [terms of service](https://pika.art/terms-of-service) and [privacy policy](https://pika.art/privacy-policy).

This repository is published automatically from Pika's internal plugin repository, so pull requests here are not merged. Please report problems as issues.

## License

[MIT](LICENSE)
