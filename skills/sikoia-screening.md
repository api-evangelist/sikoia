---
name: Screen an entity for PEPs, sanctions and adverse media
description: Run PEPs & Sanctions and Adverse Media searches against a person or company entity.
api: openapi/sikoia-openapi.yml
operations: [POST_v2-peps-sanctions, POST_v2-adverse-media]
source: https://docs.sikoia.com/docs/peps-sanctions-1
generated: '2026-07-21'
method: generated
---

# Screen an entity for PEPs, sanctions and adverse media

Run PEPs & Sanctions and Adverse Media searches against a person or company entity.

## Authentication
Obtain an OAuth 2.0 access token via `POST https://oauth2.sikoia.com/token` (grant_type=client_credentials,
scope=`https://api.sikoia.com/.default`). Send `Authorization: Bearer <token>` on every request. Tokens
expire after 1 hour. All requests and responses are JSON over HTTPS.

## Steps
1. `POST /v2/peps-sanctions` (`POST_v2-peps-sanctions`) — Request PEPs & Sanctions search
2. `POST /v2/adverse-media` (`POST_v2-adverse-media`) — Request Adverse Media search

## Conventions & error handling
- Poll async request resources by `request_id` until their status is terminal (e.g. `Complete`/`Failed`).
- Reusing an idempotency key returns `409 Conflict`; a `429 RateLimit` means you exceeded 200 requests/minute.
- Every error carries `type`, `status`, `title`, `detail`, and a `correlation_id`; capture the
  `X-Correlation-Id` response header for support. See `errors/sikoia-problem-types.yml` and
  `conventions/sikoia-conventions.yml`.
