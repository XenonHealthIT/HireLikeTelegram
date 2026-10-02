# R2A: Arrays and Strings

## A01 — Median Across Two Sorted Shards

**Source:** Adapted from LeetCode 4, [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/) (Hard). This is rewritten as an original assessment variant.

### Candidate prompt

Two storage shards each return response latencies in nondecreasing order. Implement `combinedMedian(a, b)` that returns the exact median of all values without merging the full inputs. Either input may be empty, but not both. Values are signed 32-bit integers; the total length is at most 2,000,000. Your solution must run in `O(log(min(len(a), len(b))))` time and use `O(1)` auxiliary space.

Examples: `[2, 8]` and `[3]` produce `3`; `[1, 7]` and `[3, 9]` produce `5.0`.

Explain how your partition handles an empty left or right side and how you avoid overflow when averaging two integers.

### Proposed solution

Binary-search the shorter array for a partition `i`; derive `j = (m+n+1)/2 - i` in the other array. Treat missing left values as negative infinity and missing right values as positive infinity. A valid split satisfies `aLeft <= bRight` and `bLeft <= aRight`. If `aLeft > bRight`, move `i` left; if `bLeft > aRight`, move it right. For odd total length, return the larger left boundary. For even length, average the larger left boundary and smaller right boundary using a wider numeric type.

Time is `O(log min(m,n))`; extra space is `O(1)`.

### Key points and hidden cases

- Candidate must search the shorter input so `j` remains valid.
- Test an empty array, one-element arrays, duplicates, disjoint ranges, negative values, and `INT_MIN`/`INT_MAX`.
- A linear merge is correct but fails the required complexity.
- Watch integer division and overflow in the even-length case.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct partition invariant and binary-search direction | 3 |
| Correct odd/even result and boundary sentinels | 2 |
| Meets required time and space | 2 |
| Handles overflow, empty input, duplicates, and extremes | 2 |
| Clear implementation and explanation | 1 |

Automatic fail for this question: does not return a correct value on ordinary valid input. Cap at 6/10 for a correct linear merge because it violates the central constraint.

## A02 — Retained Water Between Barriers

**Source:** Adapted from LeetCode 42, [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/) (Hard). This is rewritten as an original assessment variant.

### Candidate prompt

A containment channel is represented by nonnegative barrier heights `h[0..n-1]`, each one meter wide. After rainfall, water remains wherever taller barriers bound a lower section. Return the total retained volume. `n` may be 2,000,000 and each height may be up to `10^9`, so use a result type that cannot overflow. Target `O(n)` time and `O(1)` auxiliary space.

Example: `[4, 1, 2, 0, 3]` retains `6` units.

### Proposed solution

Maintain pointers at both ends plus `leftMax` and `rightMax`. Whichever current boundary is lower determines a side whose retained water is already knowable: if `h[left] <= h[right]`, update `leftMax` and add `leftMax-h[left]`, then advance left; otherwise symmetrically process the right. The taller opposite boundary guarantees the lower side can be finalized without knowing future interior heights.

Time is `O(n)` and auxiliary space is `O(1)`. Prefix/suffix maxima are also correct but use `O(n)` space.

### Key points and hidden cases

- The important evidence is the invariant explaining why the smaller side is safe to settle.
- Test monotone arrays, all equal, fewer than three positions, deep basins, multiple basins, and large totals.
- Reject negative heights or document that they are outside the contract.
- A stack solution is valid `O(n)` but misses the requested `O(1)` space.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct two-pointer invariant | 3 |
| Correct accumulation over all basin shapes | 3 |
| `O(n)` time and `O(1)` extra space | 2 |
| Edge cases and wide result type | 1 |
| Clear code and tests | 1 |

## A03 — Smallest Complete Log Window

**Source:** Adapted from LeetCode 76, [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/) (Hard). This is rewritten as an original assessment variant.

### Candidate prompt

An incident log is a string `log`, and `required` lists marker characters that must all occur in a diagnostic excerpt, including repeated markers. Return the shortest contiguous excerpt of `log` whose character multiset covers `required`. If several excerpts have equal minimum length, return the earliest. If none exists, return an empty string. Inputs contain Unicode code points already exposed by the language as an iterable sequence; `len(log)` may be 1,000,000.

Example: `log="CABXACB"`, `required="AABC"` returns `"CABXA"`.

### Proposed solution

Build a frequency map for the required multiset and track either the number of satisfied distinct requirements or the total number of matched required occurrences. Expand a right pointer, updating the window count. Once all requirements are met, repeatedly move the left pointer while coverage remains valid, recording a better window before invalidating it. Update the best answer only on strictly shorter windows to preserve the earliest tie.

Time is `O(n + |required|)` because each pointer moves forward at most once; space is `O(u)` for the distinct required symbols (or alphabet size).

### Key points and hidden cases

- Repeated required characters are the primary trap.
- Test empty requirement, missing marker, exact match, irrelevant prefixes, equal-length ties, and non-ASCII characters.
- Rechecking all counts at every move can turn the solution quadratic in a large alphabet.
- Candidate must state the platform's string/indexing assumptions for Unicode.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct multiset coverage accounting | 3 |
| Correct expand/contract window logic | 3 |
| Linear-time reasoning and appropriate space | 2 |
| Tie, empty, repeated-symbol, and Unicode handling | 1 |
| Clear code and tests | 1 |

## A04 — Merge K Ordered Event Streams

**Source:** Adapted from LeetCode 23, [Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/) (Hard). This is rewritten as an original assessment variant.

### Candidate prompt

You receive `k` finite event streams. Each stream is an iterator yielding records `(timestamp, streamId, sequence, payload)` in ascending `(timestamp, sequence)` order for that stream. Produce one iterator in global order by `(timestamp, streamId, sequence)`. Do not load all events in memory. The input may contain empty streams, equal timestamps, and up to 100,000 streams.

State the complexity in terms of total events `N` and active streams `k`.

### Proposed solution

Prime a min-heap with the first event from every nonempty stream. Heap entries contain the complete global comparison key plus a reference to the originating iterator. Repeatedly remove the minimum, yield it, pull the next event from the same iterator, and insert that event if present. At most one pending record per stream is held.

Time is `O(N log k)` and extra space is `O(k)`. A balanced pairwise merge has similar asymptotic time for materialized linked lists but does not naturally preserve streaming behavior.

### Key points and hidden cases

- The full tie-break key must be deterministic; comparing payload objects is unsafe.
- Test zero streams, all empty, one stream, equal timestamps across streams, long skewed streams, and iterator exhaustion.
- The implementation must not materialize the result or all source events.
- Candidate should discuss how upstream iterator errors are surfaced and whether the consumer can stop early.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct heap-based streaming merge | 3 |
| Deterministic handling of ties and empty streams | 2 |
| Lazy output with at most one buffered item per stream | 2 |
| Correct `O(N log k)`/`O(k)` analysis | 2 |
| Clear code and operational edge cases | 1 |

## A05 — Largest Rectangle in a Capacity Profile

**Source:** Adapted from LeetCode 84, [Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/) (Hard). This is rewritten as an original assessment variant.

### Candidate prompt

A row of adjacent machines has integer spare-capacity values. A batch assigned to a contiguous range must use the same capacity on every machine, so the batch capacity equals `range length × minimum capacity in that range`. Return the maximum possible batch capacity. The array length can be 2,000,000 and values are nonnegative. Use a wide result type.

Example: `[2, 1, 5, 6, 2, 3]` produces `10` from the two-machine range with minimum capacity `5`.

### Proposed solution

Scan left to right with a stack of increasing heights and their earliest usable start index. For each height at index `i`, pop taller entries; each popped height's maximal right boundary is `i-1`, so calculate `height × (i-start)`. Carry the earliest popped start into the new entry. Equal heights can be coalesced. Append a conceptual zero-height sentinel or flush the stack at the end.

Every entry is pushed and popped once, giving `O(n)` time and `O(n)` worst-case space.

### Key points and hidden cases

- Candidate must connect a pop to the first smaller value on the right and the saved start to the first smaller value on the left.
- Test increasing, decreasing, equal, zero-separated, single-element, and overflow cases.
- Quadratic range enumeration and repeated minimum queries are insufficient.
- Accept the two-pass nearest-smaller-boundary method if correct, though it uses more arrays.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct monotonic-stack invariant | 3 |
| Correct width/start calculation on pop | 3 |
| Complete final flush and duplicate handling | 1 |
| `O(n)` analysis and wide arithmetic | 2 |
| Clear code and tests | 1 |
