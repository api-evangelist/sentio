---
name: Query Sentio on-chain data with SQL
description: Run SQL against a Sentio project's indexed on-chain data and page through results.
api: openapi/sentio-openapi.yml
operations: [ExecuteSQL, ExecuteSQLAsync, QuerySQLResult, QueryLog]
---

# Query Sentio on-chain data with SQL

Use this skill to query a Sentio project's indexed data (metrics, event logs, entities, materialized views) via the Data API.

## Auth
- Create an API key at `https://app.sentio.xyz/profile/apikeys`.
- Send it on every request as the `api-key` header (or `api-key` query param).
- Base URL: `https://api.sentio.xyz`.

## Steps
1. Identify the project scope: `{owner}` (user or org) and `{slug}` (project).
2. **ExecuteSQL** — `POST /v1/analytics/{owner}/{slug}/sql/execute` with body `{"sqlQuery": {"sql": "<your query>"}}` and the `api-key` header. For long-running queries use **ExecuteSQLAsync** and then **QuerySQLResult** by `execution_id`.
3. Paginate: if the response returns a `cursor`, re-POST the same endpoint with body `{"cursor": "<value>"}` (headers unchanged) until no cursor is returned.
4. For raw event logs, use **QueryLog** instead of SQL.

## Rules
- Error envelope is grpc-gateway `google.rpc.Status` (`code`/`message`/`details`) — see `errors/sentio-error-codes.yml` for processor `ERRxxx` codes.
- Data-API calls are billed in compute units by query-engine size (see `https://docs.sentio.xyz/docs/quotas-and-limits`).
- The fastest way to author a query is the Data Studio SQL Editor "Export as cURL" button.
