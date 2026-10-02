# R2A: Graphs and Indexing

## A16 — Lexicographically Smallest Complete Itinerary

**Source:** Adapted from LeetCode 332, [Reconstruct Itinerary](https://leetcode.com/problems/reconstruct-itinerary/) (Hard). This is rewritten as an original assessment variant.

### Candidate prompt

You receive directed travel coupons `(from,to)`. A valid itinerary begins at a specified origin and uses every coupon exactly once. The input guarantees that at least one valid itinerary exists. Return the lexicographically smallest sequence of locations among all valid itineraries. Duplicate coupons are distinct and must each be consumed. There may be 300,000 coupons.

### Proposed solution

Model coupons as directed multigraph edges. Store each origin's destinations in a min-heap (or reverse-sorted vector popped from the end). Apply iterative Hierholzer traversal: while the current vertex has unused outgoing edges, consume the lexicographically smallest edge and push its destination. When no edge remains, pop the vertex into the route. Reverse the resulting postorder. Local smallest-edge selection works with Hierholzer because dead ends are committed backward rather than prematurely terminating a forward greedy route.

Time is `O(E log E)` with heaps or `O(E log E)` total sorting plus linear traversal; space is `O(E)`.

### Key points and hidden cases

- A simple forward greedy walk can get stuck before consuming all edges.
- Duplicate tickets require a multiset/list, not a set.
- Test cycles, forced detours, duplicate edges, a single edge, and an origin appearing only as destination.
- Validate the returned route has exactly `E+1` vertices even though existence is promised.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Recognizes Eulerian-edge-use structure | 3 |
| Correct Hierholzer traversal and reversal | 3 |
| Lexical ordering and duplicate handling | 2 |
| Complexity and large-depth-safe implementation | 1 |
| Edge tests and clarity | 1 |

## A17 — Single-Point Network Links

**Source:** Adapted from LeetCode 1192, [Critical Connections in a Network](https://leetcode.com/problems/critical-connections-in-a-network/) (Hard). This is rewritten as an original assessment variant.

### Candidate prompt

An undirected network has vertices `0..n-1` and no duplicate edges. Return every link whose removal increases the number of connected components. The graph is usually connected, but your implementation must also handle disconnected input. `n` and the edge count can each reach 500,000. Return each link with the smaller endpoint first; output order does not matter.

### Proposed solution

Run depth-first search in every unvisited component. Record discovery time `tin[v]` and the smallest discovery time reachable from `v` through its DFS subtree plus at most one back edge, `low[v]`. After exploring tree edge `(v,to)`, update `low[v] = min(low[v],low[to])`; the edge is a bridge exactly when `low[to] > tin[v]`. For a visited non-parent neighbor, update from `tin[to]`, not `low[to]`.

Time is `O(V+E)` and space `O(V+E)`. At this scale, use an iterative DFS or a runtime with a safely enlarged stack.

### Key points and hidden cases

- The strict `>` comparison matters; equality means the child can reach the parent via another route.
- Test a tree, a cycle, cycles connected by one edge, disconnected components, and deep chains.
- Parent must be tracked by edge identity if parallel edges are ever permitted in a future contract.
- Merely removing each edge and checking connectivity is too slow.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct discovery/low-link definitions | 3 |
| Correct bridge condition and back-edge update | 3 |
| Covers all connected components | 1 |
| Linear complexity and depth safety | 2 |
| Tests and implementation clarity | 1 |

## A18 — Minimum Transit Lines

**Source:** Adapted from LeetCode 815, [Bus Routes](https://leetcode.com/problems/bus-routes/) (Hard). This is rewritten as an original assessment variant.

### Candidate prompt

Each transit line is a set of stations visited repeatedly. A traveler begins at `source` and may board any line serving that station, ride to any station on it, and transfer. Return the minimum number of distinct boardings needed to reach `target`, or `-1`. Up to 500 lines are present and the total number of line-station entries is at most 100,000. Station IDs are sparse nonnegative integers.

### Proposed solution

Build an inverted index from station to lines. Breadth-first search either lines or stations, with the BFS level representing boardings. A clean approach enqueues all lines serving the source at distance one, then for each dequeued line visits its stations and all not-yet-used lines serving those stations. Mark lines visited to avoid boarding them again; mark/clear expanded stations so a large hub's adjacency list is not rescanned repeatedly. If `source==target`, return zero.

The intended implementation is approximately `O(total route entries)` time and space because each line and each station adjacency is expanded once.

### Key points and hidden cases

- Shortest number of station hops is not the same as fewest boardings.
- Test equal endpoints, missing stations, large shared hubs, disconnected components, duplicate station entries, and one direct line.
- Constructing every pairwise line intersection can be quadratic.
- Clearing an inverted-list bucket after expansion is a useful performance detail.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Models BFS levels as boardings | 3 |
| Correct station-to-line inverted index | 2 |
| Avoids repeated hub/line expansion | 2 |
| Correct unreachable and equal-endpoint behavior | 1 |
| Complexity, tests, and clarity | 2 |

## A19 — Later Values Smaller Than Current

**Source:** Adapted from LeetCode 315, [Count of Smaller Numbers After Self](https://leetcode.com/problems/count-of-smaller-numbers-after-self/) (Hard). This is rewritten as an original assessment variant.

### Candidate prompt

For each position in an integer array, return how many values strictly smaller than it occur to its right. The array can contain 500,000 signed 32-bit values and duplicates. An `O(n log n)` solution is required.

Example: `[5, 2, 6, 1]` produces `[2, 1, 1, 0]`.

### Proposed solution

One solution coordinate-compresses all distinct values to ranks. Scan from right to left using a Fenwick tree of frequencies. For value rank `r`, query the prefix sum through `r-1`, store that count, then add one at `r`. Strictly smaller semantics are captured by excluding the current rank.

An equally strong solution performs merge sort over `(value,originalIndex)` pairs and counts how many right-half elements move ahead of each left element during merge. Both approaches take `O(n log n)` time and `O(n)` space.

### Key points and hidden cases

- Duplicates are not counted as smaller.
- Test all equal, sorted ascending/descending, negative values, integer extremes, and empty input.
- Compression must preserve order but not numeric distance.
- A balanced search tree needs subtree sizes and duplicate counts; a plain set is insufficient.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct right-to-left or merge-count formulation | 3 |
| Strict inequality and duplicate handling | 2 |
| Correct Fenwick/merge implementation | 2 |
| Required complexity and safe count types | 2 |
| Edge tests and clarity | 1 |

## A20 — First Missing Positive Identifier

**Source:** Adapted from LeetCode 41, [First Missing Positive](https://leetcode.com/problems/first-missing-positive/) (Hard). This is rewritten as an original assessment variant.

### Candidate prompt

An array contains arbitrary signed integers and may be modified. Return the smallest positive integer not present. The solution must run in `O(n)` time with `O(1)` auxiliary space; sorting and hash sets are disallowed. The array may contain duplicates and integer extremes.

### Proposed solution

Only values from `1` through `n` can affect the answer. Repeatedly place each in-range value `x` at index `x-1` by swapping while the destination does not already contain `x`. After placement, scan for the first index `i` whose value is not `i+1`; return `i+1`. If every position matches, return `n+1`.

Each successful swap places at least one value into its final slot, so despite the nested-looking loop total work is `O(n)`. Extra storage is constant.

An alternative sign-marking solution is acceptable if it safely normalizes irrelevant values and handles the presence of `1`.

### Key points and hidden cases

- The destination-equality check prevents infinite swaps on duplicates.
- Test empty input, no positive values, duplicates, gaps at one and `n`, already arranged values, and extremes.
- Off-by-one errors between value `x` and index `x-1` are common.
- A hash set is correct functionally but violates the space constraint.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct in-place placement/marking invariant | 3 |
| Correct duplicate and out-of-range handling | 2 |
| Correct final scan and `n+1` case | 2 |
| Valid linear-time/constant-space proof | 2 |
| Edge tests and code clarity | 1 |
