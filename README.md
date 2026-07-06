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

## Provider

- Provider id: `confluence`
- API hosts: `*.atlassian.net` and `api.atlassian.com`
- Recommended OAuth scopes for artifact workflows:
  - `read:page:confluence`
  - `read:attachment:confluence`
  - `write:page:confluence`

Confluence Cloud does not currently expose an official REST page-to-PDF export
endpoint. `artifact.export_request({format: "pdf"})` returns an explicit
`unsupported_pdf_export` error instead of using undocumented UI endpoints.

## Useful Methods

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

## References

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

## Validation

```sh
harn connector test . --provider confluence
```

The smoke tests use Harn HTTP mocks and do not call Atlassian APIs.
