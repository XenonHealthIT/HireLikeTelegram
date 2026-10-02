# R2A: Data Structures and Streams

## A11 — Least-Frequent Cache

**Source:** Adapted from LeetCode 460, [LFU Cache](https://leetcode.com/problems/lfu-cache/) (Hard). This is rewritten as an original assessment variant.

### Candidate prompt

Implement a fixed-capacity cache with `get(key)` and `put(key,value)`. Both operations must have expected `O(1)` time. Reading or updating an existing key increases its frequency. When capacity is full, insertion evicts the least frequently used key; ties are broken by least recent use among keys at that frequency. Capacity may be zero. Frequencies need not be persisted across process restarts.

### Proposed solution

Use three coordinated structures: a map from key to node `(value,frequency)`, a map from frequency to a doubly linked recency list, and `minFrequency`. A touch removes the node from its current frequency list, increments its frequency, and inserts it at the most-recent end of the new list. If the old list becomes empty and it held `minFrequency`, increment the minimum. A new key starts at frequency one and resets `minFrequency` to one. Eviction removes the least-recent node from the `minFrequency` list.

Every map/list operation is expected `O(1)`; space is `O(capacity)`.

### Key points and hidden cases

- Updating an existing value counts as access under this contract.
- Test zero capacity, repeated reads, tied frequencies, update without eviction, and a list becoming empty.
- A heap is usually `O(log n)` and stale-entry heap tricks do not satisfy strict expected `O(1)`.
- Candidate must keep all three structures consistent during removal and movement.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct key and frequency structures | 3 |
| LFU eviction with LRU tie-breaking | 3 |
| Correct `minFrequency` maintenance | 2 |
| Expected `O(1)` analysis | 1 |
| Zero-capacity and transition tests | 1 |

## A12 — Building-Silhouette Breakpoints

**Source:** Adapted from LeetCode 218, [The Skyline Problem](https://leetcode.com/problems/the-skyline-problem/) (Hard). This is rewritten as an original assessment variant.

### Candidate prompt

Each building is a half-open rectangle `[left,right)` with positive height. Given up to 200,000 buildings, return the minimal ordered list of breakpoints `(x,height)` describing the visible upper silhouette. At a breakpoint, `height` is the new height beginning at `x`. Do not emit adjacent points with equal height. Buildings may share boundaries and heights.

### Proposed solution

Create start and end events, group all events by the same `x`, and maintain active heights as a multiset (balanced tree) or a max-heap with lazy deletion/end coordinates. For the heap variant, push buildings whose left edge is at the current `x`, remove expired entries with `right <= x`, then observe the maximum height. Emit a point only when this maximum differs from the previously emitted height. Sorting buildings by left coordinate can avoid explicit end events when their right edge travels in the heap.

Time is `O(n log n)` and space is `O(n)`.

### Key points and hidden cases

- Events at the same coordinate must be processed together to avoid spurious vertical segments.
- Half-open intervals mean a building ending at `x` is inactive at `x`.
- Test nested buildings, identical rectangles, touching edges, same-x starts/ends, and final return to height zero.
- Removing arbitrary heap elements linearly destroys the complexity target.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct sweep-line event model | 3 |
| Correct active-height structure | 2 |
| Same-coordinate and half-open semantics | 2 |
| Minimal output without duplicate heights | 1 |
| `O(n log n)` analysis and edge tests | 2 |

## A13 — Rolling Peak Telemetry

**Source:** Adapted from LeetCode 239, [Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/) (Hard). This is rewritten as an original assessment variant.

### Candidate prompt

Given an array of signed measurements and a window width `w`, return the maximum measurement in every contiguous window. The array may contain 10,000,000 elements, so the solution must run in `O(n)` time. Define behavior for invalid `w`; in the assessment contract, throw an argument error when `w < 1` or `w > n`.

### Proposed solution

Maintain a deque of indices whose values are in nonincreasing order. Before inserting index `i`, remove the front if it lies before `i-w+1`, then remove from the back while its value is less than or equal to the new value. Append `i`. Once the first full window is reached, the front index holds its maximum. Removing equal older values is safe because the newer equal value expires later.

Each index enters and leaves the deque once, so time is `O(n)` and auxiliary space is `O(w)`.

### Key points and hidden cases

- Store indices, not just values, so expiration is known.
- Test `w=1`, `w=n`, duplicates, decreasing/increasing arrays, negative values, and invalid widths.
- A heap with lazy expiration is `O(n log n)` and misses the required bound.
- Check whether expiry happens before reading the answer.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct monotonic deque invariant | 3 |
| Correct expiry and output timing | 3 |
| Linear-time proof and `O(w)` space | 2 |
| Invalid input and duplicate handling | 1 |
| Clear code/tests | 1 |

## A14 — Online Median Monitor

**Source:** Adapted from LeetCode 295, [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/) (Hard). This is rewritten as an original assessment variant.

### Candidate prompt

Implement a monitor supporting `add(int value)` and `median()` for an unbounded arrival stream. `median()` is called only after at least one value. Insertions should take `O(log n)` and median queries `O(1)`. Duplicate and extreme 32-bit values are allowed. Explain what changes would be required if arbitrary deletion were added later.

### Proposed solution

Keep the lower half in a max-heap and upper half in a min-heap. Maintain two invariants: every lower value is no greater than every upper value, and heap sizes differ by at most one (choose which heap may hold the extra element consistently). Insert based on the lower maximum, then rebalance by moving a root. The median is the root of the larger heap or the average of both roots, computed in a wide type.

Insertion is `O(log n)`, query is `O(1)`, and space is `O(n)`. Arbitrary deletion needs indexed heaps, balanced multisets, or lazy-deletion maps with logical sizes.

### Key points and hidden cases

- Size balance alone is insufficient; ordering must also hold.
- Test duplicates, negative values, alternating extremes, one item, even/odd counts, and average overflow.
- Candidates should not sort the entire collection on every query.
- Good follow-up answers distinguish physical heap contents from logical sizes under lazy deletion.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct two-heap ordering invariant | 3 |
| Correct balancing and median computation | 3 |
| Required complexities and safe averaging | 2 |
| Sensible deletion extension | 1 |
| Edge tests and clarity | 1 |

## A15 — Grid Route With Limited Breaches

**Source:** Adapted from LeetCode 1293, [Shortest Path in a Grid with Obstacles Elimination](https://leetcode.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/) (Hard). This is rewritten as an original assessment variant.

### Candidate prompt

A rectangular grid contains open cells (`0`) and locked cells (`1`). Moving orthogonally costs one step. A responder starts at the top-left open cell and must reach the bottom-right open cell, with authorization to breach at most `k` locked cells. Return the minimum steps, or `-1` if unreachable. The grid can be 200×200 and `k` can be large.

### Proposed solution

Breadth-first search over state `(row,column,remainingBreaches)` returns the shortest path in steps. For each cell, it is sufficient to remember the greatest remaining-breach value seen at an equal or smaller BFS distance: a new visit with no more remaining capacity is dominated and can be discarded. Enqueue an open neighbor without cost to capacity and a locked neighbor only when at least one breach remains. An optional shortcut returns Manhattan distance when `k` is large enough to breach every interior position of a shortest geometric route.

Worst-case time and space are `O(rows×cols×k)` with a full 3D visited set; dominance pruning often reduces this to stored `O(rows×cols)` best-capacity values while preserving correctness under BFS ordering.

### Key points and hidden cases

- Visiting by coordinate alone is wrong because arriving with more remaining capacity is a different and potentially better state.
- Test one cell, no breaches, impossible walls, revisiting a cell with better capacity, and large `k`.
- BFS, not Dijkstra, is enough because every move costs one.
- Candidate should avoid consuming capacity for the guaranteed-open endpoints.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct augmented BFS state | 3 |
| Correct obstacle accounting and shortest-distance result | 2 |
| Sound dominance/visited rule | 2 |
| Accurate complexity discussion | 2 |
| Edge cases and clear code | 1 |
