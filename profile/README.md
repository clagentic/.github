<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/clagentic/.github/main/profile/clagentic-wordmark-dark.png" />
    <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/clagentic/.github/main/profile/clagentic-wordmark-light.png" />
    <img src="https://raw.githubusercontent.com/clagentic/.github/main/profile/clagentic-wordmark-light.png" alt="clagentic" width="360" />
  </picture>
</p>

<h5 align="center">clagentic</h5>

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

The interfaces you run directly — a workspace and a coding harness.

| Tool | What it does |
|---|---|
| [clagentic: console](https://github.com/clagentic/clagentic-console) | Self-hosted, multi-user team workspace daemon where human developers and named AI agents (Claude Code, Codex) share the same interface — each with their own login, session history, and tool-approval flow. Installable via `npm install -g @clagentic/console`; projects, sessions, and approvals stay on your own machine |
| [clagentic: lite](https://github.com/clagentic/clagentic-lite) | Cross-vendor AI coding harness (POSIX shell, no server) that enforces deterministic security gates around Claude Code / Codex sessions — five roles (Builder, Reviewer, Auditor, Merge Gate, Troubleshooter), each with its own model-CLI fallback chain, and five gates including local security scans and a full SQLite audit trail |

### Platform & Infrastructure

The services these tools (and your own agents) run on top of.

| Tool | What it does |
|---|---|
| [clagentic: router](https://github.com/clagentic/clagentic-router) | Self-hosted Go daemon that routes LLM API calls across multiple backends (Claude CLI, Codex CLI, Ollama, Anthropic API, OpenAI API), walking a configurable fallback chain on rate-limit or outage and exposing an OpenAI-compatible `/v1/chat/completions` endpoint |
| [clagentic: gatekeeper](https://github.com/clagentic/clagentic-gatekeeper) | Go service that mints short-lived, role-scoped GitHub App installation tokens for automated agents — builder, reviewer, merger, security — so build/review/merge actions are performed by separate identities. App private keys never reach the agent; it mints tokens, that is the whole surface |
| [clagentic: triage](https://github.com/clagentic/clagentic-triage) | LLM-powered triage agent that watches a GitHub org or repo for new issues/PRs, assesses each against repo-specific intent context, and produces a verdict and suggested action — human-in-the-loop by default, with pluggable adapters for GitHub, GitLab, and Forgejo |
| [clagentic: directory](https://github.com/clagentic/clagentic-directory) | Self-hosted, dependency-free Go HTTP registry that stores versioned agent capability declarations and answers routing queries — which agents handle a given intent, accept a conversation kind, or follow a specific agent in a sequencing chain |
| [clagentic: loadout](https://github.com/clagentic/clagentic-loadout) | Platform-agnostic Python CLI that issues each agent role the exact set of verbs it may run and nothing else — attested identity, guard hooks, and a fail-closed merge gate (stale-SHA refusal, reviewer-verdict fences, PR-title gate) — with bot-attributed push/review/merge on Forgejo or GitHub |

## design principles

- **self-hosted first** — run it on your own infrastructure, not someone else's
- **CLI over SDK** — agents talk to each other via standard interfaces, not vendor lock-in
- **composable** — each component does one thing; you wire them together
- **auditable** — no magic black boxes; decisions, tokens, and access are all traceable
