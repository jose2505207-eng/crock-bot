# Evaluation: which open-source clone to fork

Done 2026-11-21. Decisions so far: API keys only for now (no local models); fork an existing project instead of building from scratch.

## Recommendation

Fork **Rakazo** (https://github.com/elie222/rakazo, Apache-2.0). Inspected at commit `a78f51e` (2026-11-22 upstream time) by reading its docs and repo layout. It was not installed or run, and its code was not audited.

## Why Rakazo

| Requirement | Rakazo |
| --- | --- |
| Self-host on a VPS | Docker Compose installer; documented production deployment with HTTPS (Caddy) and a host-hardening script |
| UI from anywhere | Web app, plus Electron desktop, iOS and Android clients |
| API keys | Supported out of the box (OpenRouter key or a provider connected at onboarding) |
| Full Grok Bot feature set | Roster, memory, routines, computer and browser use with live view and takeover, approvals, group chats, delegation, voice, MCP and connected apps |
| License allows forking | Apache-2.0; keep `LICENSE` and `NOTICE` |
| Health | ~4,200 commits, daily activity, ~2,000 test files out of ~6,100 files |

Others considered: OpenMausBot (desktop only), OpenBot (alpha template, depends on CopilotKit Intelligence), Lorca (GPL-3.0, very young), Rerun (AGPL-3.0, needs Supabase), OpenTeam (bots share logins and passwordless sudo), OpenClaw and Hermes Agent (no per-bot computer and roster UI).

## Gaps and improvement candidates

1. **Agents on their own Linux machine (our requirement).** Rakazo's Docker computers must run on the same host as the API and worker, because they mount bot homes from a shared data directory. Its documented ways to move computers off the VPS are hosted providers (E2B, Daytona and others) or Kubernetes. A self-hosted "second machine runs the computers" mode is not documented. This is the clearest thing to build. Needs confirmation in code.
2. **Safer defaults for a single-owner VPS.** `.env.example` ships `SIGNUPS_ENABLED=true`, and computer egress defaults to `auto`, which can fall back to open and expose cloud metadata. Both are fixable by configuration; a hardened single-owner preset would make it the default.
3. **Operational weight.** Postgres, API, worker, supervisor, web and a container per bot. A slimmer single-user profile may be possible. Unverified.

## Costs of forking

- Upstream moves fast (hundreds of open PRs and issues). A fork that diverges will be expensive to keep in sync. Keep changes small and isolated, and offer them upstream where possible.
- The earlier `architecture.md` proposal is superseded by Rakazo's architecture if we fork.

## Open decisions

- How to fork: GitHub "Fork" button (keeps the upstream link) or import Rakazo's history into this repo (replaces the current scaffold).
- Rename and rebrand to Crock Bot now, or run it unmodified first.
- Agent machine: second VPS, and its specs.
