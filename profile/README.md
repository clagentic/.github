<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/clagentic/.github/main/profile/clagentic-wordmark-dark.png" />
    <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/clagentic/.github/main/profile/clagentic-wordmark-light.png" />
    <img src="https://raw.githubusercontent.com/clagentic/.github/main/profile/clagentic-wordmark-light.png" alt="clagentic" width="278" />
  </picture>
</p>

<h4 align="center">AI tooling. Built for builders.</h4>

<p align="center">
  <a href="https://clagentic.ai"><img src="https://img.shields.io/badge/-clagentic.ai-00CFFF?style=flat&logoColor=white" alt="clagentic.ai" /></a>
  <a href="https://ko-fi.com/clagentic"><img src="https://img.shields.io/badge/Ko--fi-FF5E5B?style=flat&logo=ko-fi&logoColor=white&label=support" alt="Support on Ko-fi" /></a>
  <a href="mailto:hello@clagentic.ai"><img src="https://img.shields.io/badge/hello%40clagentic.ai-4A7FE8?style=flat&logo=mail.ru&logoColor=white" alt="hello@clagentic.ai" /></a>
</p>

---

Self-hosted tools for developers working with AI agents — focused on control,
auditability, and keeping complexity where it belongs: in the stack, not in the cloud.

## tools

The full index is at **[clagentic.ai/tools](https://clagentic.ai/tools)**.

### End-User Tools

The interfaces you run directly — a workspace, a coding harness, and a vetted app registry for your agents.

| Tool | What it does |
|---|---|
| [clagentic: console](https://github.com/clagentic/clagentic-console) | Self-hosted, multi-user team workspace daemon where human developers and named AI agents (Claude Code, Codex) share the same interface — each with their own login, session history, and tool-approval flow. Agents are first-class users: from a shell or inside a session they can open, message, and schedule input into each other's sessions, and every injected message records its sender. Installable via `npm install -g @clagentic/console`; projects, sessions, and approvals stay on your own machine |
| [clagentic: lite](https://github.com/clagentic/clagentic-lite) | Cross-vendor AI coding harness (POSIX shell, no server) that enforces deterministic security gates around Claude Code / Codex sessions — five roles (Builder, Reviewer, Auditor, Merge Gate, Troubleshooter), each with its own model-CLI fallback chain, and five gates including local security scans and a full SQLite audit trail |
| [clagentic: toolshed](https://github.com/clagentic/clagentic-toolshed) | Vetted, sandboxed, self-updating registry of agent-drivable apps (CLI or MCP) — a release installs only if its checksum list is GPG-signed by a pinned key and the archive matches, then agents run it as an MCP server in a locked-down container (no network, read-only root, capabilities dropped, three mounts). Updates auto-promote only when the tool surface is unchanged, otherwise they are held for approval, with rollback; standalone, needs no other clagentic product |

### Platform & Infrastructure

The services these tools (and your own agents) run on top of.

| Tool | What it does |
|---|---|
| [clagentic: router](https://github.com/clagentic/clagentic-router) | Self-hosted Go daemon that routes LLM API calls across multiple backends (Claude CLI, Codex CLI, Gemini CLI, Ollama, Anthropic API, OpenAI API, AWS Bedrock), walking a configurable fallback chain on rate-limit or outage, scoring backends by health, quota pressure, and cost, and exposing an OpenAI-compatible `/v1/chat/completions` endpoint (plus Anthropic Messages and Bedrock-shaped endpoints) |
| [clagentic: gatekeeper](https://github.com/clagentic/clagentic-gatekeeper) | Go service for agent identity and role-scoped access: an open Identity Assertion contract (signed, short-lived statement of who is acting, on whose behalf, under which role ceiling; published schemas and conformance vectors) plus a mint half that issues short-lived, role-scoped GitHub App installation tokens — builder, reviewer, merger, security, or custom roles — so build/review/merge actions are performed by separate identities. App private keys never reach the agent; the assertion issuer itself is not yet part of the release |
| [clagentic: triage](https://github.com/clagentic/clagentic-triage) | LLM-powered triage agent that watches a GitHub org or repo for new issues/PRs, assesses each against repo-specific intent context, and produces a verdict and suggested action — human-in-the-loop by default (auto-approve opt-in per action class), external contributors only by default, with pluggable source adapters for GitHub, GitLab, and Forgejo, multiple LLM runners (Claude CLI, Anthropic API, any OpenAI-compatible server), and optional dispatch into Jira, Linear, GitHub Issues, or a webhook |
| [clagentic: directory](https://github.com/clagentic/clagentic-directory) | Self-hosted, dependency-free Go HTTP registry that stores versioned agent capability declarations and answers routing queries — which agents handle a given intent, accept a conversation kind, or follow a specific agent in a sequencing chain. Registry from a local directory (hot-reload) or a polled git repo, strict vocabulary validation, and opt-in self-build mechanisms that propose changes for operator review |
| [clagentic: loadout](https://github.com/clagentic/clagentic-loadout) | Platform-agnostic Python CLI that issues each agent role the exact set of verbs it may run and nothing else — attested identity, guard hooks, and a fail-closed merge gate (stale-SHA refusal, reviewer-verdict fences, PR-title gate) — with bot-attributed push/review/merge on Forgejo or GitHub |

## design principles

- **self-hosted first** — run it on your own infrastructure, not someone else's
- **CLI over SDK** — agents talk to each other via standard interfaces, not vendor lock-in
- **composable** — each component does one thing; you wire them together
- **auditable** — no magic black boxes; decisions, tokens, and access are all traceable
