---
'@modelcontextprotocol/hono': patch
---

`createMcpHonoApp()` no longer answers `400 Invalid JSON` when a bodyless `GET`, `HEAD` or `DELETE` request, or a bodyless `POST`, carries `Content-Type: application/json`. Those requests are left unparsed for the transport to answer, so a mounted `createMcpHandler` returns `405` with `Allow: POST` for `GET`/`DELETE` and the JSON-RPC `-32700` parse error for an empty `POST`, instead of plain-text `400 Invalid JSON`. A non-empty invalid JSON body still gets `400 Invalid JSON`, and a body over `maxRequestBodySize` still gets `413`.
