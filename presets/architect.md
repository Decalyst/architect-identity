# Project Context

> Edit this file with anything every agent should know about your project.
> It is injected into every agent's system prompt. Keep it focused — this
> runs on every call. Soft cap: ~4 KB.

## What this project is

A single-paragraph description of what this codebase is, who uses it, and
what success looks like. Keep it tight — every agent reads this on every
call, so earned clarity beats poetic prose.

## Stack

- **Languages:** e.g. TypeScript, Rust
- **Frameworks:** e.g. React, Tauri
- **Runtime / deployment:** e.g. Vercel, AWS Lambda, Tauri desktop bundle
- **Storage:** e.g. Postgres, SQLite, S3

## Architecture

The one or two architectural decisions that are load-bearing for this
project. Examples:

- "All IPC between frontend and backend goes through the commands.ts
  registry. Never call `invoke()` directly."
- "Every database write is wrapped in a transaction. No exceptions."
- "We use event sourcing for billing state. Don't mutate billing rows."

## Conventions

What's true *here* that isn't true everywhere else:

- Naming conventions for files, functions, database tables
- Test layout and conventions
- Error handling style (thrown errors vs. Result types vs. error codes)
- Import style (absolute vs relative, path aliases)

## Hard rules

- Never [X] — Reason: [Y]
- Always [X] — Reason: [Y]

Examples:
- Never add a dependency without checking the package manifest first.
- Never commit generated code to the repo.
- Always use the shared logger — no `console.log` in production paths.

## Domain knowledge

Vocabulary, business rules, things outsiders won't know. If an agent
could misinterpret a term (is "customer" a paying account or any user?),
define it here.

## Active constraints

- Performance budgets (bundle size, p99 latency)
- Compliance requirements (SOC2, GDPR, HIPAA)
- Deprecation deadlines (what's being removed and when)
