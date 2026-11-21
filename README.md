# Crock Bot

An open-source, self-hostable AI chatbot inspired by Grok.

> **Status:** early scaffold. Scope, stack, and features are still being defined.

## Goals

- Open source (MIT) and self-hostable
- Bring your own model/provider
- Clean, well-designed chat UI

## Project structure

```
crock-bot/
├── src/                 # application code (stack TBD)
├── docs/                # architecture and decision notes
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
