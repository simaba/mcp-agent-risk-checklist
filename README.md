# MCP Agent Risk Checklist

A practitioner review toolkit for Model Context Protocol servers, tools, and agent integrations, centered on identity, authority, data reach, invocation controls, containment, and recovery.

The repository is intentionally review-oriented. It does not scan a server or declare an integration secure. It helps a reviewer describe what the integration can do, how authority is granted, which failures matter, and what evidence is required for a bounded decision.

## Start here

| Artifact | Use it for |
|---|---|
| [`docs/AUTHORITY_MODEL.md`](docs/AUTHORITY_MODEL.md) | principal binding, capability inventory, data reach, invocation contract, confirmation, supply chain, containment, and recovery |
| [`docs/RISK_SCORING.md`](docs/RISK_SCORING.md) | scenario-based risk characterization without over-relying on a 5×5 matrix |
| [`schemas/mcp-risk-review.schema.json`](schemas/mcp-risk-review.schema.json) | machine-readable fictional review record |
| [`examples/fictional-mcp-risk-review.json`](examples/fictional-mcp-risk-review.json) | public-safe example aligned to the schema |
| [`docs/COMMON_MITIGATIONS.md`](docs/COMMON_MITIGATIONS.md) | mitigation prompts to adapt and verify |

## The review question

Do not begin with “Is this MCP server trusted?”

Begin with:

> Which principal can cause which read, write, communication, financial, code, configuration, deletion, or delegated action against which data and systems—and how can that authority be verified, constrained, revoked, and recovered?

The answer may differ by tool, user, tenant, environment, and workflow state. One server-wide risk label is rarely enough.

## Review model

### 1. Principal and identity

- Who is the agent acting for?
- Can the server enforce the end user’s permissions, or does it receive one broad service credential?
- How is tenant context bound and verified?
- Can credentials or sessions be revoked quickly?
- Can delegated authority exceed the caller’s authority?

### 2. Effective capability

Classify tools by effect, not name:

- read and aggregate;
- create draft;
- write or change configuration;
- communicate externally;
- create financial or contractual commitment;
- execute code or infrastructure action;
- delete or revoke;
- delegate to another tool, workflow, or agent.

A tool described as “draft” may still persist data or trigger another automation. A tool described as “query” may expose an entire tenant.

### 3. Data reach

Record systems, tenants, fields, sensitivity, aggregation, write destinations, result exposure, logging, retention, and deletion. Enforce least privilege at the server or source system; a prompt instruction is not an access-control boundary.

### 4. Invocation contract

Review:

- schema and semantic validation;
- server-side authorization;
- allow-listed operations, targets, and destinations;
- untrusted-content separation;
- rate, batch, cost, and concurrency limits;
- timeout, cancellation, idempotency, and replay;
- dry-run or preview capability;
- result verification and partial-failure semantics.

Valid JSON does not imply authorized or safe action.

### 5. Confirmation and execution

For consequential actions, separate:

```text
propose → preview → authorize → execute → verify → record
```

Authorization should bind to the exact action and parameters. If the destination, amount, record set, or effect changes after approval, require renewed authorization.

### 6. Untrusted content

Test the full path from retrieved or tool-returned content to action. Documents, webpages, messages, and memory may contain instructions hostile to the user’s intent.

Controls should prevent content from:

- changing policy or granting authority;
- selecting unauthorized tools or destinations;
- extracting secrets;
- bypassing confirmation;
- creating recursive or persistent behavior;
- turning a data result into an executable instruction without validation.

### 7. Supply chain

Review publisher provenance, code and artifact integrity, dependencies, hosted backend, update channels, mutable tool lists, telemetry, vulnerability response, and end-of-life. A pinned client version does not control an unversioned hosted server or a compromised maintainer.

### 8. Observability

Retain enough privacy-aware provenance to reconstruct principal, server and tool version, authorization, operation, result, confirmation, retry/replay, and external-state verification.

Avoid logging secrets and full sensitive content by default. Define access, retention, and deletion.

### 9. Containment and recovery

Test the ability to:

- disable one tool or the integration;
- revoke credentials and sessions;
- stop queued and recursive actions;
- move to read-only or draft-only mode;
- identify completed, partial, failed, and uncertain actions;
- reverse or compensate for changes;
- quarantine memory and artifacts;
- restore and verify a known-good state.

A UI toggle is not a kill switch when the server, credential, or queue remains active.

## Risk characterization

The review uses specific scenarios and several dimensions:

- authority;
- data reach;
- externality;
- principal binding;
- exposure;
- recoverability;
- control confidence;
- likelihood and impact.

Likelihood × impact can help sort a queue, but it is an ordinal aid rather than calibrated expected loss. Hard boundaries are evaluated separately.

See [`docs/RISK_SCORING.md`](docs/RISK_SCORING.md).

## Decision outcomes

| Outcome | Use when |
|---|---|
| **Block / redesign** | authority or data boundary is absent, unbounded, or unrecoverable |
| **Pilot with conditions** | users, data, tools, authority, and exposure can be tightly constrained |
| **Approve bounded use** | evidence supports the exact reviewed scope and residual risk is accepted |
| **Defer** | evidence or ownership is missing and a safe bounded test is not justified |
| **Remove** | the capability is unnecessary or creates more risk than product value |

The decision should record permitted tools and versions, prohibited actions and data, confirmation requirements, monitoring, stop conditions, owner, expiry, and re-review triggers.

## Machine-readable review

The schema and example support consistent review records. Validation confirms structure; it does not prove that the permission boundary, risk estimate, mitigation, or decision is correct.

```bash
python scripts/validate_examples.py
```

## Quality standard

A strong contribution should add:

- a concrete authority or data-flow scenario;
- a control with enforcement and test evidence;
- a failure or bypass path;
- a containment or recovery exercise;
- a schema rule that catches a meaningful review defect;
- a source or platform change that materially alters the review model.

Avoid generic security advice that cannot be tied to a tool capability, principal, data boundary, or observable control.

## Publication safety

Use only fictional or fully sanitized examples. Do not publish real tool manifests, server configurations, endpoints, credentials, private schemas, customer data, permission maps, audit logs, incidents, or proprietary policies.

## Maturity and scope

This is an early practitioner review toolkit. It is not an automated scanner, penetration test, formal threat model, security assessment, legal review, compliance certification, or official guidance from an MCP or platform provider.

Real integrations require qualified security, privacy, legal, compliance, product, and system-owner review appropriate to the granted authority and affected systems.

---

*Maintained by [Sima Bagheri](https://github.com/simaba).*
