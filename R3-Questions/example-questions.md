# R3 Example Questions

These are original assessment questions, not copied contest questions. The source links identify the style archives that informed the design.

## M01 — Reachable Integer Pairs

**Style reference:** [Oxford MAT archive](https://www.maths.ox.ac.uk/study-here/undergraduate-study/maths-admissions-test) and [STEP preparation archive](https://www.ocr.org.uk/students/step-mathematics/preparing-for-step/).

### Candidate prompt

Begin with the ordered pair `(1,1)`. At each step you may perform exactly one of these operations:

- replace `(a,b)` by `(a+b,b)`; or
- replace `(a,b)` by `(a,a+b)`.

Characterize exactly which ordered pairs of positive integers can be reached. Prove both directions of your characterization. Then determine whether `(2026,2025)` and `(2026,2024)` are reachable.

### Proposed solution

The reachable pairs are exactly the pairs `(a,b)` with `gcd(a,b)=1`.

Each operation preserves the greatest common divisor because

`gcd(a+b,b)=gcd(a,b)` and `gcd(a,a+b)=gcd(a,b)`.

Since the starting gcd is one, every reachable pair is coprime.

Conversely, take a coprime positive pair other than `(1,1)`. Its coordinates cannot be equal: equal positive coordinates would have gcd equal to that common value, so coprimality would force `(1,1)`. Subtract the smaller coordinate from the larger. The result remains positive, remains coprime, and has a strictly smaller coordinate sum. Repeating this reverse operation must terminate; the only possible terminal coprime pair with equal coordinates is `(1,1)`. Reversing the subtraction sequence gives an allowed forward construction.

`gcd(2026,2025)=1`, so `(2026,2025)` is reachable. `gcd(2026,2024)=2`, so `(2026,2024)` is not.

### Key observations

- Finding the gcd invariant proves only necessity; a complete solution must also prove sufficiency.
- The reverse Euclidean algorithm supplies the construction.
- Termination needs justification through a decreasing positive integer measure.

### Scoring rubric (20 points)

| Evidence | Points |
| --- | ---: |
| Conjectures the exact coprime characterization | 3 |
| Proves gcd invariance | 4 |
| Introduces the reverse subtraction process | 4 |
| Proves positivity, gcd preservation, and termination | 5 |
| Correctly resolves both requested pairs | 2 |
| Clear, logically complete presentation | 2 |

## M02 — Largest Divisibility-Free Set

**Style reference:** [MAA Putnam archive](https://maa.org/maa-putnam-archive/) and [IMC problem archive](https://www.imc-math.org.uk/?item=info&item=problems).

### Candidate prompt

Let `n` be a positive integer.

1. Prove that any selection of `n+1` distinct integers from `{1,2,...,2n}` contains two selected integers such that one divides the other.
2. Show that `n+1` cannot be replaced by `n`; that is, construct a selection of `n` integers containing no such pair.

### Proposed solution

Write every positive integer uniquely as `2^k m`, where `m` is odd. Among the integers from 1 through `2n`, there are only `n` possible odd parts: `1,3,5,...,2n-1`.

If `n+1` numbers are selected, the pigeonhole principle gives two with the same odd part, say `2^r m` and `2^s m`. Assuming `r<s`, the first divides the second.

For sharpness, choose `{n+1,n+2,...,2n}`. If two distinct members `x<y` satisfied `x|y`, then `y` would be at least `2x`, which is greater than `2n` because `x>n`. This is impossible. Thus a divisibility-free set of size `n` exists.

### Key observations

- The right grouping is by odd part, not by parity alone.
- Uniqueness of the decomposition must be stated.
- The upper-half construction proves the bound is exact.

### Scoring rubric (20 points)

| Evidence | Points |
| --- | ---: |
| Uses the unique odd-part/power-of-two decomposition | 5 |
| Counts exactly `n` possible odd parts | 3 |
| Applies pigeonhole and proves divisibility | 5 |
| Gives the upper-half construction | 3 |
| Proves the construction is divisibility-free | 3 |
| Clear presentation | 1 |

## M03 — A Self-Similar Polynomial

**Style reference:** [MAA Putnam archive](https://maa.org/maa-putnam-archive/). This is intended as the high-end discriminator on a form.

### Candidate prompt

Find every polynomial `P` with real coefficients satisfying

`P(x^2)=P(x)^2`

for every real number `x`. Prove that your list is complete.

### Proposed solution

The solutions are `P(x)=0` and `P(x)=x^m` for every nonnegative integer `m`.

The zero polynomial works. A constant solution `c` must satisfy `c=c^2`, giving `c=0` or `c=1`; the latter is `x^0`.

Now suppose `P` is nonconstant. Its leading coefficient `a` satisfies `a=a^2`, so `a=1`. Factor

`P(x)=x^m Q(x)`,

where `m` is the multiplicity of zero as a root and `Q(0)≠0`. Substitution gives `Q(x^2)=Q(x)^2`, and at zero this implies `Q(0)=1`.

We show `Q` has no complex root. If a nonzero complex number `alpha` were a root, then every square root of `alpha` would also be a root, because `Q(beta)^2=Q(beta^2)=Q(alpha)=0`. Repeating produces roots of arbitrarily large `2`-power depth. These include infinitely many distinct complex numbers, contradicting that a nonzero polynomial has finitely many roots. Therefore `Q` has no complex roots. By the fundamental theorem of algebra, a nonconstant real polynomial would have a complex root, so `Q` is constant. Since `Q(0)=1`, `Q=1` and `P=x^m`.

Each listed polynomial directly satisfies the equation.

### Key observations

- Checking only monomials is not a completeness proof.
- Factoring the root at zero separates the only allowable root.
- A candidate may instead use coefficient comparison or root multiplicities if the proof is complete.

### Scoring rubric (20 points)

| Evidence | Points |
| --- | ---: |
| Finds zero, one, and the monomial family | 4 |
| Handles constants and leading coefficient | 3 |
| Correctly factors `P=x^mQ` with `Q(0)=1` | 4 |
| Proves `Q` cannot have a nonzero complex root | 5 |
| Uses the fundamental theorem to conclude `Q=1` | 2 |
| Verifies all solutions and presents clearly | 2 |

## M04 — A Quadratic Functional Equation

**Style reference:** [STEP preparation archive](https://www.ocr.org.uk/students/step-mathematics/preparing-for-step/) and [IMC problem archive](https://www.imc-math.org.uk/?item=info&item=problems).

### Candidate prompt

Determine every continuous function `f:R→R` such that

`f(x+y)+f(x-y)=2f(x)+2f(y)`

for all real `x,y`, and `f(1)=1`.

### Proposed solution

The unique solution is `f(x)=x^2`.

Set `y=0` to obtain `f(0)=0`. Set `x=0` to see that `f` is even. Setting `y=x` gives `f(2x)=4f(x)`.

For a fixed real `x`, the original equation with inputs `nx` and `x` yields

`f((n+1)x)+f((n-1)x)=2f(nx)+2f(x)`.

Using `f(0)=0`, `f(x)=f(x)`, and induction in this recurrence gives `f(nx)=n^2f(x)` for every integer `n`. Applying this to `x/n` gives `f(x/n)=f(x)/n^2`. Consequently, for every rational `q`,

`f(q)=q^2f(1)=q^2`.

For any real `x`, choose rationals converging to `x`. Continuity gives `f(x)=x^2`. Direct substitution verifies the solution.

### Key observations

- Continuity is needed only to extend from a dense set to all real values.
- A proof that merely guesses `x^2` receives limited credit.
- Other regularity assumptions could replace continuity, but are outside this prompt.

### Scoring rubric (20 points)

| Evidence | Points |
| --- | ---: |
| Derives `f(0)=0`, evenness, or the doubling rule | 4 |
| Establishes the integer recurrence | 4 |
| Proves `f(nx)=n^2f(x)` | 5 |
| Extends correctly to rational arguments | 3 |
| Uses continuity to cover reals | 2 |
| Verification and clarity | 2 |

## M05 — Records in a Random Ordering

**Style reference:** [MAA Putnam archive](https://maa.org/maa-putnam-archive/) and [IMC problem archive](https://www.imc-math.org.uk/?item=info&item=problems).

### Candidate prompt

A uniformly random permutation `X1,X2,...,Xn` of `{1,2,...,n}` is revealed from left to right. Position `k` is called a record if `Xk` is larger than every earlier revealed value. Position 1 is always a record. Let `R` be the number of records.

1. Find `E[R]`.
2. For `n≥2`, prove that `R` is even with probability `1/2` and odd with probability `1/2`.

### Proposed solution

For each `k`, define `Ik` to be one when position `k` is a record. Among the first `k` values, each position is equally likely to contain their maximum, so `P(Ik=1)=1/k`. Therefore

`E[R]=sum(k=1..n) 1/k`.

For the parity statement, use the relative rank representation of a random permutation: at time `k`, the rank of `Xk` among the first `k` values is uniform on `{1,...,k}`, and these relative ranks are independent. Hence the record indicators are independent Bernoulli variables with probabilities `1/k`.

Now

`E[(-1)^R] = product(k=1..n) E[(-1)^Ik] = product(k=1..n) (1-2/k)`.

For `n≥2`, the factor for `k=2` is zero, so `E[(-1)^R]=0`. But this expectation equals `P(R even)-P(R odd)`. The two probabilities sum to one, so both are `1/2`.

### Key observations

- Linearity of expectation does not require independence for part 1.
- Part 2 does require a valid argument for independence or an equivalent counting recurrence.
- Stating that records “seem independent” is not enough; justify the relative-rank construction.

### Scoring rubric (20 points)

| Evidence | Points |
| --- | ---: |
| Defines record indicators | 2 |
| Proves `P(Ik=1)=1/k` | 3 |
| Obtains the harmonic-number expectation | 3 |
| Establishes independent relative ranks or an equivalent recurrence | 5 |
| Uses the parity generating expectation correctly | 5 |
| Clear conclusion | 2 |

## M06 — A Cubically Nilpotent Transformation

**Style reference:** [IMC problem archive](https://www.imc-math.org.uk/?item=info&item=problems). Use only when elementary linear algebra is declared prerequisite knowledge.

### Candidate prompt

Let `V` be a real vector space of dimension `n`, and let `T:V→V` be linear with `T^3=0`.

1. Prove that `rank(T)≤floor(2n/3)`.
2. For every `n`, construct an example showing that this bound is attainable.

### Proposed solution

Let `r=rank(T)`. The standard rank inequality gives

`rank(T^2) ≥ rank(T)+rank(T)-n = 2r-n`.

Because `T^3=0`, every vector in the image of `T^2` is killed by `T`. Thus `im(T^2)⊆ker(T)`, and

`rank(T^2)≤nullity(T)=n-r`.

Combining the inequalities gives `2r-n≤n-r`, hence `3r≤2n` and `r≤floor(2n/3)`.

For sharpness, decompose as many dimensions as possible into blocks of size three. On each triple with basis `e1,e2,e3`, define `T(e3)=e2`, `T(e2)=e1`, and `T(e1)=0`; this block has cube zero and rank two. If `n=3q`, use `q` such blocks. If `n=3q+1`, add one zero block. If `n=3q+2`, add a two-dimensional block `T(f2)=f1`, `T(f1)=0`, contributing rank one. The resulting ranks are respectively `2q`, `2q`, and `2q+1`, equal to `floor(2n/3)`.

### Key observations

- The inclusion `im(T^2)⊆ker(T)` uses the cube-zero condition exactly.
- Candidates may use Jordan blocks if that theorem is within the declared syllabus.
- A construction only for multiples of three is incomplete.

### Scoring rubric (20 points)

| Evidence | Points |
| --- | ---: |
| Introduces rank/nullity notation appropriately | 2 |
| Obtains `rank(T^2)≥2r-n` | 4 |
| Uses `im(T^2)⊆ker(T)` | 4 |
| Derives the sharp upper bound | 3 |
| Constructs size-three blocks | 3 |
| Handles all three residues of `n mod 3` | 3 |
| Clear presentation | 1 |

## M07 — Growth of a Nonlinear Recurrence

**Style reference:** [STEP preparation archive](https://www.ocr.org.uk/students/step-mathematics/preparing-for-step/) and [MAA Putnam archive](https://maa.org/maa-putnam-archive/).

### Candidate prompt

Let `a1>0` and define

`a(n+1)=a(n)+1/a(n)`

for `n≥1`. Prove that

`lim(n→∞) a(n)/sqrt(2n)=1`.

A complete solution must justify every estimate used; recognizing the likely scale alone is not enough.

### Proposed solution

Squaring the recurrence gives

`a(n+1)^2 = a(n)^2 + 2 + 1/a(n)^2`.

In particular, `a(n+1)^2≥a(n)^2+2`, so by induction

`a(k)^2≥a1^2+2(k-1)`.

Summing the squared recurrence from `k=1` to `n-1` gives

`a(n)^2 = a1^2+2(n-1)+sum(k=1..n-1) 1/a(k)^2`.

The lower bound on `a(k)^2` shows that the sum is at most a constant plus a constant multiple of the harmonic sum, hence `O(log n)`. Therefore

`a(n)^2 = 2n + O(log n)`.

Dividing by `2n` yields `a(n)^2/(2n)→1`. All terms are positive, so taking square roots gives the desired limit.

### Key observations

- The squared recurrence turns a nonlinear update into an almost telescoping expression.
- It is not enough to discard the positive error term; it must be shown to be lower order than `n`.
- Any rigorous comparison establishing `sum 1/a(k)^2=o(n)` earns full method credit.

### Scoring rubric (20 points)

| Evidence | Points |
| --- | ---: |
| Derives the exact squared recurrence | 4 |
| Establishes a linear lower bound for `a(k)^2` | 4 |
| Telescopes/sums the recurrence | 4 |
| Bounds the error sum by `O(log n)` or otherwise `o(n)` | 5 |
| Completes the limit carefully | 2 |
| Clear presentation | 1 |

## M08 — A Sharp Curvature Bound

**Style reference:** [STEP preparation archive](https://www.ocr.org.uk/students/step-mathematics/preparing-for-step/).

### Candidate prompt

Let `f` be twice differentiable on `[0,1]`, with

`f(0)=f(1)=0` and `|f''(x)|≤1`

for every `x` in `(0,1)`. Prove the sharp bound

`|f(x)|≤x(1-x)/2`

for every `x` in `[0,1]`. Give functions for which equality occurs.

### Proposed solution

Let `q(x)=x(1-x)/2`, so `q(0)=q(1)=0` and `q''(x)=-1`.

Since `f''≥-1`, we have `(f-q)''=f''+1≥0`. Thus `f-q` is convex. A convex function lies below the chord joining its endpoint values; those endpoint values are both zero. Hence `f(x)-q(x)≤0`, or `f(x)≤q(x)`.

Similarly, since `f''≤1`, `(f+q)''=f''-1≤0`, so `f+q` is concave. A concave function lies above its zero endpoint chord, giving `f(x)+q(x)≥0`, or `f(x)≥-q(x)`.

Together, `|f(x)|≤q(x)`. Equality throughout is obtained by `f=q` and `f=-q`, showing the constant is sharp.

### Key observations

- The comparison parabola is chosen to match both endpoint conditions and the second-derivative bound.
- The direction of the chord inequality for convex and concave functions is a common failure point.
- A Taylor-theorem proof is acceptable if it produces the exact position-dependent bound.

### Scoring rubric (20 points)

| Evidence | Points |
| --- | ---: |
| Chooses the correct comparison parabola | 4 |
| Proves the upper bound using convexity | 5 |
| Proves the lower bound using concavity | 5 |
| Combines them into the absolute-value result | 2 |
| Identifies equality examples and sharpness | 3 |
| Clear presentation | 1 |

## M09 — A Two-Color Sum Obstruction

**Style reference:** [Oxford MAT archive](https://www.maths.ox.ac.uk/study-here/undergraduate-study/maths-admissions-test). This is a recommended entry question.

### Candidate prompt

Each integer in `{1,2,3,4,5}` is colored either red or blue. Prove that there exist `x,y,z` of the same color such that `x+y=z`. The values `x` and `y` are allowed to be equal.

Then show that the statement is false if `{1,2,3,4,5}` is replaced by `{1,2,3,4}`.

### Proposed solution

Interchanging the color names if needed, assume 1 is red. Then 2 must be blue; otherwise `1+1=2` is a red solution. Next, 4 must be red; otherwise `2+2=4` is a blue solution. Now 3 must be blue; otherwise `1+3=4` is a red solution.

If 5 is red, then `1+4=5` is a red solution. If 5 is blue, then `2+3=5` is a blue solution. Either way a monochromatic equation exists.

For `{1,2,3,4}`, color 1 and 4 red, and 2 and 3 blue. The possible sums remaining in the set are `1+1=2`, `1+2=3`, `1+3=4`, and `2+2=4`; none has all three terms the same color.

### Key observations

- Symmetry permits fixing the color of 1 without loss of generality.
- The proof is a forced chain, not exhaustive enumeration of all 32 colorings.
- The counterexample establishes that five is the smallest guaranteed range.

### Scoring rubric (20 points)

| Evidence | Points |
| --- | ---: |
| Uses color symmetry correctly | 2 |
| Forces the colors of 2 and 4 | 5 |
| Forces the color of 3 | 3 |
| Completes both cases for 5 | 4 |
| Gives and verifies a valid four-element coloring | 4 |
| Clear proof | 2 |

## M10 — Paths That Stay Below the Diagonal

**Style reference:** [MAA Putnam archive](https://maa.org/maa-putnam-archive/) and [Oxford MAT archive](https://www.maths.ox.ac.uk/study-here/undergraduate-study/maths-admissions-test).

### Candidate prompt

A path from `(0,0)` to `(n,n)` consists of `n` right steps `(1,0)` and `n` up steps `(0,1)`. Count the paths that never enter the region `y>x`. Prove your formula.

### Proposed solution

There are `binom(2n,n)` unrestricted paths. Count the bad paths that at some point enter `y>x`.

For a bad path, find its first step that reaches the line `y=x+1`. Reflect the portion of the path from the start through that step across the line `y=x`. This converts one more up step than right step in the prefix into one more right step than up step. The transformed full path can be viewed as a path with `n+1` right steps and `n-1` up steps. The construction is reversible by reflecting through the first corresponding crossing, so the number of bad paths is `binom(2n,n-1)` (equivalently `binom(2n,n+1)`).

Therefore the desired number is

`binom(2n,n)-binom(2n,n-1) = (1/(n+1)) binom(2n,n)`.

This is the `n`th Catalan number.

### Key observations

- Naming the Catalan number without a proof is insufficient.
- The reflection map must be described well enough to establish a bijection.
- Check `n=1` and `n=2` to detect an index reversal.

### Scoring rubric (20 points)

| Evidence | Points |
| --- | ---: |
| Counts unrestricted paths | 3 |
| Defines the first bad crossing | 3 |
| Constructs the reflection map correctly | 6 |
| Justifies reversibility/bijection | 3 |
| Simplifies to the Catalan formula | 3 |
| Small-case check and clarity | 2 |

## M11 — A Restricted Greatest Common Divisor

**Style reference:** [Oxford MAT archive](https://www.maths.ox.ac.uk/study-here/undergraduate-study/maths-admissions-test) and [IMC problem archive](https://www.imc-math.org.uk/?item=info&item=problems).

### Candidate prompt

Let `a` and `b` be coprime positive integers. Prove that

`gcd(a+b, a^2-ab+b^2)`

is either 1 or 3. Determine exactly when it equals 3.

### Proposed solution

Let `d` be the displayed gcd. Since `d` divides `a+b`, we have `b≡-a (mod d)`. Therefore

`a^2-ab+b^2 ≡ a^2+a^2+a^2 = 3a^2 (mod d)`.

Thus `d` divides `3a^2`. Also `gcd(a,d)=1`, because any common divisor of `a` and `d` would divide both `a` and `a+b`, hence both `a` and `b`. Therefore `d` divides 3, so `d` is 1 or 3.

The gcd equals 3 exactly when 3 divides `a+b`. Indeed, if `3|(a+b)`, then `b≡-a (mod 3)`, and the same calculation shows `3|(a^2-ab+b^2)`. Conversely, if the gcd is 3, it certainly divides `a+b`.

### Key observations

- Coprimality is used to cancel the possible factors of `a` from `3a^2`.
- The characterization is `a+b≡0 mod 3`, not `a≡b mod 3`.
- A symmetric proof using `b` is equally valid.

### Scoring rubric (20 points)

| Evidence | Points |
| --- | ---: |
| Introduces the common divisor and reduces modulo it | 4 |
| Obtains divisibility by `3a^2` | 4 |
| Correctly uses coprimality to conclude `d|3` | 5 |
| Proves both directions of the equality-to-3 condition | 5 |
| Clear presentation | 2 |

## M12 — A Symmetric Product Inequality

**Style reference:** [IMC problem archive](https://www.imc-math.org.uk/?item=info&item=problems) and [STEP preparation archive](https://www.ocr.org.uk/students/step-mathematics/preparing-for-step/).

### Candidate prompt

Let `n≥3` and let `x1,x2,...,xn` be positive real numbers whose sum is 1. Prove that

`product(i=1..n) (1-xi) ≥ (n-1)^n product(i=1..n) xi`.

Determine when equality holds. You may use the arithmetic–geometric mean inequality, but you must state where and how it is applied.

### Proposed solution

For each fixed `i`,

`1-xi = sum(j≠i) xj`.

Applying AM–GM to the `n-1` positive terms with indices other than `i` gives

`1-xi ≥ (n-1) (product(j≠i) xj)^(1/(n-1))`.

Multiply these `n` inequalities. The constant factors produce `(n-1)^n`. In the product of products, each `xj` appears for every `i≠j`, exactly `n-1` times. After raising to the power `1/(n-1)`, the remaining factor is `product(j=1..n) xj`. This proves the claim.

Equality in every AM–GM application requires, for each `i`, all `xj` with `j≠i` to be equal. Together these conditions imply `x1=...=xn=1/n`. Conversely, that choice gives equality.

### Key observations

- The challenge is coordinating `n` separate AM–GM inequalities.
- Candidates must count how often each variable appears after multiplication.
- Equality must hold simultaneously in every component inequality.

### Scoring rubric (20 points)

| Evidence | Points |
| --- | ---: |
| Rewrites `1-xi` as the sum of the other variables | 3 |
| Applies AM–GM correctly for a fixed index | 5 |
| Multiplies all `n` inequalities correctly | 4 |
| Counts each variable's exponent correctly | 4 |
| Determines and verifies equality | 3 |
| Clear presentation | 1 |
