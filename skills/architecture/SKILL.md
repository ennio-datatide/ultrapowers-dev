---
name: Architecture
description: >
  Use when making system-level architecture decisions, choosing between monolith and microservices,
  selecting architectural patterns, or designing system boundaries.
---

# Architecture

Start with a monolith, extract services only when forced by concrete scaling, team, or deployment constraints. Architecture is about trade-offs, not ideals.

## When to Use

- Starting a new system or major feature
- Evaluating whether to split a monolith
- Choosing between architectural patterns (hexagonal, event-driven, CQRS)
- Reviewing system boundaries and communication patterns

## Monolith vs Microservices Decision

| Factor | Stay Monolith | Consider Splitting |
|--------|--------------|-------------------|
| Team size | < 20 engineers | Independent teams own independent services |
| Deployment | Single deploy pipeline works fine | One module's deploys block another's |
| Scaling | Uniform load, scale the whole thing | One component needs 10x the resources |
| Data | Shared database is manageable | Modules need fundamentally different data stores |
| Complexity | Business logic is interconnected | Clear bounded contexts with minimal cross-talk |

**Default**: monolith with clean internal boundaries (modular monolith). You can always extract later; merging microservices back is painful.

## Architectural Patterns

| Pattern | Core Idea | Best For |
|---------|-----------|----------|
| Layered | UI -> Service -> Repository -> DB | Simple CRUD apps, small teams |
| Hexagonal (Ports & Adapters) | Business logic at center, adapters at edges | Systems with multiple integrations |
| Clean Architecture | Dependency arrows point inward | Complex domains needing testability |
| Event-Driven | Components communicate via events | Decoupled workflows, audit trails |
| CQRS | Separate read and write models | Read-heavy systems with complex queries |

## Hexagonal Architecture

```
[External World]
    |
[Adapter] -- implements --> [Port (interface)]
                                  |
                          [Business Logic Core]
                                  |
                          [Port (interface)] <-- implements -- [Adapter]
                                                                  |
                                                          [Database / API]
```

The core knows nothing about HTTP, databases, or frameworks. Adapters translate between the outside world and the core's ports.

## Event-Driven Patterns

| Pattern | Flow | Use When |
|---------|------|----------|
| Event Notification | Fire and forget, subscribers react | Loose coupling, eventual consistency is OK |
| Event-Carried State | Event contains all data needed | Subscribers shouldn't query back |
| Event Sourcing | Store events as source of truth | Need full audit trail, time-travel debugging |

## CQRS Guidelines

| Aspect | Command Side | Query Side |
|--------|-------------|------------|
| Model | Optimized for writes and validation | Optimized for reads and display |
| Storage | Normalized, consistent | Denormalized, eventually consistent |
| Complexity | Worth it when read/write models diverge significantly |

Don't adopt CQRS unless your read and write models are genuinely different. For most apps, one model is simpler and sufficient.

## Service Communication

| Method | Coupling | Consistency | Use When |
|--------|---------|-------------|----------|
| Synchronous (HTTP/gRPC) | Higher | Strong | Request/response, real-time needs |
| Async messaging (queue) | Lower | Eventual | Background work, cross-service events |
| Shared database | Highest | Strong | Avoid in distributed systems |

## Boundary Design Rules

1. **One team, one service** -- organizational boundaries drive service boundaries
2. **Share contracts, not code** -- APIs and schemas, not libraries
3. **Own your data** -- each service owns its datastore, no shared databases
4. **Design for failure** -- every network call can fail; handle it

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Starting with microservices on day one | Start monolith, extract when pain is concrete |
| Distributed monolith (services that must deploy together) | If they can't deploy independently, merge them |
| Sharing a database between services | Each service owns its data; sync via events or APIs |
| Choosing architecture based on resume appeal | Choose based on team size, problem complexity, and constraints |
| No clear module boundaries in the monolith | Define internal boundaries now so extraction is possible later |

## Attribution
**Original** -- Datatide, MIT licensed.
