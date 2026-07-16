# MCP Authority and Containment Review

An MCP server or agent-tool integration should be reviewed as an authority boundary, not only as a list of endpoints. The important question is not “Is the tool trusted?” It is: which principal can cause which state change, against which data, under what confirmation and containment controls?

## 1. Principal binding

Record:

- the human, service, tenant, or organization on whose behalf the agent acts;
- how identity and tenant context are established;
- whether the MCP server can distinguish the end user from the calling agent or host;
- how delegated authority is represented;
- whether credentials are user-scoped, service-scoped, shared, or long-lived;
- how sessions and credentials are revoked.

A server that receives one broad service credential may be unable to enforce the end user’s actual permissions even when the UI shows an authenticated user.

## 2. Capability inventory

Classify each tool by the strongest effect it can produce.

| Capability | Examples | Review concern |
|---|---|---|
| Read | search records, retrieve documents | data minimization, tenant scope, inference and aggregation |
| Draft | create an uncommitted object | visibility, persistence, later execution path |
| Write | modify records or configuration | authorization, validation, rollback, conflict handling |
| External communication | send message, publish content, create ticket | impersonation, recipient scope, irreversible disclosure |
| Financial / contractual | purchase, transfer, accept terms | dual control, limits, legal authority |
| Code / infrastructure | execute code, deploy, change access | isolation, privilege escalation, persistence |
| Delete / destructive | remove records, revoke, reset | confirmation, recovery, retention obligations |
| Delegate | invoke another agent, workflow, or tool | authority amplification and recursive execution |

Review the effective capability, not the friendly tool name. `update_profile` may change a public identity; `run_query` may expose an entire database; `create_draft` may trigger downstream automation.

## 3. Data reach

For each tool, identify:

- systems and tenants reachable;
- data classes and fields;
- row, document, or object-level scope;
- query and aggregation capability;
- write destinations;
- data returned to the model, host, logs, and user;
- retention and deletion behavior;
- cross-border or regional constraints where applicable.

Least privilege should be enforced by the source system or server, not only by tool descriptions or prompt instructions.

## 4. Invocation contract

Define:

- strict input schema and field validation;
- allow-listed identifiers, destinations, and operations;
- server-side authorization independent of model intent;
- separation of untrusted content from control instructions;
- maximum batch, cost, rate, and concurrency;
- timeout and cancellation behavior;
- idempotency and replay protection;
- dry-run or preview support;
- result schema and verification;
- partial-failure semantics.

A valid JSON call can still be unauthorized or unsafe. Schema validation is necessary but not sufficient.

## 5. Confirmation and authorization

For consequential actions, separate:

1. **proposal** — agent drafts the intended action and relevant parameters;
2. **preview** — user sees target, effect, data, cost, and reversibility;
3. **authorization** — authenticated principal approves a specific action;
4. **execution** — server enforces authorization and performs the bounded action;
5. **verification** — resulting state is confirmed;
6. **record** — disposition and provenance are retained.

Confirmation should bind to the exact action, not a vague earlier consent. Material parameter changes after approval require renewed authorization.

## 6. Untrusted content and prompt injection

Assume that documents, webpages, messages, tool results, and stored memory can contain instructions hostile to the user’s intent.

Controls may include:

- separating retrieved content from system and policy instructions;
- preventing tool-returned text from granting new authority;
- validating destinations and arguments server-side;
- limiting which tools can follow from an untrusted source;
- requiring confirmation for external effects;
- provenance labels and source display;
- testing multi-step and indirect injection paths;
- refusing to pass secrets into content-controlled contexts.

A prompt-injection review should exercise the complete path from content to tool action, not only whether the model repeats a malicious instruction.

## 7. Supply chain and server integrity

Review:

- publisher and repository provenance;
- release and update process;
- dependency and artifact integrity;
- signing or verification where available;
- server hosting and data processing;
- telemetry and update channels;
- configuration and tool-list changes;
- vulnerability response and end-of-life policy;
- whether the server can introduce new tools without review.

Pinning a package version does not solve a compromised maintainer, hosted backend change, or mutable remote tool definition.

## 8. Observability

A useful event record should be able to reconstruct:

- principal and tenant;
- agent / host / server versions;
- tool and operation;
- authorization context;
- arguments or privacy-preserving references;
- data classification;
- result and external state verification;
- confirmation or exception;
- retry, replay, and partial failure;
- reviewer or incident disposition.

Do not log secrets or all retrieved content by default. Define access, retention, and deletion.

## 9. Containment and recovery

Test the ability to:

- disable the integration or individual tool;
- revoke credentials and sessions;
- stop queued or recursive work;
- restrict operation to read-only or draft-only mode;
- identify completed, failed, partial, and uncertain actions;
- reverse or compensate for writes;
- quarantine persisted memory or generated artifacts;
- restore a known-good server and tool configuration;
- notify affected owners or users;
- preserve evidence for investigation.

A kill switch that only hides the UI is not containment if the server, credentials, or queued actions remain active.

## 10. Decision record

Conclude the review with:

- approved principal and user population;
- permitted servers and versions;
- enabled tools and authority;
- prohibited data and actions;
- required confirmations;
- monitoring and stop conditions;
- unresolved findings and dispositions;
- residual-risk owner;
- expiry and re-review triggers;
- removal and incident owner.

Approval should expire or be invalidated by material changes to server ownership, tools, schemas, permissions, hosting, data reach, or confirmation behavior.
