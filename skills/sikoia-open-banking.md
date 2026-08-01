---
name: Set up an open banking connection
description: Create an Open Banking consent connection for an entity, poll its status, and read the connected account transactions.
api: openapi/sikoia-openapi.yml
operations: [POST_v2-openbanking, GET_v2-openbanking-bank_connection_id, GET_v2-bankaccounts-account_connection_id-transactions]
source: https://docs.sikoia.com/recipes/set-up-an-open-banking-connection
generated: '2026-07-21'
method: generated
---

# Set up an open banking connection

Create an Open Banking consent connection for an entity, poll its status, and read the connected account transactions.

## Authentication
Obtain an OAuth 2.0 access token via `POST https://oauth2.sikoia.com/token` (grant_type=client_credentials,
scope=`https://api.sikoia.com/.default`). Send `Authorization: Bearer <token>` on every request. Tokens
expire after 1 hour. All requests and responses are JSON over HTTPS.

## Steps
1. `POST /v2/openbanking` (`POST_v2-openbanking`) — Create Open Banking connection
2. `GET /v2/openbanking/{bank_connection_id}` (`GET_v2-openbanking-bank_connection_id`) — Retrieve Open Banking connection status
3. `GET /v2/bankaccounts/{account_connection_id}/transactions` (`GET_v2-bankaccounts-account_connection_id-transactions`) — Retrieve account transactions

## Conventions & error handling
- Poll async request resources by `request_id` until their status is terminal (e.g. `Complete`/`Failed`).
- Reusing an idempotency key returns `409 Conflict`; a `429 RateLimit` means you exceeded 200 requests/minute.
- Every error carries `type`, `status`, `title`, `detail`, and a `correlation_id`; capture the
  `X-Correlation-Id` response header for support. See `errors/sikoia-problem-types.yml` and
  `conventions/sikoia-conventions.yml`.
