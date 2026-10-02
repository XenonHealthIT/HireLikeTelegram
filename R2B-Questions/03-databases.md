# R2B: Databases

## B12 — On-Call Scheduling Write Skew

**Source:** PostgreSQL documentation, [Transaction Isolation](https://www.postgresql.org/docs/current/transaction-iso.html).

### Candidate prompt

Two doctors are on call. Business policy requires at least one to remain on call. Two concurrent transactions each read both rows, see the other doctor available, and set their own row to `off`. Under snapshot-style repeatable read, both may commit because they update different rows.

Name the anomaly, explain why repeatable reads alone do not protect the invariant, and provide three valid designs that preserve it.

### Proposed answer

This is write skew: both transactions make decisions from compatible snapshots and write disjoint rows, producing a final state that cannot satisfy the cross-row invariant. Stable snapshots prevent reread changes but do not necessarily serialize predicate-dependent writes.

Valid designs include PostgreSQL Serializable isolation with retry of serialization failures; locking a shared schedule/shift row with `SELECT ... FOR UPDATE` before checking/updating doctors; or representing the invariant so conflicting changes touch a common row or are enforced by a carefully designed constraint/transaction. An application advisory lock keyed by shift can also serialize decisions if every writer obeys it. Merely locking each doctor's own row is insufficient.

### Key points

- The invariant spans rows, while each transaction writes only one row.
- Serializable callers must retry the entire transaction, using bounded retry policy.
- A normal check constraint on an individual row cannot express the cross-row condition.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Identifies and explains write skew | 3 |
| Explains why disjoint writes both commit | 2 |
| Gives three sound invariant-preserving designs | 3 |
| Includes full-transaction retry for Serializable | 1 |
| Rejects ineffective own-row locking | 1 |

## B13 — Database Deadlock Under Load

**Source:** PostgreSQL documentation, [Explicit Locking and Deadlocks](https://www.postgresql.org/docs/current/explicit-locking.html).

### Candidate prompt

Transaction T1 updates customer 10 and then customer 20. T2 updates customer 20 and then customer 10. Under load, PostgreSQL aborts one with a deadlock error. The application converts that error into HTTP 500 without retry.

Explain detection and victim behavior. Propose prevention, retry, and observability practices. Why is simply increasing the lock timeout not a fix?

### Proposed answer

Each transaction holds a row lock required by the other, creating a wait-for cycle. PostgreSQL detects the deadlock and aborts one transaction so the other can progress; all work in the victim transaction must be rolled back.

Prevent most occurrences by acquiring locks in a stable global order, for example sorting customer IDs before updates, keeping transactions short, and avoiding user/network waits while locks are held. Still handle deadlock/serialization SQL states by rolling back and retrying the entire idempotent transaction with bounded randomized backoff. Cap attempts and surface a retryable failure when exhausted. Observe victim counts, lock wait duration, transaction age, involved queries/resources, and traces. A longer timeout merely prolongs the cycle until detection or timeout and can worsen resource occupancy.

### Key points

- Retrying only the failed statement is unsafe because the transaction is aborted and its prior reads/writes formed one unit.
- Lock ordering reduces deadlocks but cannot guarantee none across every dependency.
- External side effects should not occur irreversibly inside a retried unit without an outbox/idempotency design.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct wait-cycle and victim rollback explanation | 3 |
| Stable lock ordering and short transactions | 2 |
| Full-transaction bounded retry | 2 |
| Handles external-side-effect/idempotency risk | 1 |
| Useful monitoring and timeout reasoning | 2 |

## B14 — MVCC, Long Transactions, and Table Bloat

**Source:** PostgreSQL documentation, [MVCC glossary entry](https://www.postgresql.org/docs/current/glossary.html#GLOSSARY-MVCC) and [Routine Vacuuming](https://www.postgresql.org/docs/current/routine-vacuuming.html).

### Candidate prompt

A frequently updated PostgreSQL table grows rapidly even though its logical row count is stable. Autovacuum runs, but disk use and scan cost keep increasing. Monitoring shows a reporting transaction that has remained open for several days.

Explain how MVCC and the old transaction can cause this. Give immediate remediation and prevention measures, including what not to do blindly in production.

### Proposed answer

MVCC updates create new row versions while old versions remain visible to transactions whose snapshots might need them. Vacuum can reclaim dead tuples only when no relevant old snapshot can still see them. A days-old transaction can therefore hold back cleanup, increasing table/index bloat and work.

Confirm the oldest active transaction/snapshot, dead-tuple trends, vacuum progress, and replication-slot horizons. If safe, cancel the query and terminate or roll back the abandoned transaction; then allow/tune vacuum and assess whether normal vacuum can reuse space or whether an online rebuild/repack or a disruptive rewrite is needed to return space to the OS. Prevent with transaction timeouts, no “idle in transaction” sessions, shorter report snapshots, connection-pool hygiene, pagination/replicas for long reports, autovacuum tuned to update volume, and monitoring for old `xmin` horizons.

### Key points

- Ordinary vacuum generally makes space reusable internally; it does not necessarily shrink the file.
- `VACUUM FULL` takes strong locks and should not be prescribed casually.
- Long-lived replication slots can cause related retention even without a client transaction.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct MVCC row-version explanation | 3 |
| Connects old snapshot to blocked reclamation | 2 |
| Safe immediate diagnosis/remediation | 2 |
| Strong prevention and monitoring | 2 |
| Correct vacuum/file-shrink/locking nuance | 1 |

## B15 — Choosing a Composite Index

**Source:** PostgreSQL documentation, [Multicolumn Indexes](https://www.postgresql.org/docs/current/indexes-multicolumn.html) and [Combining Multiple Indexes](https://www.postgresql.org/docs/current/indexes-bitmap-scans.html).

### Candidate prompt

A table `events(tenant_id, created_at, status, payload)` has 500 million rows. The dominant query is:

```sql
SELECT created_at, status
FROM events
WHERE tenant_id = $1
  AND created_at >= $2
ORDER BY created_at DESC
LIMIT 100;
```

Other queries sometimes filter only by `created_at`, and writes are heavy. Propose indexes, explain column order, and state how you would validate the choice. Discuss why creating every plausible index is harmful.

### Proposed answer

The primary candidate is a B-tree on `(tenant_id, created_at DESC)` with `status` as an included column if index-only scans are likely and the extra size/write cost is justified. Equality on the leading tenant column followed by a range/order column supports locating one tenant's newest qualifying rows and stopping after 100. An index beginning with `created_at` is less targeted for this query because tenant filtering follows a broad time range.

If time-only queries are important, add a separate `created_at` index only after workload measurement; the composite index may not serve them efficiently. Consider a partial index only when a stable predicate matches common queries, and partitioning/BRIN for time-correlated append-heavy data where appropriate. Validate with production-like data, `ANALYZE`, `EXPLAIN (ANALYZE, BUFFERS)`, latency distributions, index size, cache behavior, and write amplification.

### Key points

- Selectivity, ordering, range position, and limit all matter.
- `INCLUDE` can cover output but does not make index-only scans guaranteed; visibility and page access matter.
- Each index consumes storage and increases insert/update/vacuum work.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Strong `(tenant_id, created_at)` primary index | 3 |
| Correct column-order/range/order explanation | 2 |
| Sensible covering and alternate-query tradeoffs | 2 |
| Production-like validation plan | 2 |
| Recognizes write/storage amplification | 1 |

## B16 — A Fast Plan Becomes Slow

**Source:** PostgreSQL documentation, [Using EXPLAIN](https://www.postgresql.org/docs/current/using-explain.html) and [Examining Index Usage](https://www.postgresql.org/docs/current/indexes-examine.html).

### Candidate prompt

A join that normally finishes in 80 ms now takes 40 seconds for one customer. `EXPLAIN ANALYZE` shows the planner estimated 10 rows from a filtered table but produced 2,000,000; a nested loop repeatedly scans the inner side. An index exists.

Diagnose likely causes, identify the most useful plan evidence, and propose fixes in a safe order. Why is forcing index scans globally a poor first response?

### Proposed answer

The central failure is cardinality estimation, not necessarily missing index access. Likely causes include stale statistics, highly skewed values, correlated predicates not represented by independent column statistics, parameter/generic-plan behavior, or a query shape hiding selectivity. Inspect estimated versus actual rows at each node and loop count, filters and rows removed, buffer hits/reads, spills, planning/execution time, parameter values, table/statistics freshness, and distribution for the affected tenant.

Start with `ANALYZE` and verify autovacuum/analyze health. Increase statistics targets for skewed columns or add extended statistics for correlated columns where supported. Rewrite predicates only if semantics remain clear, consider a more appropriate/partial index for the exceptional access pattern, and evaluate custom versus generic prepared plans. Forcing index scans globally can make ordinary queries worse, conceal the estimation defect, and prevent sequential scans that are genuinely cheaper for large result sets.

### Key points

- An index existing does not imply it is the cheapest correct plan.
- `EXPLAIN ANALYZE` executes the statement; use care with writes and production load.
- The first badly estimated node often explains downstream plan choices.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Identifies severe cardinality misestimate | 3 |
| Names plausible stats/skew/correlation/parameter causes | 2 |
| Reads useful actual-vs-estimate, loops, and buffer evidence | 2 |
| Gives safe ordered remedies | 2 |
| Explains why global forcing is harmful | 1 |
