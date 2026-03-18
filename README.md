# Ultrapowers Dev

54 development skills for your coding agents — language best practices for 13 languages, 12 framework patterns, 7 agentic patterns, and architecture fundamentals. A companion plugin to [Ultrapowers](https://github.com/ennio-datatide/ultrapowers).

**[Documentation](https://www.datatide.com/ultrapowers)** · **[GitHub](https://github.com/ennio-datatide/ultrapowers-dev)** · **[Issues](https://github.com/ennio-datatide/ultrapowers-dev/issues)**

## How it works

These skills give your coding agent deep expertise across languages, frameworks, and architectural patterns. When your agent encounters a React component, a FastAPI endpoint, or a Rust service, it automatically applies the right patterns and best practices.

Each skill is self-contained and triggers automatically when relevant. No special commands needed — your agent just has development superpowers.

## Example

> "Refactor our Express API to FastAPI."

The agent automatically applies express-patterns to understand the existing code, python-best-practices and fastapi-patterns for the migration, api-design for endpoint conventions, error-handling for proper Result patterns, and testing-tdd to ensure every endpoint has coverage before and after the switch.

## Installation

### Claude Code (via Ultrapowers Marketplace)

Register the marketplace first (one time):

```bash
/plugin marketplace add ennio-datatide/ultrapowers
```

Then install:

```bash
/plugin install ultrapowers-dev@ultrapowers
```

### From Source

```bash
git clone https://github.com/ennio-datatide/ultrapowers-dev.git
```

### Verify Installation

Start a new session and ask for something that should trigger a skill (for example, "build a FastAPI endpoint" or "review this React component"). The agent should automatically invoke the relevant skill.

## What's Inside

### Category Skills (14) — Language-Agnostic

| Skill | What it covers |
|-------|---------------|
| `testing-tdd` | TDD cycle, test design, fixtures, mocking, coverage |
| `error-handling` | Exception/Result patterns, validation, degradation |
| `design-patterns` | SOLID, DDD, composition, separation of concerns |
| `architecture` | Monolith, microservices, hexagonal, clean, event-driven |
| `database-design` | Schema design, migrations, indexing, optimization |
| `caching` | Cache strategies, invalidation, TTL, write-through |
| `api-design` | REST/GraphQL conventions, versioning, pagination |
| `observability` | Structured logging, metrics, distributed tracing |
| `resilience` | Retries, circuit breakers, timeouts, backoff |
| `auth-security` | Authentication, authorization, secrets, OWASP |
| `background-jobs` | Task queues, workers, event-driven, idempotency |
| `rag-ai` | RAG pipelines, embeddings, vector search, chunking |
| `ci-cd` | Pipeline design, deployment strategies, rollback |
| `type-safety` | Type systems, generics, contracts, strict checking |

### Language Best Practices (13) — One Per Language

| Skill | Language | Ecosystem |
|-------|----------|-----------|
| `typescript-best-practices` | TypeScript | React, Next.js, Vue, Angular, Express, NestJS |
| `javascript-best-practices` | JavaScript | ES2024+, tooling, project structure |
| `python-best-practices` | Python | FastAPI, Django, Flask |
| `rust-best-practices` | Rust | Axum, Actix, Tokio |
| `go-best-practices` | Go | Gin, Echo, Fiber |
| `java-best-practices` | Java | Spring Boot, Quarkus |
| `csharp-best-practices` | C# | ASP.NET, Blazor, EF Core |
| `php-best-practices` | PHP | Laravel, Symfony |
| `ruby-best-practices` | Ruby | Rails, Sinatra |
| `swift-best-practices` | Swift | SwiftUI, UIKit |
| `kotlin-best-practices` | Kotlin | Spring Boot, Ktor, Compose |
| `dart-best-practices` | Dart | Flutter |
| `c-cpp-best-practices` | C / C++ | CMake, systems programming |
| `sql-best-practices` | SQL | PostgreSQL, MySQL, SQLite |

### Framework Patterns (12) — Gap Fillers

Frameworks where no official skill exists. Each language skill points to these.

| Skill | Framework | Why we wrote it |
|-------|-----------|----------------|
| `fastapi-patterns` | FastAPI | Only partial community skill existed |
| `django-patterns` | Django | No official skill — major gap |
| `flask-patterns` | Flask | No official skill |
| `express-patterns` | Express.js | No official skill |
| `rails-patterns` | Ruby on Rails | No official skill — major gap |
| `angular-patterns` | Angular | No official skill — major gap |
| `laravel-patterns` | Laravel | Only an external plugin existed |
| `nestjs-patterns` | NestJS | Partial community skill, low quality |
| `nextjs-patterns` | Next.js | Complements [vercel-labs/next-skills](https://github.com/vercel-labs/next-skills) |
| `spring-boot-patterns` | Spring Boot | Complements [github/awesome-copilot](https://github.com/github/awesome-copilot) |
| `supabase-patterns` | Supabase | Complements [supabase/agent-skills](https://github.com/supabase/agent-skills) |
| `tailwind-patterns` | Tailwind CSS | Complements community skill |

### Agentic Patterns (7)

| Skill | What it covers |
|-------|---------------|
| `agent-loop` | Autonomous tool-calling agent loop |
| `orchestrator-workers` | Central orchestrator with specialized workers |
| `dag-workflows` | DAG workflows with shared state and conditional routing |
| `parallelization` | Fan-out/fan-in, voting, parallel analysis |
| `multi-agent-debate` | Multi-round debate with judge convergence |
| `multi-agent-handoffs` | Routing between specialized agents |
| `tool-calling` | Fundamental LLM tool calling pattern |

### Frontend & Design (4)

| Skill | Attribution |
|-------|-------------|
| `frontend-design` | Derived from [anthropics/skills](https://github.com/anthropics/skills) (MIT) |
| `react-best-practices` | Derived from [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) (MIT) |
| `react-patterns` | Canonical React patterns for component design, hooks, and state |
| `web-design-guidelines` | Derived from [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) (MIT) |

### TUI Development (1)

| Skill | What it covers |
|-------|---------------|
| `ratatui-patterns` | Ratatui app architecture (TEA), async event loops, tui-term PTY rendering, pane management, axum co-running, color theming, snapshot testing |

### Plugin Development (1)

| Skill | What it covers |
|-------|---------------|
| `plugin-development` | Plugin structure, skill authoring, marketplace setup, versioning, multi-platform distribution |

### Browser & E2E (2)

| Skill | What it covers |
|-------|---------------|
| `browser-automation` | Puppeteer, Playwright, headless browsers |
| `e2e-testing` | End-to-end test strategies, selectors, CI integration |

## Official Skills We Reference (Don't Duplicate)

These frameworks have high-quality official skills — use those, not ours:

| Framework | Official Skill |
|-----------|---------------|
| React | [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) |
| Vue | [antfu/skills](https://github.com/antfu/skills) |
| Nuxt | [antfu/skills](https://github.com/antfu/skills) + [onmax/nuxt-skills](https://github.com/onmax/nuxt-skills) |
| SwiftUI | [AvdLee/SwiftUI-Agent-Skill](https://github.com/AvdLee/SwiftUI-Agent-Skill) |
| React Native | [callstackincubator/agent-skills](https://github.com/callstackincubator/agent-skills) |
| Supabase | [supabase/agent-skills](https://github.com/supabase/agent-skills) |
| Playwright | [currents-dev/playwright-best-practices-skill](https://github.com/currents-dev/playwright-best-practices-skill) |

## Attribution

We believe in giving credit where it's due. Each skill has an attribution section:

- **Original** — Written by Datatide, MIT licensed
- **Inspired by [source]** — Our own implementation informed by another skill, with link
- **Derived from [source]** — Modified version, original attribution and license preserved
- **Forked from [source]** — Minimal changes, original license applies

### Credits

- **[Anthropic](https://github.com/anthropics/skills)** (MIT) — Frontend design inspiration
- **[Vercel](https://github.com/vercel-labs/agent-skills)** (MIT) — React best practices, web design guidelines
- **[Jesse Vincent / obra](https://github.com/obra/superpowers)** (MIT) — TDD methodology inspiration
- **[Anthropic Docs](https://docs.anthropic.com/en/docs/build-with-claude/agent-patterns)** — Agent pattern documentation
- **[Supabase](https://github.com/supabase/agent-skills)** — Supabase patterns reference
- **[antfu](https://github.com/antfu/skills)** — Vue/Vite/Vitest skills reference

## Companion Plugins

- **[ultrapowers](https://github.com/ennio-datatide/ultrapowers)** — Core workflow engine (brainstorming → research → planning → implementation)
- **[ultrapowers-business](https://github.com/ennio-datatide/ultrapowers-business)** — 38 business skills (marketing, compliance, finance, communication)

## Updating

```bash
/plugin update ultrapowers-dev
```

## Contributing

Skills live directly in this repository. To contribute:

1. Fork the repository
2. Create a branch for your skill
3. Submit a PR

## License

- **Original skills** — MIT License, Copyright (c) 2026 Datatide
- **Derived/forked skills** — Original license preserved (noted in each skill)

## Community

Built by [Ennio Maldonado](https://www.enniomaldonado.com) at [Datatide](https://www.datatide.com).

- **Docs**: https://www.datatide.com/ultrapowers
- **Issues**: https://github.com/ennio-datatide/ultrapowers-dev/issues
