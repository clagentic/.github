<p align="center">
  <img src="https://raw.githubusercontent.com/clagentic/.github/main/profile/clagentic-logo-256.png" alt="clagentic" width="96" />
</p>

<h2 align="center">clagentic</h2>

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

| Tool | What it does |
|---|---|
| [clagentic:console](https://github.com/clagentic/clagentic-console) | Self-hosted browser console for Claude Code and Codex — tool approvals, sessions, push notifications, from any device |
| [clagentic:router](https://github.com/clagentic/clagentic-router) | Self-hosted LLM routing daemon — fallback chains, quota tracking, OpenAI-compatible API |
| [clagentic:lite](https://github.com/clagentic/clagentic-lite) | Cross-vendor coding harness — Builder/Reviewer roles, security gates, SQLite audit trail. No server |
| [clagentic:gatekeeper](https://github.com/clagentic/clagentic-gatekeeper) | Role-scoped GitHub App tokens for automated agents — builder, reviewer, merger |
| [clagentic:triage](https://github.com/clagentic/clagentic-triage) | LLM-powered triage agent for GitHub issues and PRs |
| [clagentic:directory](https://github.com/clagentic/clagentic-directory) | Agent capability registry — discover, resolve, and route to agents by capability |

## design principles

- **self-hosted first** — run it on your own infrastructure, not someone else's
- **CLI over SDK** — agents talk to each other via standard interfaces, not vendor lock-in
- **composable** — each component does one thing; you wire them together
- **auditable** — no magic black boxes; decisions, tokens, and access are all traceable
