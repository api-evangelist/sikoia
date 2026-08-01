---
name: Verify income & employer
description: Attach a data source (document upload or open banking), request income & employer verification, and retrieve the result.
api: openapi/sikoia-openapi.yml
operations: [POST_v2-documents, POST_v2-income-employer, GET_v2-income-employer-request_id]
source: https://docs.sikoia.com/recipes/verify-income-employer
generated: '2026-07-21'
method: generated
---

# Verify income & employer

Attach a data source (document upload or open banking), request income & employer verification, and retrieve the result.

## Authentication
Obtain an OAuth 2.0 access token via `POST https://oauth2.sikoia.com/token` (grant_type=client_credentials,
scope=`https://api.sikoia.com/.default`). Send `Authorization: Bearer <token>` on every request. Tokens
expire after 1 hour. All requests and responses are JSON over HTTPS.

## Steps
1. `POST /v2/documents` (`POST_v2-documents`) — Upload a document to an entity
2. `POST /v2/income-employer` (`POST_v2-income-employer`) — Request income & employer verification
3. `GET /v2/income-employer/{request_id}` (`GET_v2-income-employer-request_id`) — Retrieve income & employer verification

## Conventions & error handling
- Poll async request resources by `request_id` until their status is terminal (e.g. `Complete`/`Failed`).
- Reusing an idempotency key returns `409 Conflict`; a `429 RateLimit` means you exceeded 200 requests/minute.
- Every error carries `type`, `status`, `title`, `detail`, and a `correlation_id`; capture the
  `X-Correlation-Id` response header for support. See `errors/sikoia-problem-types.yml` and
  `conventions/sikoia-conventions.yml`.
