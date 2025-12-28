# Fast Polygon RPC — Simple & Predictable Polygon RPC for Bots and dApps

FastPolygon is a **Polygon RPC provider** built on our own **Polygon node** (Erigon).  
You get a single **Polygon RPC endpoint** with an API key, predictable limits, and crypto-friendly payments.

## What is FastPolygon?

- A **Polygon JSON RPC** gateway (Kong) in front of our own **Erigon Polygon node**
- **Ethereum compatible RPC** (standard JSON-RPC 2.0 methods)
- **Non-archive** node (optimized for real-time reads for bots and dApps)
- A simple billing UI to create keys and manage plans

## Why not public Polygon RPC?

Public endpoints are great for quick experiments, but for bots and production workloads they often mean:

- Throttling without notice
- Unstable rate limits
- Shared infrastructure with noisy neighbors
- No predictable quotas or guarantees

## Why not Alchemy / Infura / QuickNode?

These providers are excellent, but can be overkill for many bots:

- Compute units / pricing complexity and “surprise bills”
- Account overhead (dashboards, projects, keys, policies)
- Credit cards / KYC requirements for some regions/flows
- Slower setup when you just want a clean **web3 RPC** URL for a bot

## Who is this for?

- Developers who need a predictable **polygon rpc** for bots and dApps
- Teams that want a simple **polygon rpc provider** with clear RPS and monthly quotas
- Builders who just want a stable **polygon rpc endpoint** and to start shipping

## Who is this NOT for?

- Users who need an **archive node** (historical state at old blocks)
- Analytics platforms or indexed data APIs
- Trace/debug-heavy workflows (e.g. `debug_*`, full tracing)
- Multi-region enterprise SLA setups

## Features

- Simple API-key based access
- Predictable rate limits and monthly quotas per plan
- Crypto payments (invoice flow)
- Two URL formats: path key and query key
- Monitoring and basic security baseline on the backend

## Pricing

Current MVP plans:

- **Free**: 100k req / month, 3 RPS, 1 key
- **Starter ($10)**: 1M req / month, 10 RPS, 1 key
- **Pro ($25)**: 5M req / month, 25 RPS, 2 keys
- **Heavy ($50)**: 20M req / month, 50 RPS, 3 keys

## Quick Start

### 1) Get an API key

Open the app, log in, and create a key:

- App: `https://app.fastpolygon.tech`

### 2) Call the Polygon JSON-RPC endpoint

Main format:

```bash
API_KEY="YOUR_API_KEY"

curl -sS -X POST "https://rpc.fastpolygon.tech/v1/${API_KEY}" \
  -H "Content-Type: application/json" \
  --data '{"jsonrpc":"2.0","id":1,"method":"eth_chainId","params":[]}'
```

Fallback (query key):

```bash
API_KEY="YOUR_API_KEY"

curl -sS -X POST "https://rpc.fastpolygon.tech/v1?api_key=${API_KEY}" \
  -H "Content-Type: application/json" \
  --data '{"jsonrpc":"2.0","id":1,"method":"eth_chainId","params":[]}'
```

## Example Bot

See the companion template repo: `polygon-bot-template`.

## Rate Limits & Quotas

- Rate limiting is enforced per API key (plan-based).
- Monthly usage is tracked and keys can be blocked when quota is exceeded.

Typical responses:
- **200** OK
- **429** Too Many Requests (RPS exceeded)
- **401** Unauthorized (invalid / deleted key)
- **403** Forbidden (quota exhausted / key blocked)

## Payments (Crypto)

Plans can be upgraded via crypto invoices (NOWPayments flow).  
Invoice creation is available from the dashboard in the app.

## Limitations

- **Non-archive**: some historical state queries (old block tags) may fail.
- **No analytics**: this is a raw RPC endpoint, not an indexed API.
- **Syncing**: right after node start, `eth_blockNumber` can be low/`0x0` while `eth_syncing` indicates progress.

## FAQ

**Is this standard Ethereum JSON-RPC?**  
Yes. This is an Ethereum compatible RPC endpoint for Polygon.

**Do you implement methods yourself?**  
No. We proxy JSON-RPC requests to the upstream Erigon node. If Erigon supports a method, it works here.

**Does it support `eth_getBalance`, `eth_call`, `eth_getLogs`?**  
Yes — as long as the upstream node supports the query and it’s not an archive-only requirement.
