# Crock Bot

An open-source, self-hosted alternative to xAI's Grok Bot: persistent AI agents that work on their own Linux machine, with a web UI you can reach from anywhere and any model you choose.

> **Status:** research and design. Nothing runs yet. See [docs/research.md](docs/research.md) and [docs/architecture.md](docs/architecture.md).

## Goals

- Self-hosted on your own VPS; MIT licensed
- Any model: API key or local runtime
- Web UI reachable from anywhere
- Agents run on a separate Linux machine, one sandbox per bot
- Approvals before risky actions; secrets never shown to the model

## Project structure

```
crock-bot/
├── src/                 # application code (stack TBD)
├── docs/                # research.md, architecture.md, decisions
├── .claude/             # shared agent settings (skills/plugins)
├── AGENTS.md            # instructions for coding agents
├── CONTRIBUTING.md
├── .env.example
└── LICENSE
```

## Getting started

Not runnable yet. Setup instructions will land with the first implementation.

## Development with coding agents

This repo is set up to be built with agent skills. See [AGENTS.md](AGENTS.md).

- [mattpocock/skills](https://github.com/mattpocock/skills): engineering workflow (spec, tickets, TDD, code review)
- [ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill): design system and UI/UX guidance

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE)

Crock Bot is an independent project and is not affiliated with xAI or Grok.
