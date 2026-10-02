# R2B: Operating Systems and Concurrency

## B01 — Process or Thread Boundary?

**Source:** Oracle Java Tutorials, [Processes and Threads](https://docs.oracle.com/javase/tutorial/essential/concurrency/procthread.html).

### Candidate prompt

A document-processing service runs untrusted third-party parsers. The current implementation starts every parser as a thread in the main service. One parser occasionally corrupts shared state; another leaks memory and destabilizes the whole service. The team proposes putting every parser in a separate process.

Explain which failure modes a process boundary improves, what costs it introduces, and whether it alone makes untrusted code safe. Recommend an architecture for communicating jobs and results.

### Proposed answer

Threads share a process's address space, open resources, and failure domain. A memory corruption, uncontrolled allocation, fatal runtime error, or accidental shared-state mutation can affect all threads. Separate processes normally provide distinct virtual address spaces and resource ownership, so a parser crash can be detected and restarted without directly corrupting the parent.

Costs include process startup, higher baseline memory, serialization and IPC, more complex cancellation/monitoring, and potentially more expensive context switches. A process boundary is not a complete sandbox: children may still inherit privileges, access files/network, exhaust host resources, or exploit the kernel. Use worker processes with a narrow IPC protocol, no unnecessary inherited handles, least privilege, OS/container resource limits, timeouts, output-size limits, and supervised restart.

### Key points

- Isolation is the key distinction; “threads are faster” alone is inadequate.
- IPC choices may include pipes, local sockets, or a broker, with explicit framing and backpressure.
- Strong answers distinguish fault containment from security isolation.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Explains shared thread resources and separate process address spaces | 3 |
| Identifies improved crash/corruption/leak containment | 2 |
| Identifies IPC, startup, memory, and operational costs | 2 |
| Notes that process separation alone is not a sandbox | 2 |
| Gives a concrete supervised IPC design | 1 |

## B02 — Fork, Copy-on-Write, and the Memory Spike

**Source:** Linux Kernel documentation, [Copy On Write pages](https://www.kernel.org/doc/gorman/pdf/understand.pdf) and [Memory-management concepts](https://docs.kernel.org/admin-guide/mm/concepts.html).

### Candidate prompt

A Linux service preloads a 12 GB in-memory model and then forks eight workers. Immediately after `fork`, total resident memory stays near 12 GB. During warm-up, every worker modifies scattered counters embedded throughout the model, and resident memory rapidly multiplies.

Explain the observations and propose at least three mitigations. Distinguish virtual address space from resident physical memory.

### Proposed answer

After `fork`, parent and children have separate virtual address spaces whose page-table entries initially reference the same physical pages. Writable mappings are protected for copy-on-write. A write fault causes the kernel to allocate and copy the affected page for that process. Scattered writes can dirty a large fraction of pages even when only a few bytes per page change, producing many private copies and the observed resident-set growth.

Mitigations include separating mutable counters from immutable model pages; mapping the model read-only or through a shared file mapping when semantics permit; performing initialization before forking; aggregating per-worker counters in compact dedicated regions; reducing allocator/GC writes to shared pages; or using threads if the trust and failure model allows shared memory. Huge pages can amplify copied bytes and need measurement. A 12 GB virtual mapping does not imply 12 GB of unique resident memory per process.

### Key points

- Copy-on-write occurs at page granularity, not object or field granularity.
- Reads preserve sharing; writes are the trigger.
- Strong answers suggest measuring proportional set size/private dirty pages rather than adding RSS values blindly.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct COW and page-fault explanation | 3 |
| Distinguishes virtual, resident, shared, and private memory | 2 |
| Connects scattered writes to page-granularity copies | 2 |
| Provides three feasible mitigations | 2 |
| Mentions measurement or huge-page nuance | 1 |

## B03 — Page Faults and a Collapsing Working Set

**Source:** Linux Kernel documentation, [Memory-management concepts](https://docs.kernel.org/admin-guide/mm/concepts.html).

### Candidate prompt

A batch job scans a 200 GB dataset on a machine with 64 GB RAM. It begins at 900 MB/s but later oscillates between short bursts and long stalls. CPU utilization falls, disk activity stays saturated, and unrelated services become slow. Restarting the job temporarily restores performance.

Give the most likely operating-system explanation, name measurements that would confirm it, and propose changes at both application and deployment levels.

### Proposed answer

The active working set exceeds available physical memory. File-backed pages enter the page cache; under pressure the kernel reclaims them, and the scan or competing services fault them back in. If anonymous memory is also pressured, swapping may occur. Repeated eviction/refault creates cache thrashing: the CPU waits on storage, throughput oscillates, and unrelated workloads lose useful cached pages.

Confirm with major/minor fault rates, page-cache and working-set/refault metrics, swap I/O, disk queue/latency, memory pressure-stall information, and per-process resident/anonymous/file-backed memory. Mitigate through sequential streaming with bounded buffers, avoiding repeated passes, partitioning to fit a useful working set, limiting concurrency, using appropriate access hints/direct I/O only after measurement, adding memory or faster storage, and isolating the batch job with resource controls or a dedicated node.

### Key points

- High disk activity plus low CPU suggests I/O wait, not insufficient compute.
- A page fault is not always disk I/O; major faults are the stronger signal.
- Dropping caches repeatedly hides the cause and harms other services.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Identifies working-set pressure/thrashing | 3 |
| Correctly explains page cache, reclaim, and faults | 2 |
| Names useful confirming measurements | 2 |
| Gives application and deployment mitigations | 2 |
| Avoids simplistic “clear cache” diagnosis | 1 |

## B04 — Two Locks, One Deadlock

**Source:** Oracle Java Tutorials, [Liveness](https://docs.oracle.com/javase/tutorial/essential/concurrency/liveness.html).

### Candidate prompt

`transfer(A,B)` locks account A and then B. At the same time, `transfer(B,A)` locks B and then A. Production occasionally freezes with both threads waiting indefinitely.

Explain the exact cycle, give two sound prevention strategies, and compare their tradeoffs. Also distinguish deadlock from livelock and starvation.

### Proposed answer

Thread 1 holds A while waiting for B; thread 2 holds B while waiting for A. Mutual exclusion, hold-and-wait, no forced preemption, and a circular wait coexist. The usual prevention is a global lock ordering, such as always locking the lower immutable account ID first. Another approach uses timed/nonblocking acquisition: if the second lock is unavailable, release the first and retry with randomized backoff. Coarser locking prevents the cycle but reduces concurrency; transactional/actor designs may avoid shared locks at architectural cost.

Livelock means threads remain active and respond to one another but make no progress, often by repeatedly backing off in sync. Starvation means one participant is perpetually denied progress while others continue.

### Key points

- Sorting mutable or non-unique identifiers is unsafe; the ordering key must be total and stable.
- `tryLock` without randomized/backoff discipline can convert deadlock into livelock.
- Detection and victim cancellation is recovery, not prevention.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct wait-for cycle and necessary conditions | 3 |
| Global-order solution is complete and stable | 2 |
| Second valid strategy with tradeoffs | 2 |
| Correct deadlock/livelock/starvation distinction | 2 |
| Operational detection or testing insight | 1 |

## B05 — Published Flag, Stale Payload

**Source:** Oracle Java Tutorials, [Memory Consistency Errors](https://docs.oracle.com/javase/tutorial/essential/concurrency/memconsist.html) and [Synchronization](https://docs.oracle.com/javase/tutorial/essential/concurrency/sync.html).

### Candidate prompt

One thread executes `payload = load(); ready = true;`. Another repeatedly checks `ready` and then consumes `payload`. Neither field is protected by synchronization. In tests it works; under load, the consumer can loop too long or observe an unexpected payload state.

Explain why source-code order is insufficient. Give three correct publication mechanisms and describe what guarantee each must establish.

### Proposed answer

Without a happens-before relationship, the language/runtime may permit stale cached values, compiler or CPU reordering, and visibility of `ready` without the payload writes that logically preceded it. “Eventually visible” is not a correctness contract.

Correct mechanisms include guarding both fields with the same lock; publishing through a volatile/atomic readiness variable whose release write and acquire read order the payload writes; transferring the value through a thread-safe blocking queue; completing a future/promise; or constructing immutable state and safely publishing its reference through a defined synchronization mechanism. The essential guarantee is that initialization writes happen-before consumption reads, not merely that the flag operation is individually atomic.

### Key points

- Volatile semantics are language-specific; candidates should state their assumed memory model.
- Marking only the payload reference volatile may work if it is the actual publication event, but internal mutable state still needs safe construction and ownership.
- `sleep` and repeated polling do not create synchronization.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Explains visibility/reordering and missing happens-before | 3 |
| Provides three valid publication mechanisms | 3 |
| Explains release/acquire or lock ordering correctly | 2 |
| Addresses payload's internal mutable state | 1 |
| Rejects timing-based pseudo-fixes | 1 |

## B06 — Overloaded Producer–Consumer Pipeline

**Source:** Oracle Java API, [BlockingQueue](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/concurrent/BlockingQueue.html).

### Candidate prompt

Twenty producers enqueue work faster than four consumers can process it. The queue is unbounded, so latency and memory rise for hours until the service is killed. Product requires that accepted high-priority jobs are not silently lost.

Design a bounded backpressure policy. Explain overload behavior, shutdown behavior, fairness, and the metrics you would expose.

### Proposed answer

Use a bounded queue sized from acceptable queued work and latency, not available memory. When full, choose an explicit contract: block producers with a deadline, reject with a retryable response, or reserve separate bounded capacity for priority classes. Admission control should occur before expensive work. Persist jobs in a durable broker if “accepted” means surviving process failure; an in-memory blocking queue cannot provide that guarantee.

Consumers should support cancellation and graceful drain. Shutdown needs a defined protocol—stop admission, signal workers, drain until a deadline, then record/requeue unfinished jobs. Monitor queue depth/age, admission/rejection/block time, arrival and service rate, consumer utilization, processing latency, retries, and durable-broker lag. Fairness may require per-tenant queues or weighted scheduling to prevent a noisy producer monopolizing capacity.

### Key points

- More consumers help only until another resource saturates.
- Dropping oldest work conflicts with the stated acceptance guarantee unless product explicitly permits it.
- Queue length alone misses old stuck jobs; age matters.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Proposes bounded capacity and explicit overload contract | 3 |
| Preserves the accepted-job guarantee appropriately | 2 |
| Sound shutdown/drain behavior | 2 |
| Addresses fairness and downstream saturation | 1 |
| Useful capacity/latency/rejection metrics | 2 |
