# R2B Computer Fundamentals Question Bank

This bank contains 20 scenario-based questions for the R2B computer-fundamentals filter. Sources are authoritative standards or official documentation for the underlying facts. The candidate prompts and evaluation materials are original.

## Administration

- Build a 45–60 minute form from 6–10 questions spanning at least three domains.
- Use a mixture of short answer, multiple-select plus justification, and diagnostic scenarios.
- Prefer explanations over exact terminology. A correct conclusion with incorrect causal reasoning should not receive full credit.
- Publish the expected technology scope for each role. Do not surprise candidates with vendor trivia.
- Grade every response against the question-specific 10-point matrix, then normalize the form score.
- Use equivalent forms and retire compromised questions.

## Index

| ID | Question | Domain |
| --- | --- | --- |
| B01 | Process or Thread Boundary? | Operating systems |
| B02 | Fork, Copy-on-Write, and the Memory Spike | Operating systems |
| B03 | Page Faults and a Collapsing Working Set | Operating systems |
| B04 | Two Locks, One Deadlock | Concurrency |
| B05 | Published Flag, Stale Payload | Concurrency / memory model |
| B06 | Overloaded Producer–Consumer Pipeline | Concurrency / backpressure |
| B07 | Messages Over a TCP Byte Stream | Networking |
| B08 | Retrying an Ambiguous Payment Request | HTTP / reliability |
| B09 | DNS Cutover and Stale Answers | DNS |
| B10 | Incorrect Shared HTTP Cache | HTTP caching |
| B11 | TLS Works, but Identity Is Not Verified | Security / networking |
| B12 | On-Call Scheduling Write Skew | Databases / isolation |
| B13 | Database Deadlock Under Load | Databases / locking |
| B14 | MVCC, Long Transactions, and Table Bloat | Databases / storage |
| B15 | Choosing a Composite Index | Databases / indexing |
| B16 | A Fast Plan Becomes Slow | Databases / query planning |
| B17 | Throughput Versus Tail Latency in GC | Runtime systems |
| B18 | Container Requests, Limits, and OOM Kills | Containers / resources |
| B19 | Parameterization and Dynamic SQL | Application security |
| B20 | Safe Deployment Under Partial Failure | Distributed systems |

Files are grouped by domain:

- `01-os-concurrency.md`: B01–B06
- `02-networking.md`: B07–B11
- `03-databases.md`: B12–B16
- `04-runtime-production.md`: B17–B20

