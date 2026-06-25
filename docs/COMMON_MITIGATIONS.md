# Common MCP and Agent-Tool Mitigations

Use these as prompts for a context-specific review, not as proof that a deployment is safe.

| Risk area | Example mitigation patterns |
|---|---|
| Tool scope | Separate read-only, write-capable, destructive, and externally visible tools; keep tool descriptions narrow and unambiguous. |
| Permissions | Use dedicated least-privilege identities, scoped credentials, short-lived tokens where appropriate, revocation procedures, and periodic access review. |
| Data exposure | Filter/redact sensitive fields before tool exposure; minimize returned fields; define log retention and access boundaries. |
| Prompt injection | Treat retrieved content as untrusted; apply tool allowlists, structured parameter validation, policy checks, and human confirmation for high-impact calls. |
| Auditability | Log actor, tool, parameter summary, allow/deny decision, result category, and escalation; protect logs from unnecessary access. |
| Failure modes | Bound retries, define timeouts, validate tool responses, degrade safely, and provide a remediation or rollback path for write actions. |
| Human oversight | Define approval thresholds, accountable owners, escalation routes, and a process for incident review. |
| Change management | Version tool manifests, permission scopes, prompts, and policies; re-review when any boundary expands. |

Do not publish real tool manifests, permission maps, endpoints, credentials, audit logs, or incidents in public examples.