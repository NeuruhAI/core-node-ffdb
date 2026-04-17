# core-node-ffdb

**Layer:** L1 State
**Version:** 0.1.0
**Part of:** NEURUH Convergence Protocol

## What This Is

Failover-First Database. Every write is durable before acknowledgement. Every state mutation is replicated to a quorum before the calling layer sees success. Designed so the Router can treat write persistence as a boolean invariant: either committed or never happened.

In the roads-funnel metaphor: the road itself refuses to let you proceed until your merge has been recorded on both sides of the interchange.

## Role In The Router

Aegis selects FFDB whenever an input shape has `compliance: >=soc2` or `domain: finance | real_estate` — any destination where partial writes are unacceptable.

## Contract

```ts
interface FFDB<K, V> {
  write(key: K, value: V): Promise<Committed>;
  read(key: K): Promise<V | null>;
  replicas(): ReplicaStatus[];
  health(): HealthStatus;
}
```

Every `write()` must return `Committed` or throw. There is no partial-success state.

## Depends On

- `ether-layer@0.1.0` (L0 Substrate) — replication transport + audit log

## Used By

- NATL world
- Signal-IQ world
- TaxShield world

## Status

Scaffolded. Implementation pending Router Spec v0.1 lock.

## License

Apache 2.0
