# Architecture (proposal, not yet approved)

Derived from the stated requirements: self-hosted on our own VPS, model from a local runtime or an API key, UI reachable from anywhere, agents running on their own Linux machine.

## Components

```
 Browser / phone
       │ HTTPS + login
┌──────▼───────────────── VPS: control plane ─────────────────┐
│ Web UI      roster, chat, approvals, live screen view        │
│ API         auth, bots, chats, realtime events               │
│ Orchestrator agent loop, tool calls, review gate             │
│ Scheduler   routines (cron + event triggers)                 │
│ Store       database (bots, memory, logs) + encrypted vault  │
│ Model router one interface → API providers or local runtime  │
└──────┬───────────────────────────────────────────────────────┘
       │ outbound connection opened by the runner
┌──────▼──────────── Linux agent machine: runner ─────────────┐
│ Runner daemon   executes tool calls, reports results         │
│ Per-bot sandbox shell, files, browser, virtual display       │
│ Screen stream   live view and takeover                       │
└──────────────────────────────────────────────────────────────┘
```

## Key decisions proposed

1. **Control plane and runner are separate processes** that can live on one VPS or two. The runner dials out to the control plane, so the agent machine needs no open inbound ports.
2. **One isolated sandbox per Bot** (container or VM) instead of Grok Bot's shared computer. This fixes its main documented weakness. Sharing becomes opt-in.
3. **Model router speaks one OpenAI-compatible interface**, covering hosted providers and local runtimes such as Ollama or vLLM. Model is configurable per Bot.
4. **Secrets never enter model context.** The runner injects vault values into pages or environment variables.
5. **Approval gate on by default** for sends, payments, deletes and shell commands outside an allowlist.
6. **MCP as the plugin system** rather than inventing our own connector format.

## Risks

- **Local model quality.** Computer use needs reliable tool calling and vision. Small local models are likely to struggle with browser tasks; this needs testing, not assumption.
- **Local model hardware.** A typical VPS has no GPU. Local inference probably means a separate GPU machine or a slow CPU-only model.
- **Security.** An internet-reachable UI that can drive a shell is a high-value target. Auth, TLS and the approval gate are v1 requirements, not polish.
- **Scope.** Full parity (voice, mobile apps, Slack/X clients, marketplace) is large. Phasing below.

## Phases

| Phase | Delivers |
| --- | --- |
| 1 | Login, Bot roster, chat, model router (API key + local), runner with shell and files, approval cards |
| 2 | Browser and computer use, live screen view and takeover |
| 3 | Per-Bot memory, skills, routines (schedule) |
| 4 | Vault, MCP connectors, event triggers, multi-Bot hand-off |
| 5 | Mobile-friendly PWA, voice, Slack or Telegram client |

## Open decisions

- Build from scratch, or fork or borrow from an existing clone (see `research.md`)?
- Stack for control plane and runner.
- Sandbox technology: Docker containers, or full VMs.
- Single user, or multiple accounts.
