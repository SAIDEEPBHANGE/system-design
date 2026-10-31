# 03 Caching

```mermaid
mindmap
  root((Caching))
    Layers
      Client
      CDN
      Web server
      App cache
      DB cache
    Write strategies
      Cache-aside
      Write-through
      Write-behind
      Refresh-ahead
    Eviction
      LRU
      LFU
      FIFO
      TTL
    Problems
      Invalidation
      Stampede
      Stale data
```

## Why cache
- Memory is about 100x faster than SSD, thousands of times faster than a network call to a DB.
- Reduces DB load and latency.
- Works only if reads >> writes and data is reused.

## Layers (closest to user first)
- Client/browser, CDN, reverse proxy, application cache (Redis/Memcached), database cache.

## Strategies
- **Cache-aside (lazy):** app checks cache, on miss reads DB then fills cache.
  - Pros: only requested data cached, cache failure is survivable
  - Cons: first request slow, data can go stale
- **Write-through:** write to cache and DB together.
  - Pros: cache always fresh
  - Cons: slower writes, caches data that may never be read
- **Write-behind:** write to cache, DB updated later (async).
  - Pros: fast writes
  - Cons: data loss if cache dies before flush
- **Refresh-ahead:** auto-refresh hot items before expiry.
  - Cons: wrong prediction wastes resources

## Eviction
- **LRU:** drop least recently used. Default choice.
- **LFU:** drop least frequently used. Good for stable hot sets.
- **FIFO:** simple, rarely best.
- **TTL:** expire after time. Always set one.

## Typical Problems
- **Invalidation:** the hardest part. Options: TTL, delete on write, versioned keys.
- **Cache stampede:** a hot key expires and thousands hit the DB. Fix: locking, jittered TTL, refresh-ahead.
- **Stale reads:** accept it or use write-through.
- **Cold start:** empty cache after restart floods the DB. Warm it.
- **Not worth it when:** data changes constantly or is rarely re-read.

## Connects to
- CDN is edge caching → [02 networking](02-networking-and-load-balancing.md)
- Consistency cost → [01 consistency](01-fundamentals.md)
- Reduces DB load before sharding → [04 databases](04-databases.md)
- Hit ratio math → [06 estimation](06-estimation-and-numbers.md)
