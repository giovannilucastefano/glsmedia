---
## GLS Media Custom GPT API “ViaLink”

**This document permanently describes the custom GPT API interface for the GLS Media operational assistant.

- Repo: `giovannilucastefano/glsmedia`
- Format: OpenAPI 3.1.0
- Type: `apiClient` with base64 compliance

---

## Integration Details

This api requires the following rules to manage notes within the `services` folder of the repo:

** Download note content with base64 safety

** Update notes by first getting the latest SHA via `GET`

** Sha is omitted only for new note creation

```json
put: /repos/giovannilucastefano/glsmedia/contents/{ path }
```

## Endpoints

- `\/contents`: List files and folders in root
- `/contents/{folderPath}`[get]: List files in any specific folder
- `\/contents/{path}[get]: Read note content (Base64 string)
- `/contents/{path}[put]: Create or update note. Base64 required.
- `/search/code[get]: Search Markdown notes through repo-limited code query

## Requirements & Validation

- BASE64 encoding required for all note content
- No newlines (continuous base64)
- No emojis or unicode special characters
- Aleways retrieve SHA before update to prevent conflicts

## Responses (200, UID, 422)

- 200: SUCCESS: The note was updated or retrieved
- 201: Created note
- 422: SHA mismatch or base64 error

## Components: Schemas & Support

- `FileUpdate`: Structured request body for write/update
- `FileResponse`: Read note metadata with content and SHA
- `SearchResponse`: Response for vault-level markdown search

** Uses `eos-planning` and `contentType` for metadata-categorized files

