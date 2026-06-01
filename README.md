# MCP Agent Risk Checklist

A lightweight checklist for reviewing Model Context Protocol (MCP) servers, tools, and agent integrations before they are used in agentic workflows.

## Status

**Initial checklist draft.**

This repository is currently a public-ready starting point for structured MCP and agent-tool risk review. It is not yet a full security framework, automated scanner, or formal compliance tool.

## Why this exists

MCP-style tool access can make agents more useful, but it also expands the risk surface. A practical review should ask whether the agent can access, modify, exfiltrate, or misuse data or tools in ways that were not intended.

This checklist focuses on the operational questions teams should ask before connecting tools to agents.

## Checklist areas

### 1. Tool scope

- What tools does the MCP server expose?
- Are any tools write-capable, destructive, or externally visible?
- Are tool names, descriptions, and parameters clear enough for safe selection?
- Are dangerous actions separated from read-only actions?

### 2. Permission boundaries

- What account, workspace, or system identity does the tool run as?
- Does the agent receive broader access than the human user intended?
- Are least-privilege permissions enforced?
- Can permissions be reduced, revoked, or audited?

### 3. Data exposure

- What data can the agent read through the tool?
- Could the tool expose secrets, credentials, private documents, customer data, or internal records?
- Are sensitive fields filtered or redacted before agent access?
- Are logs safe to store and review?

### 4. Prompt injection and tool misuse

- Could retrieved content instruct the agent to misuse tools?
- Are tool calls validated against policy before execution?
- Are high-impact actions confirmed by a human?
- Are unexpected tool-call chains detected or blocked?

### 5. Auditability

- Are tool calls logged with timestamp, actor, parameters, and result summary?
- Can reviewers reconstruct why the agent used a tool?
- Are failed, denied, or escalated calls recorded?
- Are logs protected from unauthorized access?

### 6. Failure modes

- What happens if the tool returns stale, partial, malformed, or adversarial data?
- Does the agent fail safely when a tool is unavailable?
- Are retries bounded?
- Is there a rollback or remediation path for write actions?

### 7. Human oversight

- Which actions require human confirmation?
- Who owns approval for high-risk tool access?
- Who reviews incidents or unexpected behavior?
- Is there a clear escalation path?

## Public-safe use rule

Do not publish real MCP server configurations, private tool schemas, internal endpoints, credentials, customer data, or proprietary agent policies in this repository.

Use fictional examples when demonstrating:

- tool manifests
- permission models
- logs
- incident scenarios
- approval workflows
- risk assessments

## What this repo does not claim yet

This repo does **not** yet claim:

- automated MCP security scanning
- complete coverage of all agent-tool risks
- compliance certification
- formal security review
- vendor endorsement
- production-readiness certification

## Next maturity step

To make this repository stronger, add:

1. a machine-readable checklist schema
2. a filled fictional example review
3. a CLI that validates a checklist file
4. risk scoring guidance by severity and likelihood
5. sample mitigations for common MCP failure modes
6. links to relevant public security and agent-safety resources

## Scope and disclaimer

This repository is shared in a personal capacity. It is not security certification, legal advice, compliance certification, or official guidance from any vendor, standards body, or employer.

Use this checklist as a starting point. Real agent-tool deployments should be reviewed by qualified security, privacy, legal, compliance, and system owners before production use.

---

*Maintained by [Sima Bagheri](https://github.com/simaba).*
