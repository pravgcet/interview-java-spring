
# Caching Policies

In caching, **policies** are rules or strategies that govern **how data is stored, retrieved, and evicted** from the cache.

---

## 1. Eviction Policies

These determine **which cache entries to remove** when the cache reaches its maximum size.

| Policy | Description |
|--------|-------------|
| **LRU (Least Recently Used)** | Evicts the least recently accessed item. |
| **LFU (Least Frequently Used)** | Evicts the item accessed the fewest times. |
| **FIFO (First In First Out)** | Evicts items in the order they were added. |
| **MRU (Most Recently Used)** | Opposite of LRU; evicts the most recently accessed item. |
| **Random Replacement** | Evicts a random entry from the cache. |
| **Clock / Second-Chance** | Approximation of LRU using a circular list and reference bits. |

---

## 2. Expiration Policies

These determine **how long** a cache entry stays valid.

| Policy | Description |
|--------|-------------|
| **TTL (Time to Live)** | Entry is removed after a fixed time, regardless of access. |
| **TTI (Time to Idle)** | Entry expires if not accessed for a certain duration. |
| **Absolute Expiration** | Entry is valid until a specific timestamp. |
| **Sliding Expiration** | Resets expiration time upon each access. |

---

## 3. Write Policies

These define **when and how** data is written to the underlying data store.

| Policy | Description |
|--------|-------------|
| **Write-Through** | Writes data to the cache and backing store simultaneously. |
| **Write-Around** | Writes data only to the backing store, bypassing the cache. |
| **Write-Behind (Write-Back)** | Writes data only to the cache initially, then asynchronously updates the backing store. |

---

## 4. Read Policies

These define **how the cache handles data reads**.

| Policy | Description |
|--------|-------------|
| **Cache-Aside (Lazy Loading)** | Application checks cache first, then loads from DB and populates cache if missed. |
| **Read-Through** | Cache automatically fetches from DB on a miss. |
| **Refresh-Ahead** | Proactively refreshes cache entries before they expire. |

---

## Summary Table

| Category | Examples |
|----------|----------|
| **Eviction** | LRU, LFU, FIFO, MRU |
| **Expiration** | TTL, TTI, Sliding Expiration |
| **Write** | Write-Through, Write-Around, Write-Behind |
| **Read** | Cache-Aside, Read-Through, Refresh-Ahead |
