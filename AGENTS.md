# AGENTS.md

Shared connector authoring rules live in the Harn guide:

- [Connector authoring guide](https://github.com/burin-labs/harn/blob/main/docs/src/connectors/authoring.md)

Put shared connector guidance in the Harn guide and keep only
Confluence-specific notes here.

## Provider notes

- Keep API calls scoped to `*.atlassian.net` and `api.atlassian.com`.
- Use the exact page and attachment scopes declared in `harn.toml`.
- Treat page-to-PDF export as unsupported until Atlassian documents a Cloud
  REST endpoint; do not call private UI endpoints.
