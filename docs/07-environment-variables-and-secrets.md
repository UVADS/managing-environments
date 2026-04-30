---
layout: default
title: Environment Variables and Secrets
nav_order: 7
permalink: /environment-variables-and-secrets/
---

# Environment variables and secrets

What an environment variable is, and the three places they typically live:

1. **Shell rc files** (`~/.zshrc`) — for things you want everywhere
2. **Project `.env` files** — for per-project config; loaded by `python-dotenv`, `direnv`, or your framework
3. **Secret managers** — 1Password CLI, AWS Secrets Manager, etc., for anything sensitive

Rules:

- Never commit `.env` files. Add them to `.gitignore`.
- Provide a committed `.env.example` showing required keys with empty values.
- Treat API keys, database URLs, and tokens as secrets even in coursework.
