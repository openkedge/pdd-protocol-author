---
name: pdd-protocol-author
description: Convert ambiguous human-language software requirements into Protocol-Driven Development (PDD) bundles. Use when Codex should clarify requirements, identify ambiguity, draft typed handshakes, structural/behavioral/operational invariants, capability manifests, validation plans, evidence requirements, or write a reusable PDD protocol bundle for a feature, API, service, pipeline, library module, or agentic workflow.
---

# PDD Protocol Author

## Overview

Use this skill to turn human intent into a machine-checkable PDD bundle. Treat natural language as a starting point, not the final artifact: extract intent, expose ambiguity, make conservative assumptions, and emit structural, behavioral, and operational constraints.

## Operating Mode

- If the user asks for a bundle, create files.
- If the user asks for design help, return the bundle in Markdown/YAML without writing files.
- If the requirement is too ambiguous to proceed safely, ask up to three blocking questions. Otherwise proceed with explicit assumptions and an ambiguity log.
- Default to language-neutral JSON Schema plus YAML manifests unless the user requests OpenAPI, Protobuf, TypeScript, Zod, Rego, TLA+, or another stack.

## Workflow

1. Extract intent.
   - Identify component name, purpose, inputs, outputs, state, dependencies, side effects, failure modes, users, and trust boundaries.
   - Define the protocol boundary: what is inside the component and what remains external.

2. Scan for ambiguity.
   - Flag words such as "safe", "fast", "valid", "secure", "reasonable", "retryable", "handle errors", "near real time", "best effort", and "should not call too much".
   - Resolve ambiguity by turning vague prose into explicit constraints, assumptions, or open questions.
   - Use `references/ambiguity-taxonomy.md` when the requirement has many vague phrases.

3. Draft typed handshakes.
   - Specify request, response, event, or file schemas.
   - Include required/optional fields, nullability, enums, error variants, versioning, idempotency keys, and compatibility rules.
   - Prefer small stable schemas over broad object blobs.

4. Author invariants.
   - Structural invariants (`S`): schema, interface, versioning, compatibility, serialization, and error-shape constraints.
   - Behavioral invariants (`B`): idempotence, determinism, monotonicity, ordering, conservation, authorization, failure semantics, data integrity, and state transition properties.
   - Operational invariants (`O`): network, disk, database calls, latency, memory, CPU, secrets, concurrency, dependency allowlists, logging, and background work.
   - Use `references/invariant-patterns.md` for common invariant templates.

5. Define validators and evidence.
   - Map each invariant to at least one validation method: schema validation, unit/property test, fuzzing, sandbox policy, static analysis, runtime instrumentation, provenance check, or manual review gate.
   - Specify evidence artifacts: validation logs, hashes, dependency lockfiles, sandbox traces, coverage summaries, signed attestations, and Discovery Logs.

6. Emit the PDD bundle.
   - For file output, use this structure by default:
     ```text
     pdd-bundles/<protocol-name>/
     ├── protocol.yaml
     ├── schemas/
     │   ├── request.schema.json
     │   └── response.schema.json
     ├── capability-manifest.yaml
     ├── invariants/
     │   ├── structural.yaml
     │   ├── behavioral.yaml
     │   └── operational.yaml
     ├── validators/
     │   └── validation-plan.yaml
     ├── ambiguity-log.md
     └── evidence-requirements.yaml
     ```
   - Start from `assets/templates/` when creating files.
   - Run `scripts/validate_pdd_bundle.py <bundle-dir>` after creating or editing a bundle.

## Output Requirements

Every completed bundle should include:

- A short protocol purpose and boundary.
- Canonical typed handshake(s).
- At least one invariant in each class: structural, behavioral, operational.
- An ambiguity log with resolved assumptions and open questions.
- A validation plan that links invariants to validator mechanisms.
- Evidence requirements sufficient for audit and regeneration.

## Authoring Rules

- Do not invent domain facts silently. Mark assumptions.
- Prefer explicit numeric limits over vague adjectives.
- Prefer protocol-visible behavior over implementation internals.
- Keep implementation suggestions optional; PDD governs admission, not style.
- Distinguish "must" invariants from "should" preferences.
- Do not claim a property is proven unless the validator plan can establish it under stated assumptions.
- If a requirement conflicts with an operational invariant, surface the conflict before writing implementation guidance.

## References

- `references/pdd-bundle-spec.md`: bundle file contract and field meanings.
- `references/ambiguity-taxonomy.md`: common ambiguity classes and how to resolve them.
- `references/invariant-patterns.md`: reusable structural, behavioral, and operational invariant patterns.
- `references/examples.md`: worked examples from natural language to PDD bundle.
