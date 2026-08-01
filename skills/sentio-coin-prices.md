---
name: Look up crypto prices with Sentio
description: Resolve coins and fetch current or historical prices from the Sentio Price API.
api: openapi/sentio-openapi.yml
operations: [GetPrice, BatchGetPrices, ListCoins]
---

# Look up crypto prices with Sentio

Use this skill to fetch best-effort token/coin prices.

## Auth
- `api-key` header (create at `https://app.sentio.xyz/profile/apikeys`); base URL `https://api.sentio.xyz`.

## Steps
1. **ListCoins** — discover the coin identifiers available (symbol / address / chain).
2. **GetPrice** — fetch the price of a single coin identifier at (or near) a timestamp. If no data exists Sentio returns a `NOT_FOUND` error; check the returned timestamp and decide whether the price is fresh enough to use.
3. **BatchGetPrices** — price many coins in one call when you need a portfolio snapshot.

## Rules
- Prices are best-effort: always inspect the returned timestamp before relying on a value.
- A coin may be added by its CoinGecko id if missing (the CoinGecko id is not the same as the symbol).
- Errors follow the grpc-gateway `google.rpc.Status` envelope.
