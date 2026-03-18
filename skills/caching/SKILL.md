---
name: Caching
description: >
  Use when adding caching to a system, choosing cache strategies, designing invalidation logic,
  or diagnosing cache-related bugs.
---

# Caching

Cache the right thing at the right layer with the right TTL. The two hardest problems in caching are invalidation and knowing when not to cache at all.

## When to Use

- A read path is slow and the data doesn't change on every request
- Reducing load on a database or external API
- Choosing between caching strategies
- Debugging stale data or inconsistency issues

## Caching Strategies

| Strategy | How It Works | Best For |
|----------|-------------|----------|
| Cache-Aside | App checks cache, on miss reads from source and populates cache | General purpose, most common |
| Read-Through | Cache itself fetches from source on miss | When cache layer manages population |
| Write-Through | Writes go to cache and source synchronously | Strong consistency needs |
| Write-Behind | Writes go to cache, async flush to source | High write throughput, eventual consistency OK |
| Refresh-Ahead | Cache proactively refreshes before expiry | Predictable access patterns, low-latency reads |

**Default choice**: cache-aside. It's simple, explicit, and you control both read and write paths.

## Cache-Aside Flow

```
read(key):
  value = cache.get(key)
  if value is null:
    value = database.get(key)
    cache.set(key, value, ttl=300)
  return value

write(key, value):
  database.set(key, value)
  cache.delete(key)          // Invalidate, don't update
```

**Delete on write, don't update.** Updating the cache risks race conditions where a stale write overwrites a newer one.

## Invalidation Strategies

| Strategy | Mechanism | Trade-off |
|----------|-----------|-----------|
| TTL-based | Key expires after fixed duration | Simple but serves stale data until expiry |
| Event-based | Delete cache on write/update events | Consistent but requires event infrastructure |
| Version-based | Key includes version number, bump on change | Good for static assets, manual management |
| Purge on deploy | Clear cache on each deployment | Safe for config/template caches |

## TTL Guidelines

| Data Type | Suggested TTL | Rationale |
|-----------|--------------|-----------|
| User session | 15-30 minutes | Security and freshness |
| API response (external) | 60-300 seconds | Reduce upstream load |
| Configuration / feature flags | 30-60 seconds | Balance freshness with read speed |
| Static assets | Hours to days | Versioned URLs handle invalidation |
| Computed aggregates | Depends on staleness tolerance | Regenerate on schedule or event |

## When Caching Hurts

| Scenario | Why It Hurts |
|----------|-------------|
| Write-heavy, read-once data | Cache churn with no read benefit |
| Highly personalized data (unique per user) | Low hit rate, memory wasted |
| Data that must be real-time consistent | Stale cache causes correctness bugs |
| Cache is same speed as source | Adds complexity without performance gain |
| Thundering herd on cold cache | All requests hit the source simultaneously |

## Thundering Herd Prevention

| Technique | How It Works |
|-----------|-------------|
| Lock/mutex on cache miss | One request populates, others wait |
| Stale-while-revalidate | Serve expired value while refreshing in background |
| Request coalescing | Deduplicate concurrent requests for the same key |
| Warm-up on deploy | Pre-populate cache before serving traffic |

## Cache Key Design

- Include all parameters that affect the result: `users:{id}:profile`
- Include version if schema changes: `v2:users:{id}`
- Avoid unbounded keys (e.g., full query strings) -- normalize first
- Use namespaces to enable bulk invalidation: `tenant:{tid}:*`

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Caching without a TTL | Always set a TTL -- even a long one prevents infinite stale data |
| Updating cache on write instead of deleting | Delete on write; let the next read repopulate |
| Caching errors or empty results | Cache only successful responses; use short TTL for "not found" if needed |
| No monitoring on hit/miss ratio | Track hit rate -- below 80% means your cache isn't helping |
| Ignoring cold-start behavior | Plan for empty cache: warm-up, rate limiting, or stale-while-revalidate |

## Attribution
**Original** -- Datatide, MIT licensed.
