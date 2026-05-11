---
layout: default
title: AI Tooling
nav_order: 7
permalink: /ai-tooling/
---

# AI tooling
{: .no_toc .text-delta }

1. TOC
{:toc}


AI and LLM-powered assistants — Claude Code, Cursor, GitHub Copilot, Codex CLI, and the agent features built into modern IDEs — are now a standard part of the local development stack. Treat them as another layer alongside your shell, package managers, and editor: something you install, configure, and learn to use deliberately.

What this looks like in practice:

- **Code in your editor** — inline completions and chat in VS Code, Cursor, JetBrains, or Positron
- **Code in your terminal** — CLI agents like Claude Code or Codex that can read, edit, and run commands in your project
- **Project-aware context** — assistants read your repo, understand your environment, and follow conventions you commit to files like `CLAUDE.md` or `.cursorrules`

A few habits that keep this useful instead of chaotic:

- Keep AI suggestions inside version control. If you can't `git diff` it, you can't review it.
- Pin which model and tool a project expects, the same way you pin a Python or Node version.
- Never paste secrets, student data, or private credentials into a hosted assistant. Use `.env` and a secret manager — see [Environment Variables and Secrets]({{ site.baseurl }}/environment-variables-and-secrets/).
- Read the diff before accepting it. The assistant is a collaborator, not an authority.

## Selecting models and token usage

AI assistants vary widely in capability, speed, and cost. Matching the right model to the task saves money and time.

**Model tiers:**
- **Fastest/cheapest** (e.g., Haiku 4.5, GPT-4o mini): Good for quick edits, inline completions, simple code generation. Use for routine tasks where speed matters more than nuance.
- **Mid-tier** (e.g., Sonnet 4.6): General-purpose work: refactoring, debugging, writing tests, explaining code. A solid default for most development.
- **Most capable** (e.g., Opus 4.7, Claude Pro): Complex tasks: multi-file refactors, designing systems, reviewing production incidents, teaching unfamiliar domains. Worth the cost when you need fewer iterations or better reasoning.

**Token usage basics:**
- Tokens are chunks of text (roughly 4 chars). Every message to the assistant uses tokens: your input and the generated output both count.
- Long conversations accumulate tokens fast. For APIs, track usage in logs; for hosted tools, check your account dashboard.
- Context windows vary: Haiku and Sonnet get 200K tokens, Opus gets 200K. Larger codebases or long chat histories consume context quickly.
- Cost scales with input + output tokens. A $0.005/1M input, $0.015/1M output model is cheap for reading code but expensive for generating long outputs.

**Practical strategies:**
- Start with a faster model for exploration; upgrade to a capable one if you need better results or fewer roundtrips.
- Summarize long conversations or close old chats instead of keeping them open forever.
- For recurring tasks (linting, PR reviews), use the most efficient model that does the job reliably — don't overshoot.
- In CLAUDE.md files, specify which model the project prefers, just like pinning a language version. This prevents surprise costs when teammates use different tools.
- If you're building an agent or API integration, consider a smaller model for high-volume tasks (logs, webhooks, summaries) and a larger one for code review or design.

## Extending AI Tools

Advanced users who use AI-enabled tools on a regular basis may wish to interact with external systems or data resources within the context of their work, delegate repetitive tasks to specialized agents, run automated workflows, or use reusable skills to perform work more efficiently. This is the universe of agentic AI, and there are exciting and powerful options to learn:

- **MCP (Model Context Protocol)** — A standard for tools like Claude Code, Cursor, and Codex to safely interact with external systems and data sources. MCPs extend what the assistant can see and do without copying secrets into the chat. Examples: reach out to a calendar system to find available meeting times and reserve rooms; query a company wiki or knowledge base for context while working on documentation; connect to an internal bug tracker to auto-link issues; interact with AWS services for infrastructure queries.

- **Agents** — Specialized personas that handle a specific task or domain. Agents are invoked on-demand and can perform complex, multi-step work autonomously. Examples: a senior code reviewer agent that checks conformity, optimization, error handling, and logging; a security review agent that scans PRs for common vulnerabilities; a PR summarization agent that reads diffs and writes clear summaries for stakeholders. You invoke the agent, it works, and reports back with results or fixes.

- **Skills** — Reusable prompts or tools for common, repeated tasks. Skills encapsulate best practices and domain knowledge into single commands. Examples: a commit-message skill that generates conventional commits from staged changes; a simplify skill that reviews code for unnecessary complexity and suggests refactors; a git-overview skill that runs pre-commit checks for debug artifacts; a claude-api skill that helps optimize Anthropic SDK code for caching and performance.

- **Hooks** — Automated workflows that execute before or after a specific event. Hooks run locally without user intervention, making them ideal for guardrails and efficiency. Examples: run a security scan before every commit; auto-format code after file save; run tests after a branch is pushed; check for hardcoded credentials or API keys.

- **Preferences** — A declarative document (like `.claude/settings.json` or `CLAUDE.md`) that establishes your architectural approach, coding conventions, style guide, tool constraints, and agentic behaviors. Instead of repeating guidance in every conversation, you write it once and all tools read it. Examples: "use async/await in TypeScript, not Promises"; "run database tests against a real DB, not mocks"; "before deploying, check the oncall dashboard at grafana.internal/d/api-latency"; "prefer Sonnet 4.6 for code review, Haiku 4.5 for quick edits".
