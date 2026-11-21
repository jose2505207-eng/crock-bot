# Agent instructions

Crock Bot is an open-source, self-hostable AI chatbot. The stack is not chosen yet; do not assume one.

## Skills

Install once per machine (Claude Code):

```
claude plugin install mattpocock-skills@claude-plugins-official
/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill
/plugin install ui-ux-pro-max@ui-ux-pro-max-skill
```

Then run `/setup-matt-pocock-skills` once in this repo.

Other agents: `npx skills@latest add mattpocock/skills -a <agent>` and `npx ui-ux-pro-max-cli init --ai <agent>`.

## Workflow

1. Clarify scope before building: `/grill-me` or `/grill-with-docs`.
2. Turn decisions into a spec, then tickets: `/to-spec`, `/to-tickets`.
3. Implement test-first (`tdd`), one ticket per PR.
4. UI work: generate the design system with ui-ux-pro-max first and persist it to `design-system/`; follow it for every screen.

## Conventions

- Record architecture decisions in `docs/`.
- Never commit secrets; add new variables to `.env.example`.
- Keep the README in sync with what actually runs.
