# Ultrapowers Skills

A library of development best practices and agentic pattern skills for the [ultrapowers](https://github.com/ennio-datatide/ultrapowers) workflow.

## Attribution

We believe in giving credit where it's due. Each skill has an attribution section:

- **Original** — Written by Datatide, MIT licensed
- **Inspired by [source]** — Our own implementation informed by another skill, with link to original
- **Derived from [source]** — Modified version of another skill, original attribution and license preserved
- **Forked from [source]** — Minimal changes from original, original license applies

### Credits

- **[Anthropic](https://github.com/anthropics/skills)** (MIT) — Frontend design, webapp testing, MCP patterns
- **[Vercel](https://github.com/vercel-labs/agent-skills)** (MIT) — React best practices, web design guidelines, composition patterns
- **[Jesse Vincent / obra](https://github.com/obra/superpowers)** (MIT) — TDD methodology, systematic debugging, skill authoring
- **[Anthropic](https://docs.anthropic.com/en/docs/build-with-claude/agent-patterns)** — Agent pattern documentation that informed our agentic skills

## Skill Categories

### Category Skills (Language-Agnostic)

Universal patterns that apply regardless of language.

| Skill | What it covers | Attribution |
|-------|---------------|-------------|
| `testing-tdd` | TDD cycle, test design, fixtures, mocking, coverage | Original |
| `error-handling` | Exception/Result patterns, validation, degradation | Original |
| `design-patterns` | SOLID, DDD, composition, separation of concerns | Original |
| `architecture` | Monolith, microservices, hexagonal, clean, event-driven | Original |
| `database-design` | Schema design, migrations, indexing, optimization | Original |
| `caching` | Cache strategies, invalidation, TTL, write-through | Original |
| `api-design` | REST/GraphQL conventions, versioning, pagination | Original |
| `observability` | Structured logging, metrics, distributed tracing | Original |
| `resilience` | Retries, circuit breakers, timeouts, backoff | Original |
| `auth-security` | Authentication, authorization, secrets, OWASP | Original |
| `background-jobs` | Task queues, workers, event-driven, idempotency | Original |
| `rag-ai` | RAG pipelines, embeddings, vector search, chunking | Original |
| `ci-cd` | Pipeline design, deployment strategies, rollback | Original |
| `type-safety` | Type systems, generics, contracts, strict checking | Original |

### Language Best Practices (One Per Language)

Language-specific idioms, tooling, and conventions.

| Skill | Language | Attribution |
|-------|----------|-------------|
| `rust-best-practices` | Rust | Original |
| `python-best-practices` | Python | Original |
| `typescript-best-practices` | TypeScript | Inspired by [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) |

### Agentic Patterns

Patterns for building AI agent systems.

| Skill | What it covers | Attribution |
|-------|---------------|-------------|
| `agent-loop` | Autonomous tool-calling agent loop | Original, inspired by [Anthropic agent patterns](https://docs.anthropic.com/en/docs/build-with-claude/agent-patterns) |
| `orchestrator-workers` | Central orchestrator with specialized workers | Original, inspired by Anthropic agent patterns |
| `dag-workflows` | DAG workflows with shared state and conditional routing | Original |
| `parallelization` | Fan-out/fan-in, voting, parallel analysis | Original, inspired by Anthropic agent patterns |
| `multi-agent-debate` | Multi-round debate with judge convergence | Original |
| `multi-agent-handoffs` | Routing between specialized agents | Original, inspired by Anthropic agent patterns |
| `tool-calling` | Fundamental LLM tool calling pattern | Original, inspired by Anthropic agent patterns |

### Frontend & Design

| Skill | What it covers | Attribution |
|-------|---------------|-------------|
| `frontend-design` | UI/UX aesthetics, design thinking, anti-patterns | Derived from [anthropics/skills](https://github.com/anthropics/skills) (MIT) |
| `react-best-practices` | React patterns, performance, composition | Derived from [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) (MIT) |
| `web-design-guidelines` | Web interface design standards | Derived from [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) (MIT) |

## Installation

### Claude Code

```bash
/plugin install ultrapowers-skills@ennio-datatide
```

## Contributing

Each skill follows the format: `skills/<skill-name>/SKILL.md`

Always include an attribution section in your skill if it was informed by external work.

## License

- **Original skills** — MIT License, Copyright (c) 2026 Datatide
- **Derived/forked skills** — Original license preserved (noted in each skill)

See LICENSE file and individual skill attribution sections.
