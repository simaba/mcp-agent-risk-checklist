# Risk Scoring Guidance

This is a lightweight prioritization aid for fictional or sanitized MCP/agent-tool reviews. It is not a formal security assessment or a substitute for qualified security, privacy, legal, or system-owner review.

## Score likelihood and impact

Score each from 1 to 5.

| Score | Likelihood | Impact |
|---:|---|---|
| 1 | Rare under the defined fictional conditions | Minimal, reversible inconvenience |
| 2 | Unlikely | Limited local disruption or rework |
| 3 | Plausible | Material workflow, data, or trust impact |
| 4 | Likely without a control | Serious security, privacy, reliability, or business impact |
| 5 | Expected or easily triggered | Severe, broad, irreversible, or high-impact harm |

## Map the product to a risk level

| Likelihood × impact | Suggested level |
|---:|---|
| 1–4 | Low |
| 5–9 | Medium |
| 10–16 | High |
| 17–25 | Critical |

Use judgment: a low-probability scenario can still be treated as critical when a non-negotiable security, safety, legal, privacy, or access-control boundary is involved.

## Decision rules

- **Critical:** block connection or rollout until the issue is removed or accepted through an accountable formal process outside this repository.
- **High:** require a named mitigation, owner, due date, and review before expansion.
- **Medium:** document mitigation and monitor before broader use.
- **Low:** record the rationale and review if scope changes.

## Required review context

A review should identify the tool scope, identity/permission boundary, accessible data, write/destructive capability, human-approval requirements, audit logging, failure behavior, and rollback/remediation path.

Never use a numeric score to override a failed non-negotiable control such as unrestricted credentials, unapproved data exposure, absence of required human confirmation, or missing access revocation.