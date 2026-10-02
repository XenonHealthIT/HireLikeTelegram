# R2B: Networking

## B07 — Messages Over a TCP Byte Stream

**Source:** IETF [RFC 9293: Transmission Control Protocol](https://www.rfc-editor.org/rfc/rfc9293.html).

### Candidate prompt

A client performs two socket writes: first a 40-byte header, then a 500-byte body. The server assumes its first read returns exactly 40 bytes and its second read returns exactly 500. It intermittently sees partial headers, combined header/body data, and corrupted parsing.

Explain why TCP permits this. Design a framing and read strategy that handles partial and combined reads, malformed lengths, disconnects, and multiple messages per connection.

### Proposed answer

TCP provides an ordered, reliable byte stream; it does not preserve application write, packet, or read boundaries. One write can be split, multiple writes can be coalesced, and a read returns whatever bytes are currently available up to its buffer limit.

Use an application framing protocol: for example, a fixed-size header containing version, message type, and unsigned body length in network byte order. Accumulate until the complete header is available, validate the length against a strict maximum, then accumulate exactly that body length while retaining surplus bytes for the next frame. Treat zero-byte/end-of-stream before completion as truncation. Handle timeouts and cancellation, and reject unknown versions/types without allocating attacker-controlled sizes. Delimiter or self-describing formats are alternatives if escaping and size limits are precise.

### Key points

- Repeating `read` until a requested length is collected is necessary but must handle EOF and errors.
- “TCP packets” are not the application's framing layer.
- Backpressure and bounded buffers are part of a production answer.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct byte-stream/no-boundary explanation | 3 |
| Complete length-prefixed or equivalent framing | 3 |
| Handles partial, combined, and repeated frames | 2 |
| Validates size, EOF, malformed data, and timeout | 2 |

## B08 — Retrying an Ambiguous Payment Request

**Source:** IETF [RFC 9110: HTTP Semantics](https://www.rfc-editor.org/rfc/rfc9110.html), especially idempotent methods.

### Candidate prompt

A client sends `POST /charges`. The server commits the charge, but the connection drops before the response arrives. The client retries and the customer is charged twice.

Design client and server behavior that tolerates this ambiguous outcome. Explain the difference between HTTP method idempotency and an operation made idempotent by application design.

### Proposed answer

The client cannot infer from a missing response whether the server applied the request. POST is not inherently idempotent, so blind retries can repeat the effect. Give each logical operation a client-generated idempotency key. The server atomically records the key, a hash of relevant request parameters, status, and result with the charge transaction. A repeat with the same key and same parameters returns the original result; the same key with different parameters is rejected. Concurrent duplicates require a unique constraint or equivalent serialization, not a check-then-insert race.

The client may retry timeouts with the same key and bounded backoff. Key records need a retention period at least as long as retries. A method being defined as idempotent describes intended repeated effect; logging may still repeat. Application semantics can make a particular POST safely repeatable even though POST is not generally idempotent.

### Key points

- Exactly-once delivery is not achieved; deduplication makes the business effect effectively once within a defined scope.
- The charge and idempotency record must be committed consistently.
- Status lookup/reconciliation is useful when the downstream payment provider is also ambiguous.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Recognizes the ambiguous commit outcome | 2 |
| Designs client-generated idempotency keys and replay | 3 |
| Makes deduplication atomic under concurrency | 2 |
| Handles parameter mismatch, retention, and retry policy | 2 |
| Correctly distinguishes protocol and application idempotency | 1 |

## B09 — DNS Cutover and Stale Answers

**Source:** IETF [RFC 1034: Domain Names—Concepts and Facilities](https://www.rfc-editor.org/rfc/rfc1034.html).

### Candidate prompt

An API's DNS A record has a 24-hour TTL. At noon the team changes it to a new IP and immediately shuts down the old endpoint. Some users reach the new service while others fail for most of the day. The team claims that authoritative DNS already shows the new value.

Explain the behavior and propose a safe planned migration plus an emergency mitigation.

### Proposed answer

Recursive resolvers and clients may reuse the old resource record until the TTL they received expires. Changing the authoritative value does not invalidate distributed caches. For a planned cutover, lower the TTL at least one old-TTL interval before migration, wait for previous cached records to age out, bring up the new endpoint, change the record, keep the old endpoint working through the remaining cache horizon, monitor both, then raise the TTL later.

For an emergency, restore or redirect/proxy traffic at the old IP if possible, keep both endpoints valid, or move routing/load-balancer configuration behind a stable address. Lowering TTL after the incident begins does not shorten TTLs already cached. Some local components may cache beyond expectations, so retain operational margin.

### Key points

- TTL governs cached data from the time it was learned.
- DNS propagation is not a single global push event.
- Negative caching can produce a similar problem when a name was previously nonexistent.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Correct distributed caching/TTL explanation | 3 |
| Safe pre-lowered-TTL migration sequence | 3 |
| Keeps old endpoint viable through cache expiry | 2 |
| Useful emergency mitigation | 1 |
| Mentions negative/local caching nuance | 1 |

## B10 — Incorrect Shared HTTP Cache

**Source:** IETF [RFC 9111: HTTP Caching](https://www.rfc-editor.org/rfc/rfc9111.html) and [RFC 9110 conditional requests](https://www.rfc-editor.org/rfc/rfc9110.html#name-conditional-requests).

### Candidate prompt

`GET /dashboard` returns user-specific HTML after authentication. A newly added CDN occasionally serves one user's dashboard to another. Separately, a public catalog endpoint is re-downloaded in full even when unchanged.

Diagnose both behaviors. Specify safer response headers/cache keys for the dashboard and an efficient revalidation design for the catalog.

### Proposed answer

A shared cache must not reuse a private personalized response across users. Prefer `Cache-Control: private, no-store` for highly sensitive dashboard content, with `no-store` preventing storage; do not depend on cookies being automatically part of the cache key. If shared caching is truly required, explicitly vary/key by every representation-selecting attribute and ensure authorization rules permit it, but this is risky for personalized pages.

For the catalog, return a validator such as an ETag plus an appropriate freshness lifetime. Once stale, the client/cache sends `If-None-Match`; the origin returns `304 Not Modified` when the representation is unchanged or `200` with a new body/ETag when changed. `Vary` must list request headers that select different representations, such as content encoding or language.

### Key points

- `no-cache` means revalidate before reuse; it does not mean “do not store.”
- `private` limits shared-cache storage; `no-store` is stronger for sensitive content.
- Cache key correctness and freshness are separate concerns.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Identifies cross-user cache-key/storage failure | 3 |
| Proposes safe dashboard cache directives | 2 |
| Correct ETag/conditional-request flow | 2 |
| Correctly explains `no-cache`, `no-store`, `private`, or `Vary` | 2 |
| Notes authorization/security tradeoff | 1 |

## B11 — TLS Works, but Identity Is Not Verified

**Source:** IETF [RFC 8446: TLS 1.3](https://www.rfc-editor.org/rfc/rfc8446.html) and [RFC 9525: Service Identity in TLS](https://www.rfc-editor.org/rfc/rfc9525.html).

### Candidate prompt

An internal client connects with TLS and verifies that the server certificate chains to a trusted corporate CA, but it disables hostname verification because services move between hosts. A penetration test demonstrates a machine with a different valid corporate certificate intercepting traffic.

Explain why encryption and chain validation were insufficient. Design correct service-identity verification and a workable certificate-rotation procedure.

### Proposed answer

TLS can encrypt traffic to an authenticated key, but the client must establish that the certificate represents the intended service. Trusting any certificate from the corporate CA authenticates only membership in that trust domain, so another valid certificate can terminate the connection. The client should derive a reference identity from configured service discovery or the requested URI and compare it with an appropriate `subjectAltName` identifier while validating the chain, validity period, key usage, revocation policy where applicable, and TLS parameters. Do not fall back to an arbitrary Common Name or disable checks.

For rotation, issue a new certificate whose identities overlap the service's stable name, distribute trust chain updates before switching if needed, support both old and new certificates during an overlap window, rotate private keys securely, monitor handshake failures/expiry, then revoke or retire the old credential. Service names should remain stable even when hosts change.

### Key points

- Confidentiality without correct peer identity remains vulnerable to interception.
- Certificate pinning can reduce CA scope but creates a rotation/recovery burden; pinning a managed issuer or public key with backup pins may be safer than a single leaf.
- SNI selection is not itself certificate verification.

### Evaluation matrix (10 points)

| Evidence | Points |
| --- | ---: |
| Distinguishes chain trust from service identity | 3 |
| Correct SAN/reference-identity verification | 3 |
| Preserves stable service naming across hosts | 1 |
| Safe overlapping rotation procedure | 2 |
| Pinning/SNI/revocation nuance | 1 |
