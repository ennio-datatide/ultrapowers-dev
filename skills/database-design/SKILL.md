---
name: Database Design
description: >
  Use when designing schemas, writing migrations, optimizing queries, choosing indexes,
  or deciding between normalization and denormalization.
---

# Database Design

Normalize by default, denormalize with intent. Every index speeds up reads and slows down writes -- choose deliberately.

## When to Use

- Designing a new schema or adding tables
- Optimizing slow queries
- Planning migrations for a production database
- Deciding whether to denormalize

## Normalization Quick Guide

| Normal Form | Rule | Violation Example |
|-------------|------|------------------|
| 1NF | No repeating groups, atomic values | `tags: "a,b,c"` in a single column |
| 2NF | No partial dependencies on composite keys | Non-key column depends on only part of the key |
| 3NF | No transitive dependencies | `order.customer_name` when you already have `customer_id` |

**Start at 3NF.** Denormalize only when you have measured query performance that justifies it.

## When to Denormalize

| Situation | Approach |
|-----------|----------|
| Read-heavy dashboard with expensive joins | Materialized view or summary table |
| Frequently accessed computed value | Store it, update on write |
| Cross-service data (can't join) | Duplicate what you need, sync via events |
| Reporting on historical data | Snapshot tables that don't change |

Always document *why* you denormalized and *how* consistency is maintained.

## Index Selection

| Query Pattern | Index Type |
|--------------|------------|
| Exact match (`WHERE status = 'active'`) | B-tree on `status` |
| Range query (`WHERE created_at > ?`) | B-tree on `created_at` |
| Multi-column filter (`WHERE user_id = ? AND status = ?`) | Composite index `(user_id, status)` |
| Full-text search | Full-text index or search engine |
| Existence check on nullable column | Partial index where column IS NOT NULL |

### Composite Index Order

Put the most selective (highest cardinality) column first, then range columns last:

```
-- Query: WHERE tenant_id = ? AND status = ? AND created_at > ?
-- Index: (tenant_id, status, created_at)
-- Equality columns first, range column last
```

## Migration Safety Checklist

| Step | Rule |
|------|------|
| Add column | Add as nullable or with default; never add NOT NULL to existing table without default |
| Remove column | Stop reading it first, deploy, then drop |
| Rename column | Add new, copy data, migrate readers, drop old |
| Add index | Use `CREATE INDEX CONCURRENTLY` if supported (avoids locking) |
| Change type | Add new column, migrate data, swap readers, drop old |

**Rule**: every migration must be reversible or have a documented rollback plan.

## Query Optimization Checklist

| Check | Action |
|-------|--------|
| Missing index | Run EXPLAIN, look for sequential scans on large tables |
| N+1 queries | Batch or join; load related data in one query |
| SELECT * | Select only the columns you need |
| Unbounded queries | Always use LIMIT; paginate results |
| Lock contention | Keep transactions short; avoid long-held locks |
| Unused indexes | Drop them -- they cost write performance for nothing |

## Schema Design Patterns

| Pattern | Use Case |
|---------|----------|
| Soft delete (`deleted_at`) | Need to recover data, audit trails |
| Polymorphic association | Multiple types share a relationship (use with caution) |
| Enum table | Reference table for status codes instead of raw strings |
| Audit log table | Append-only table tracking who changed what and when |
| Tenant ID on every table | Multi-tenant isolation at the row level |

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| No indexes on foreign keys | Add indexes on every FK column |
| Indexing every column "just in case" | Index based on actual query patterns |
| Storing money as floating point | Use integer cents or a decimal/numeric type |
| Running DDL without a migration tool | Use versioned, reviewable migration files |
| Giant transactions that lock many rows | Break into smaller batches, commit frequently |

## Attribution
**Original** -- Datatide, MIT licensed.
