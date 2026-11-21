# Research: what Grok Bot is

Researched 2026-11-21 from xAI's public docs and third-party write-ups. xAI has not published Grok Bot's internal orchestration code, so everything below describes documented behaviour, not implementation.

## Summary

Grok Bot (xAI, beta since 2026-08-11) is not a chatbot. It is a roster of persistent, named agents ("Bots") that work on an always-on cloud computer with a browser, filesystem and terminal, sign in to the user's apps, and keep working while the user is away. It is closed source, hosted by xAI, and limited to xAI-routed models. Those three points are what Crock Bot changes.

## Core concepts

xAI's design post names five: Bots, Chats, Prompts (one-off, saved as Skills, or triggered as Routines), Tools, Artifacts.

| Concept | Documented behaviour |
| --- | --- |
| Bot | Persistent named agent with a job, memory and routines. One "primary" Bot coordinates the others. |
| Computer | One persistent cloud computer shared by all of an account's Bots. Each Bot has its own screen; several run at once; files and browser sign-ins are shared. |
| Live view / takeover | User can watch a Bot's screen and take control for SSO, passkeys or CAPTCHAs, then hand back. |
| Memory | Per Bot: preferences, rules, dated work log. Basic user facts (name, time zone) shared across Bots. User can ask a Bot to remember, correct or forget. |
| Tools | Connected apps via API (preferred over browser clicks), MCP servers, shell, computer use. |
| Skills | A task walked through once can be saved and reused. |
| Routines | Skills run on a schedule or on an event (Slack message, email to the Bot). |
| Vault | Stores logins and cards; values are filled into pages without the model seeing them. |
| Auto Review | Checks commands and actions before they run; shows an approval card when the user is needed. |
| Custom Rules | Plain-language rules set to "Ask first" or "Allow automatically". |
| Clients | Desktop, mobile, Slack, X. Text and voice. |

## UI patterns worth copying

- Sidebar is a roster of Bots, not a chat history.
- Bot avatar motion shows state: idle, thinking, working, waiting, blocked, done.
- Three levels of computer access: status indicator, side-panel preview, full-screen takeover.
- One transcript mixes messages, system events (routine created, Bot messaged) and inline cards.
- Scoping: tools and skills belong to the account; memory and routines belong to each Bot.

## Known weaknesses of the original

- Bots are not isolated from each other: shared files, shared browser sessions, any Bot can use a saved card. xAI's docs say not to treat Bots as a security boundary.
- Auto Review reduces prompt-injection risk but does not remove it.
- No self-hosting, no model choice.

## Existing open-source clones

Several already exist (Rakazo, OpenMausBot, useAgent, Rerun, others). Rakazo is described by reviewers as the closest match. Not yet evaluated first-hand; see the open decision in `architecture.md`.

## Sources

- https://docs.x.ai/grok-bot/overview.md
- https://docs.x.ai/grok-bot/how-grok-bot-works.md
- https://x.ai/news/designing-grok-bot
- https://www.vellum.ai/blog/official-grok-bot-breakdown
- https://www.digitalapplied.com/blog/grok-bot-ai-teammates-launch-cloud-computer-2026
- https://www.bitdoze.com/best-open-source-grok-bot-alternatives/
- https://github.com/elie222/rakazo
