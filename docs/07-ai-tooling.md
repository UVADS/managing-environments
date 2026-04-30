---
layout: default
title: AI Tooling
nav_order: 7
permalink: /ai-tooling/
---

# AI tooling

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
