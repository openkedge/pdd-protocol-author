# PDD Protocol Author

A Codex skill for turning ambiguous human-language software requirements into Protocol-Driven Development (PDD) bundles.

The skill helps developers clarify intent, expose ambiguity, and draft machine-checkable protocol artifacts:

- typed handshakes
- structural invariants
- behavioral invariants
- operational invariants
- capability manifests
- ambiguity logs
- validation plans
- evidence requirements

## Install

Copy the skill folder into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
cp -R pdd-protocol-author ~/.codex/skills/
```

Then ask Codex:

```text
Use $pdd-protocol-author to convert this requirement into a PDD bundle with structural, behavioral, and operational invariants.
```

## Example

Input:

```text
Build an API that creates a user if one does not exist. It should be safe to retry and should not call external services.
```

The skill produces a PDD bundle containing:

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

## Validate A Bundle

The skill includes a lightweight structural validator:

```bash
python3 scripts/validate_pdd_bundle.py assets/templates
```

## Core Idea

PDD treats implementation as replaceable and protocol as durable. Natural language starts the design process, but the permanent artifact is a bundle of explicit constraints that can be validated.

```text
Code is transient; protocol is sovereign.
```
