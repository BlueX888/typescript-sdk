---
'@modelcontextprotocol/express': patch
'@modelcontextprotocol/server': patch
---

A request that presented no credentials no longer gets `error="invalid_token"` in its `WWW-Authenticate` challenge: following RFC 6750 §3.1, the error code is omitted whenever another auth-param (`scope` or `resource_metadata`) remains, so a fresh client's first 401 tells it to authenticate rather than implying its token went bad. A presented-but-rejected token keeps `error="invalid_token"`, and with neither scopes nor `resourceMetadataUrl` configured the challenge is unchanged, since §3 requires at least one auth-param after the scheme. The JSON error body is unchanged.
