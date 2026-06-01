# Public Release Checklist

Use this checklist before changing the repository visibility to public.

## Required before publishing

- [ ] Confirm all examples are fictional and public-safe.
- [ ] Confirm no real MCP server manifests, private tool schemas, internal endpoints, credentials, connector details, or account identifiers are committed.
- [ ] Confirm no customer, employer, vendor, or client data is included.
- [ ] Confirm no private security policies, internal escalation paths, or incident details are included.
- [ ] Confirm no API keys, tokens, credentials, private paths, or emails are present.
- [ ] Confirm the README does not imply security certification, compliance certification, or vendor endorsement.
- [ ] Confirm the checklist is framed as a starting point, not a complete security framework.

## Recommended before promotion

- [ ] Add one fictional filled checklist example.
- [ ] Add a machine-readable checklist schema.
- [ ] Add a severity/likelihood scoring model.
- [ ] Add sample mitigations for common MCP risks.
- [ ] Add references to public security and agent-safety resources.

## Final manual review

Before publishing, search the repo for internal tool names, endpoints, secrets, private prompts, customer names, employer names, emails, tokens, keys, and real incident details.

This checklist is a publication aid, not a security guarantee.
