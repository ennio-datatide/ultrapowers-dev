# Ultrapowers Dev

Development skills library for the [ultrapowers](https://github.com/ennio-datatide/ultrapowers) workflow — best practices, agentic patterns, language idioms, and framework skills.

**Companion repos:**
- [ultrapowers](https://github.com/ennio-datatide/ultrapowers) — Workflow engine (brainstorming → research → planning → implementation)
- [ultrapowers-misc](https://github.com/ennio-datatide/ultrapowers-misc) — Non-dev skills (marketing, compliance, finance, communication)

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

## Category Skills (14) — Language-Agnostic

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

## Language Best Practices (11) — One Per Language

| Skill | Language | Ecosystem |
|-------|----------|-----------|
| `typescript-best-practices` | TypeScript | React, Next.js, Vue, Angular, Express, NestJS |
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

## Framework Skills (13) — Gap Fillers

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

## Agentic Patterns (7)

| Skill | What it covers |
|-------|---------------|
| `agent-loop` | Autonomous tool-calling agent loop |
| `orchestrator-workers` | Central orchestrator with specialized workers |
| `dag-workflows` | DAG workflows with shared state and conditional routing |
| `parallelization` | Fan-out/fan-in, voting, parallel analysis |
| `multi-agent-debate` | Multi-round debate with judge convergence |
| `multi-agent-handoffs` | Routing between specialized agents |
| `tool-calling` | Fundamental LLM tool calling pattern |

## Frontend & Design (3)

| Skill | Attribution |
|-------|-------------|
| `frontend-design` | Derived from [anthropics/skills](https://github.com/anthropics/skills) (MIT) |
| `react-best-practices` | Derived from [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) (MIT) |
| `web-design-guidelines` | Derived from [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) (MIT) |

## Official Skills We Reference (Don't Duplicate)

These frameworks have high-quality official skills — use those, not ours:

| Framework | Official Skill | Installs |
|-----------|---------------|----------|
| React | [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) | 221.6K |
| Vue | [antfu/skills](https://github.com/antfu/skills) | 10.7K |
| Nuxt | [antfu/skills](https://github.com/antfu/skills) + [onmax/nuxt-skills](https://github.com/onmax/nuxt-skills) | — |
| SwiftUI | [AvdLee/SwiftUI-Agent-Skill](https://github.com/AvdLee/SwiftUI-Agent-Skill) | 9.6K |
| React Native | [callstackincubator/agent-skills](https://github.com/callstackincubator/agent-skills) | 7.6K |
| Supabase | [supabase/agent-skills](https://github.com/supabase/agent-skills) | 37.7K |
| Playwright | [currents-dev/playwright-best-practices-skill](https://github.com/currents-dev/playwright-best-practices-skill) | 11.7K |

## Installation

```bash
# Claude Code
/plugin install ultrapowers-dev@ennio-datatide
```

## License

- **Original skills** — MIT License, Copyright (c) 2026 Datatide
- **Derived/forked skills** — Original license preserved (noted in each skill)
