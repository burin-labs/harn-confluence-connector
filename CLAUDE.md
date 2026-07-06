# CLAUDE.md

See `AGENTS.md` and the canonical Harn connector authoring guide:

- https://github.com/burin-labs/harn/blob/main/docs/src/connectors/authoring.md

## Provider Notes

- Keep Confluence API calls scoped to `*.atlassian.net` and
  `api.atlassian.com`.
- Prefer least-privilege Confluence page and attachment scopes for artifact
  workflows.
- Treat Confluence Cloud page-to-PDF export as unsupported by official REST API
  until Atlassian ships a documented endpoint.
