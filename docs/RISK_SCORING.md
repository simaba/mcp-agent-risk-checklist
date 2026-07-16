# MCP Risk Characterization

A likelihood × impact score can help order a review list, but it is not a sufficient model for an agent-tool integration. The effective risk also depends on authority, data reach, reversibility, exposure, and confidence in the controls.

Use the numeric score only as one view. Never allow it to override a failed non-negotiable boundary.

## Step 1: Define the scenario

Write a specific cause → action → consequence chain.

Weak:

> The MCP server could be insecure.

Stronger:

> Untrusted text retrieved from a support ticket instructs the agent to invoke a write-capable account tool; the server accepts the shared service credential without checking the end user, causing an unauthorized account change.

A scenario should identify:

- initiating condition;
- principal and identity context;
- server, tool, and data involved;
- action path;
- affected people or systems;
- consequence;
- control expected to prevent, detect, or recover.

## Step 2: Characterize capability and exposure

| Dimension | Low | Medium | High / critical concern |
|---|---|---|---|
| Tool authority | read-only, narrow | bounded write or external draft | destructive, financial, code, access, publish, recursive delegation |
| Data reach | public or synthetic | tenant-scoped operational data | sensitive, cross-tenant, secrets, broad query/aggregation |
| Externality | private and easily reversible | internally visible or recoverable | public, legal, financial, physical, safety-relevant, hard to reverse |
| Principal binding | end-user authorization enforced | mixed user/service context | shared or ambiguous identity; server cannot enforce user rights |
| Exposure | small bounded pilot | broader internal population | external users, high volume, unattended or recursive execution |
| Recoverability | verified rollback | manual compensation | irreversible, partial-state uncertainty, no reliable recovery |
| Control confidence | tested in the full path | design reviewed, limited exercise | prompt-only, untested, bypassable, or owner unclear |

These dimensions are not meant to be summed mechanically. They explain why two scenarios with the same likelihood-impact product may deserve different decisions.

## Step 3: Estimate likelihood and impact

Use a 1–5 ordinal scale with written rationale.

| Score | Likelihood guide | Impact guide |
|---:|---|---|
| 1 | requires several unlikely conditions under the reviewed scope | local inconvenience, no sensitive data or durable state change |
| 2 | plausible but constrained by tested controls | limited rework or bounded internal disruption |
| 3 | credible during normal or foreseeable misuse | material workflow, privacy, financial, or trust effect |
| 4 | likely when one control fails or is bypassed | serious multi-user, security, legal, or business effect |
| 5 | expected, easily triggered, or repeatedly observed | severe, broad, irreversible, safety-relevant, or systemic effect |

Document:

- evidence for the estimate;
- time horizon and exposure assumption;
- control dependencies;
- uncertainty and disagreement;
- whether the scenario has been observed or only hypothesized.

The numbers are ordinal judgments. Multiplication is a sorting convention, not a calibrated expected-loss calculation.

## Step 4: Apply non-negotiable gates

Treat the review as blocked regardless of the numeric score when the approved use requires a boundary that is absent or unverified, such as:

- server-side authorization for the acting principal;
- tenant and data-scope enforcement;
- protection of credentials and secrets;
- confirmation for defined consequential actions;
- revocation and disable capability;
- containment of recursive or queued work;
- verification of external state change;
- required logging, incident ownership, or legal/privacy control;
- prohibition on an action or data class.

A low estimated probability does not make an unbounded catastrophic capability acceptable.

## Step 5: Record control and residual risk

For each scenario:

| Field | Content |
|---|---|
| Prevent | authorization, validation, isolation, confirmation, least privilege |
| Detect | denied calls, anomalous access, unexpected authority transition, state mismatch |
| Respond | stop, revoke, cancel, isolate, notify |
| Recover | reverse, compensate, restore, verify, remediate downstream effects |
| Evidence | test, review, log, exercise, or source |
| Owner | control and remediation owner |
| Residual risk | what remains and under which scope |
| Decision | block, redesign, pilot with conditions, approve bounded use, or defer |
| Expiry | date or change that requires re-review |

Do not mark a risk mitigated merely because a control is planned.

## Optional prioritization band

When a team needs a rough queue, the product can be used with caution:

| Likelihood × impact | Initial queue only |
|---:|---|
| 1–4 | lower priority unless a hard gate or high-authority scenario applies |
| 5–9 | review and document controls |
| 10–16 | high priority; named remediation and decision required |
| 17–25 | critical review priority |

Override the band upward for high authority, broad sensitive-data reach, weak principal binding, irreversibility, or low control confidence.

## Decision rules

- **Block / redesign:** a non-negotiable boundary fails, authority is unbounded, or recovery is not credible for the consequence.
- **Pilot with conditions:** scope, users, data, tools, and authority can be tightly bounded; monitoring and stop conditions are enforceable.
- **Approve bounded use:** evidence supports the reviewed scope and residual risk is accepted by an authorized owner.
- **Defer:** important evidence or ownership is missing and no safe bounded test is justified.
- **Remove:** the capability is not needed or creates more risk than product value.

## Review checklist

- [ ] Scenario is specific and traces content or request to tool consequence.
- [ ] Principal binding and delegated authority are explicit.
- [ ] Effective tool capability and data reach are recorded.
- [ ] Externality, exposure, and recoverability are considered.
- [ ] Likelihood and impact have evidence and uncertainty rationale.
- [ ] Hard gates are evaluated separately from the numeric score.
- [ ] Controls are tested or accurately labeled planned / unverified.
- [ ] Residual risk, owner, conditions, and expiry are recorded.
