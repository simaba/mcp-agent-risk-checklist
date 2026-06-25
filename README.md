# MCP Agent Risk Checklist

A lightweight, public-safe review aid for Model Context Protocol (MCP) servers, tools, and agent integrations.

## Maturity

**Early practitioner toolkit.**

This repository provides a structured checklist, fictional review schema/example, risk-scoring guidance, and common mitigation prompts. It is not a security framework, automated scanner, formal assessment, or compliance tool.

## Start here

- [Fictional risk-review schema](schemas/mcp-risk-review.schema.json)
- [Filled fictional review](examples/fictional-mcp-risk-review.json)
- [Risk scoring guidance](docs/RISK_SCORING.md)
- [Common mitigations](docs/COMMON_MITIGATIONS.md)
- [Changelog](CHANGELOG.md)

## Purpose

MCP-style tool access can make agents more useful, but it expands the risk surface. A practical review should ask whether an agent can access, modify, expose, or misuse data or tools in ways that were not intended.

## Review areas

1. **Tool scope** — separate read-only, write-capable, destructive, and externally visible tools.
2. **Permission boundaries** — define identity, least privilege, revocation, and access review.
3. **Data exposure** — minimize data, redact sensitive fields, and protect logs.
4. **Prompt injection and tool misuse** — treat retrieved content as untrusted and validate tool calls.
5. **Auditability** — retain privacy-aware records of allow/deny decisions and results.
6. **Failure modes** — bound retries, validate responses, degrade safely, and define remediation.
7. **Human oversight** — define approval thresholds, accountable owners, and escalation paths.

## Publication safety

Use only fictional or fully sanitized examples.

Do not publish real MCP server configurations, tool manifests, private schemas, internal endpoints, credentials, customer data, audit logs, incident details, permission maps, or proprietary agent policies.

## Out of scope

This repository does not provide:

- automated MCP security scanning
- complete coverage of all agent-tool risks
- security or compliance certification
- formal security review
- vendor endorsement
- production-readiness certification

## Next quality steps

1. add a local validator for the bundled schema
2. add more fictional examples for write-capable and externally visible tools
3. add a versioned reference list to primary public security and MCP resources
4. add tests for schema examples and risk-level calculation

## Scope and disclaimer

This repository is shared in a personal capacity. It is not security certification, legal advice, compliance certification, or official guidance from any vendor, standards body, or employer.

Use the checklist as a starting point. Real agent-tool deployments should be reviewed by qualified security, privacy, legal, compliance, and system owners before production use.

---

*Maintained by [Sima Bagheri](https://github.com/simaba).*