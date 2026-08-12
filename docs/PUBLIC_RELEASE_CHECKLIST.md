# Public Release Checklist

Complete this checklist before making the repository public or publishing a versioned release.

## Content safety

- [ ] Confirm all tool manifests, permissions, logs, incidents, risk reviews, mitigations, and examples are fictional or fully sanitized.
- [ ] Confirm no real endpoints, credentials, server configuration, tenant or workspace identifiers, customer data, audit records, proprietary policies, private tool schemas, or internal escalation paths are present.
- [ ] Confirm no employer, customer, vendor, or client data is included.
- [ ] Confirm no API keys, tokens, credentials, private paths, or private email addresses are present.

## GitHub surfaces

- [ ] Review all branches and the complete git history for material that should not become public.
- [ ] Review issues, pull requests, comments, Actions logs and artifacts, releases, tags, attachments, and repository metadata.

## Quality baseline

- [ ] Confirm the schema and example use only fictional names and do not imply a real security approval.
- [ ] Confirm the README, scoring guidance, authority model, and mitigations accurately describe the repository as a practitioner review aid, not a scanner, certification, or production-readiness assessment.
- [ ] Confirm the checklist is framed as a starting point rather than a complete security framework.
- [ ] Validate the fictional example against the schema on the intended release commit.
- [ ] Confirm public security and agent-safety references, where used, are current and accurately characterized.

## Release practice

- [ ] Search the repository for internal tool names, endpoints, secrets, private prompts, customer or employer names, emails, tokens, keys, and real incident details before release.
- [ ] Create a draft release and inspect all notes and assets before publishing.

This review does not replace qualified security, privacy, legal, compliance, or system-owner approval.
