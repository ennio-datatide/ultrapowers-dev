---
name: Design Patterns
description: >
  Use when making structural design decisions, applying SOLID principles, choosing between
  inheritance and composition, or deciding when to introduce an abstraction.
---

# Design Patterns

Prefer composition over inheritance, wait for three concrete cases before abstracting, and keep coupling low. Patterns are tools, not goals -- apply them when they solve a real problem.

## When to Use

- Structuring a new module or service
- Refactoring code that has grown rigid or tangled
- Deciding whether to introduce an interface, abstraction, or pattern
- Reviewing code for SOLID violations

## SOLID Quick Reference

| Principle | Rule | Smell When Violated |
|-----------|------|-------------------|
| Single Responsibility | A class/module has one reason to change | God objects, files over 300 lines |
| Open/Closed | Extend behavior without modifying existing code | Switch statements that grow with every feature |
| Liskov Substitution | Subtypes must be usable wherever the parent is expected | Overrides that throw "not supported" |
| Interface Segregation | Don't force clients to depend on methods they don't use | Interfaces with 10+ methods, many unused |
| Dependency Inversion | Depend on abstractions, not concretions | Hard-coded `new DatabaseClient()` inside business logic |

## The Rule of Three

> Don't abstract until you have three concrete cases.

| Situation | Action |
|-----------|--------|
| First occurrence | Write it inline, keep it simple |
| Second occurrence | Note the duplication, resist the urge |
| Third occurrence | Now extract -- you have enough cases to see the real pattern |

Premature abstraction creates the wrong abstraction. YAGNI (You Aren't Gonna Need It) until proven otherwise.

## Composition vs Inheritance

| Factor | Inheritance | Composition |
|--------|------------|-------------|
| Coupling | Tight -- child depends on parent internals | Loose -- depends on interface only |
| Flexibility | Fixed at compile time | Swappable at runtime |
| Depth limit | 2 levels before it hurts | No practical limit |
| Use when | True "is-a" with shared behavior | "Has-a" or "uses-a" relationships |

**Default to composition.** Use inheritance only for genuine type hierarchies with shared behavior (not just shared data).

## Essential Patterns

| Pattern | Problem It Solves | Example |
|---------|------------------|---------|
| Strategy | Swappable algorithms | Different pricing calculators behind one interface |
| Observer | Decoupled event notification | UI reacts to data changes without polling |
| Factory | Complex object creation | Build objects without exposing construction logic |
| Adapter | Incompatible interfaces | Wrap a third-party API to match your internal contract |
| Repository | Data access abstraction | Business logic doesn't know if data is in SQL or an API |
| Builder | Complex construction with many optional params | Fluent object construction with defaults |

## DDD Core Concepts

| Concept | What It Is | Guideline |
|---------|-----------|-----------|
| Entity | Object with identity that persists | Has an ID, equality by ID |
| Value Object | Object defined by its attributes | Immutable, equality by value |
| Aggregate | Cluster of entities with a root | All mutations go through the root |
| Bounded Context | Boundary where a model applies | Same word can mean different things in different contexts |
| Ubiquitous Language | Shared vocabulary with domain experts | Code names match business terms |

Use DDD concepts when the domain is complex enough to justify it. For CRUD apps, it's overhead.

## When to Introduce an Abstraction

| Signal | Action |
|--------|--------|
| Three implementations of the same interface shape | Extract the interface |
| You need to swap implementations (test, prod, vendor) | Introduce an abstraction boundary |
| A module depends on concrete infrastructure details | Invert the dependency |
| You *might* need flexibility someday | Wait. Don't abstract speculatively. |

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Abstracting on the first occurrence | Wait for the Rule of Three |
| Deep inheritance hierarchies (3+ levels) | Flatten with composition |
| Pattern for pattern's sake | Only apply a pattern when it solves a concrete problem |
| Anemic domain models (data bags + service classes) | Put behavior on the objects that own the data |
| God class that does everything | Split by responsibility, one reason to change per class |

## Attribution
**Original** -- Datatide, MIT licensed.
