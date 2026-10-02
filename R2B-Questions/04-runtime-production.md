# R2B: Runtime and Production Fundamentals

## B17 — Throughput Versus Tail Latency in Garbage Collection

**Source:** Oracle, [HotSpot Garbage Collection Tuning Guide](https://docs.oracle.com/en/java/javase/21/gctuning/) and [G1 Garbage Collector](https://docs.oracle.com/en/java/javase/21/gctuning/garbage-first-g1-garbage-collector1.html).

### Candidate prompt

A JVM API has excellent average throughput but periodically experiences 1.5-second p99.9 latency spikes. Logs correlate the spikes with stop-the-world collections. A teammate suggests doubling the heap; another suggests switching collectors immediately.

Explain the throughput/latency/footprint tradeoff and propose a measurement-led investigation. When might a larger heap help, and when might it worsen the symptom?

### Proposed answer

Throughput measures useful application time over a long interval; latency measures response delay, and stop-the-world pauses directly affect tail latency. Collectors trade CPU, memory, barriers, concurrency, and pause behavior. A larger heap can reduce collection frequency and improve throughput, but it may enlarge the live set or the amount processed during some collections, making individual pauses longer; too small a heap can cause frequent collections or allocation failure.

First correlate request traces with timestamped GC logs, pause cause and phase, allocation/promotion rate, live-set size after collection, heap occupancy, CPU saturation, safepoint time, humongous allocations, and container memory limits. Reproduce with representative load. Reduce allocation/churn or retained live data where evidence points there, size heap with headroom, then compare supported collectors and pause goals through controlled tests. Do not cargo-cult flags from a different workload.

### Key points

- Average latency can remain healthy while rare pauses violate the service objective.
- Concurrent collectors consume CPU that can reduce application throughput.
- A pause target is generally a goal, not a hard real-time guarantee.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct throughput/latency/footprint tradeoff | 3 |
| Explains both effects of increasing heap | 2 |
| Strong measurements and correlation plan | 2 |
| Suggests application and collector experiments | 2 |
| Avoids unsupported tuning certainty | 1 |

## B18 — Container Requests, Limits, and OOM Kills

**Source:** Kubernetes documentation, [Resource Management for Pods and Containers](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/) and Linux Kernel [cgroup v2](https://docs.kernel.org/admin-guide/cgroup-v2.html).

### Candidate prompt

A pod requests `250m` CPU and `256Mi` memory, with limits of `500m` CPU and `512Mi` memory. It schedules successfully on a lightly loaded node. During a burst, CPU latency rises and the container is later killed after memory reaches roughly its limit. The node still has some free capacity.

Explain requests versus limits, CPU throttling versus memory enforcement, and why successful scheduling did not guarantee survival. Recommend changes and measurements.

### Proposed answer

The scheduler primarily uses requests to decide placement and reserve/weight capacity; actual use can exceed a request when resources are available. CPU limits are enforced through throttling, so a process needing more than 500m can experience latency even if the node has idle CPU. Memory limits are enforced reactively through cgroups and can result in an OOM kill when the workload exceeds its cgroup budget; node-wide free memory does not authorize the container to exceed its own limit.

Measure usage and working set, allocation spikes, OOM reason, throttled periods/time, latency, request/limit ratios, node pressure, and restart behavior. Right-size from representative distributions, reduce leaks/bursts, use bounded caches, and set requests consistent with normal needs. Consider relaxing/removing a CPU limit when policy allows while preserving requests, and add memory headroom without hiding a leak. Configure graceful restart/readiness and avoid using restarts as memory management.

### Key points

- Requests affect scheduling; limits affect enforcement.
- CPU and memory limits do not fail the same way.
- Memory units and application/runtime heap limits must be coordinated.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct request/scheduling explanation | 2 |
| Correct CPU throttling explanation | 2 |
| Correct memory/OOM explanation | 2 |
| Useful measurements and diagnosis | 2 |
| Balanced right-sizing/mitigation recommendations | 2 |

## B19 — Parameterization and Dynamic SQL

**Source:** OWASP, [SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html).

### Candidate prompt

An endpoint accepts `customerName`, `sortColumn`, and `sortDirection`. A developer binds `customerName` as a prepared-statement value but attempts to bind the other two inside `ORDER BY ? ?`; the driver rejects it, so the developer falls back to string concatenation after escaping quotes.

Explain what can and cannot be parameterized, design a safe implementation, and add defense-in-depth controls.

### Proposed answer

Bound parameters represent data values, not SQL grammar such as identifiers or direction keywords. Keep `customerName` as a bound value. Map the external sort token through an allowlist to fixed SQL fragments—for example, `created` to a hard-coded `created_at` identifier—and map direction to exactly `ASC` or `DESC`. Reject unknown tokens. Never insert raw user strings, and do not rely on quote escaping, because identifier/keyword syntax and database modes differ.

Additional controls include a least-privilege database role, statement timeouts and result limits, structured query builders that preserve binding, input length/type validation, generic client errors with secure server logging, code review/static analysis, and tests with adversarial inputs. Stored procedures are safe only when their internal dynamic SQL is safe.

### Key points

- Parameterization separates code from data but does not substitute arbitrary syntax.
- Allowlists select developer-authored fragments; they do not “sanitize” free-form SQL.
- Escaping is context- and database-specific and is a fragile primary defense.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct code-versus-data parameterization model | 3 |
| Safe allowlist mapping for column/direction | 3 |
| Rejects concatenation/escaping as primary defense | 1 |
| Least privilege, timeouts, limits, and safe logging | 2 |
| Notes stored-procedure/query-builder caveat | 1 |

## B20 — Safe Deployment Under Partial Failure

**Source:** Kubernetes documentation, [Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) and [Liveness, Readiness, and Startup Probes](https://kubernetes.io/docs/concepts/workloads/pods/probes/).

### Candidate prompt

A new API version starts successfully but fails when reading records written in an older schema. During a rolling deployment, half the replicas run old code and half run new code. The new replicas pass liveness checks, receive traffic, and return errors. An immediate rollback also fails because the deployment already ran a destructive database migration.

Design a deployment and schema-change process that tolerates mixed versions and supports safe rollback. Explain the distinct purposes of startup, readiness, and liveness checks.

### Proposed answer

Use expand-and-contract changes. First deploy a backward-compatible schema expansion. Deploy code that can read both old and new formats and writes in a compatibility mode; backfill separately with bounded, observable jobs. Only after every instance and rollback candidate no longer depends on the old shape should a later release stop old writes, validate completion, and eventually remove old schema elements. Destructive migration must not be coupled irreversibly to the first mixed-version rollout.

Use a canary or small initial fraction, automated error/latency/business checks, bounded surge/unavailability, and an immediate traffic rollback path. A startup probe protects slow initialization from premature liveness action. Readiness determines whether an instance should receive traffic and should include critical ability to serve safely without overloading shared dependencies. Liveness detects an instance that needs restart; using it for transient dependency failure can cause restart storms.

### Key points

- Rolling deployment guarantees mixed versions; compatibility is an application/data-contract responsibility.
- Health checks are necessary but cannot prove every data path.
- Feature flags and dual reads/writes may help, but need reconciliation and removal plans.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct expand-and-contract migration sequence | 3 |
| Explicit mixed-version read/write compatibility | 2 |
| Canary, observability, and rollback design | 2 |
| Correct startup/readiness/liveness distinction | 2 |
| Notes backfill/feature-flag operational risk | 1 |
