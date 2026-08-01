---
name: Access company registry data
description: Create a case with a company, request business-registry data, and retrieve the result.
api: openapi/sikoia-openapi.yml
operations: [POST_v2-cases, POST_v2-company-registry-data, GET_v2-company-registry-data-request_id]
source: https://docs.sikoia.com/recipes/access-company-registry-data
generated: '2026-07-21'
method: generated
---

# Access company registry data

Create a case with a company, request business-registry data, and retrieve the result.

## Authentication
Obtain an OAuth 2.0 access token via `POST https://oauth2.sikoia.com/token` (grant_type=client_credentials,
scope=`https://api.sikoia.com/.default`). Send `Authorization: Bearer <token>` on every request. Tokens
expire after 1 hour. All requests and responses are JSON over HTTPS.

## Steps
1. `POST /v2/cases` (`POST_v2-cases`) — Create a case
2. `POST /v2/company-registry-data` (`POST_v2-company-registry-data`) — Request registry data
3. `GET /v2/company-registry-data/{request_id}` (`GET_v2-company-registry-data-request_id`) — Retrieve registry data

## Conventions & error handling
- Poll async request resources by `request_id` until their status is terminal (e.g. `Complete`/`Failed`).
- Reusing an idempotency key returns `409 Conflict`; a `429 RateLimit` means you exceeded 200 requests/minute.
- Every error carries `type`, `status`, `title`, `detail`, and a `correlation_id`; capture the
  `X-Correlation-Id` response header for support. See `errors/sikoia-problem-types.yml` and
  `conventions/sikoia-conventions.yml`.
