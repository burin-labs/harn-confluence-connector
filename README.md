# harn-confluence-connector

Pure-Harn Confluence connector for page and attachment artifact workflows.

The surface is deliberately connector-shaped, not document-renderer shaped:

- Normalize Confluence Cloud webhook deliveries into Harn connector events.
- Poll Confluence CQL search from Harn-managed cursor state.
- Dispatch common page, space-page, attachment, and CQL APIs through allowlisted
  egress descriptors.
- Build deterministic request descriptors for page body export, attachment
  download, and page create/update import flows.

Document rendering and manifest vocabulary stay in `harn-documents`; this
package owns the external Confluence boundary.

## Install

```sh
harn add github.com/burin-labs/harn-confluence-connector@v0.1.0
```

For local development, use a path dependency on this checkout. Use the Harn
CLI version pinned in `.harn-version` for validation.

## Configure

- Provider id: `confluence`
- API hosts: `*.atlassian.net` and `api.atlassian.com`
- Required secrets: `confluence/access-token`, `confluence/site-base-url`
- Required OAuth scopes: `read:page:confluence`, `read:attachment:confluence`,
  `write:page:confluence`

Start browser-based setup with `harn connect confluence`. Check its status with
`harn connect status --connector confluence --json`.

Confluence Cloud does not currently expose an official REST page-to-PDF export
endpoint. `artifact.export_request({format: "pdf"})` returns an explicit
`unsupported_pdf_export` error instead of using undocumented UI endpoints.

## Useful methods

- `pages.list`
- `pages.get`
- `pages.create`
- `pages.update`
- `pages.delete`
- `spaces.pages`
- `attachments.get`
- `attachments.for_page`
- `attachments.download`
- `search.cql`
- `artifact.export_request`
- `artifact.import_request`

## Provider references

- Confluence REST API v2:
  <https://developer.atlassian.com/cloud/confluence/rest/v2/>
- Page API:
  <https://developer.atlassian.com/cloud/confluence/rest/v2/api-group-page/>
- Attachment API:
  <https://developer.atlassian.com/cloud/confluence/rest/v2/api-group-attachment/>
- CQL content search:
  <https://developer.atlassian.com/cloud/confluence/rest/v1/api-group-content/#api-wiki-rest-api-content-search-get>
- Webhooks:
  <https://developer.atlassian.com/cloud/confluence/modules/webhook/>
- Atlassian Cloud PDF export feature request:
  <https://jira.atlassian.com/browse/CONFCLOUD-61557>

## Validate

```sh
harn connector test . --provider confluence
```

The smoke tests use Harn HTTP mocks and do not call Atlassian APIs.
