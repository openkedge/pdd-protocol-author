# Ambiguity Taxonomy

Use this reference when converting human language into PDD constraints.

## Structural Ambiguity

Signals:

- "user object"
- "metadata"
- "payload"
- "valid request"
- "error response"

Resolution:

- Define schemas.
- Specify required fields, optional fields, nullability, enums, default values, and error variants.
- Add versioning and compatibility rules.

## Behavioral Ambiguity

Signals:

- "safe"
- "idempotent"
- "deduplicate"
- "handle errors"
- "retryable"
- "deterministic"
- "preserve order"

Resolution:

- Turn prose into predicates, examples, or property-based tests.
- Define state transitions.
- Specify what happens on invalid input, partial failure, retries, and duplicate requests.

## Operational Ambiguity

Signals:

- "fast"
- "cheap"
- "not too many calls"
- "do not overload"
- "secure"
- "no side effects"
- "best effort"

Resolution:

- Add explicit limits for latency, memory, CPU, network, disk, database calls, retries, concurrency, secrets, and dependencies.
- State whether limits are admission requirements or monitoring goals.

## Authority Ambiguity

Signals:

- "can access user data"
- "may call services"
- "uses credentials"
- "admin operation"

Resolution:

- Define allowlists and deny-by-default behavior.
- Specify scopes, roles, identity requirements, and audit logging.

## Evidence Ambiguity

Signals:

- "tested"
- "verified"
- "passed CI"
- "safe to deploy"

Resolution:

- Specify validator versions, logs, artifact hashes, dependency manifests, coverage summaries, sandbox traces, and signed attestations.

## Decision Rule

Ask a blocking question only when no conservative default is safe. Otherwise, make the default explicit in `ambiguity-log.md`.
