---
name: Simulate and trace a transaction with Sentio
description: Create a fork, simulate a transaction on it, and inspect the resulting call trace.
api: openapi/sentio-openapi.yml
operations: [CreateFork, SimulateTransaction, GetCallTraceByTransaction, SearchTransactions]
---

# Simulate and trace a transaction with Sentio

Use this skill to dry-run a transaction and analyze its execution with Sentio's debugger/simulation surface.

## Auth
- `api-key` header (create at `https://app.sentio.xyz/profile/apikeys`); base URL `https://api.sentio.xyz`.

## Steps
1. (Optional) **CreateFork** — create a fork of a chain at a block so simulations run against a controlled state.
2. **SimulateTransaction** — submit the transaction body; the response includes a unique simulation id. Save it to fetch details later.
3. **GetCallTraceByTransaction** — retrieve the Sentio call trace for a transaction (`txId.txHash` + `chainSpec.chainId`); each entry carries a `startIndex` marking execution order for fund-flow charts.
4. **SearchTransactions** — find transactions matching filters when you do not yet have a hash.

## Rules
- Simulations are saved and addressable by id; reuse the id rather than re-running.
- For bundle simulations only the first entry's block/state-override fields take effect.
- Errors follow the grpc-gateway `google.rpc.Status` envelope; see `errors/sentio-error-codes.yml`.
