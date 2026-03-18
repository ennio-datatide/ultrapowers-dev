---
name: API Design
description: >
  Use when designing REST APIs, choosing URL structures, handling errors in responses,
  implementing pagination, or planning API versioning.
---

# API Design

Design APIs for the consumer, not the database. Consistent conventions, clear errors, and predictable behavior matter more than cleverness.

## When to Use

- Designing a new API or adding endpoints
- Standardizing error responses across a service
- Implementing pagination, filtering, or sorting
- Planning versioning strategy for an existing API

## REST URL Conventions

| Pattern | Example | Rule |
|---------|---------|------|
| Collection | `GET /users` | Plural nouns, never verbs |
| Single resource | `GET /users/42` | ID in path |
| Nested resource | `GET /users/42/orders` | One level deep max |
| Action (when needed) | `POST /orders/42/cancel` | Verb only when CRUD doesn't fit |
| Filtering | `GET /users?status=active` | Query params for filters |

**Avoid**: deeply nested URLs (`/users/42/orders/7/items/3/reviews`). After two levels, promote the resource to a top-level endpoint with a filter.

## HTTP Methods

| Method | Semantics | Idempotent | Request Body |
|--------|-----------|------------|--------------|
| GET | Read | Yes | No |
| POST | Create | No | Yes |
| PUT | Full replace | Yes | Yes |
| PATCH | Partial update | Yes | Yes (partial) |
| DELETE | Remove | Yes | No |

## Status Codes That Matter

| Code | Meaning | When to Use |
|------|---------|-------------|
| 200 | OK | Successful read or update |
| 201 | Created | Successful creation (return the resource + Location header) |
| 204 | No Content | Successful delete, nothing to return |
| 400 | Bad Request | Validation failed, malformed input |
| 401 | Unauthorized | Missing or invalid authentication |
| 403 | Forbidden | Authenticated but not permitted |
| 404 | Not Found | Resource doesn't exist |
| 409 | Conflict | Duplicate or state conflict |
| 422 | Unprocessable Entity | Semantically invalid (valid JSON, wrong values) |
| 429 | Too Many Requests | Rate limit exceeded |
| 500 | Internal Server Error | Unexpected failure (don't expose details) |

## Error Response Format

Use a consistent structure across all endpoints:

```json
{
  "error": {
    "code": "VALIDATION_FAILED",
    "message": "Human-readable summary",
    "details": [
      { "field": "email", "issue": "must be a valid email address" }
    ]
  }
}
```

**Rules**: always include a machine-readable code. Never expose stack traces or internal details in production.

## Pagination

| Style | Mechanism | Best For |
|-------|-----------|----------|
| Offset | `?page=3&per_page=20` | Simple, supports "jump to page" |
| Cursor | `?cursor=abc123&limit=20` | Large datasets, real-time feeds, stable under inserts |

Return pagination metadata in the response body:

```json
{
  "data": [...],
  "pagination": {
    "next_cursor": "abc123",
    "has_more": true
  }
}
```

**Default**: cursor-based for anything that grows or changes frequently. Offset pagination breaks when rows are inserted during traversal.

## Versioning

| Strategy | Example | Trade-off |
|----------|---------|-----------|
| URL path | `/v1/users` | Simple, obvious, but hard to migrate |
| Header | `Accept: application/vnd.api+json;version=2` | Clean URLs but less discoverable |
| No versioning | Evolve carefully, don't break | Best if you control all clients |

**Practical default**: URL path versioning (`/v1/`). Only bump the version for breaking changes. Additive changes (new fields, new endpoints) don't require a new version.

## Rate Limiting

Return rate limit info in headers so clients can self-regulate:

```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 42
X-RateLimit-Reset: 1609459200
```

Return `429` with a `Retry-After` header when the limit is exceeded.

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Verbs in URLs (`/getUsers`, `/createOrder`) | Use nouns + HTTP methods |
| Returning 200 for errors with error in body | Use proper HTTP status codes |
| Inconsistent error formats across endpoints | Define one error schema, use it everywhere |
| No pagination on list endpoints | Always paginate; unbounded lists break at scale |
| Breaking changes without version bump | Additive only in current version; new version for removals |
| Exposing internal IDs or database structure | Use stable public identifiers, don't mirror table names |

## Attribution
**Original** -- Datatide, MIT licensed.
