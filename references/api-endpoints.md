# TTTalert — Advanced API Reference

This document contains the official and recommended data sources used by **TTTalert**.

---

## 1. Primary Endpoint — Token Fees (Most Important)

**GET** `https://api.bankr.bot/token-launches/{tokenAddress}/fees?days=30`

Legacy (still working but deprecated):  
`https://api.bankr.bot/public/doppler/token-fees/{tokenAddress}?days=30`

### Critical Fields for Alerts

| Field                    | Description                          | Usage in TTTalert                  |
|--------------------------|--------------------------------------|------------------------------------|
| `totals.claimableWeth`   | Currently claimable fees             | **Fee Claim Alert** (core)         |
| `lifetimeEarnedWeth`     | Total lifetime fees earned           | Fee strength context               |
| `dailyEarnings[]`        | Array of `{ date, weth }`            | Momentum & trend detection         |
| `lifetimeBestDay`        | Best single day earnings             | Peak reference                     |
| `tokens[0].share`        | Creator fee share (usually ~57%)     | Fee quality check                  |

### Example Response
```json
{
  "address": "0x...",
  "chain": "base",
  "days": 30,
  "lifetimeEarnedWeth": "1.2345",
  "lifetimeDays": 42,
  "lifetimeBestDay": {
    "date": "2026-03-22",
    "weth": "0.0891"
  },
  "dailyEarnings": [
    { "date": "2026-08-10", "weth": "0.0123" },
    { "date": "2026-08-11", "weth": "0.0087" },
    { "date": "2026-08-12", "weth": "0.0156" }
  ],
  "totals": {
    "claimableWeth": "0.0456",
    "claimedWeth": "1.1889",
    "claimCount": 5
  },
  "tokens": [
    {
      "tokenAddress": "0x...",
      "name": "Example",
      "symbol": "EXM",
      "share": "57.00%",
      "claimable": {
        "token0": "0.0456",
        "token1": "12345.67"
      }
    }
  ]
}
```

**Rules:**
- Always request `days=30` by default (allowed range: 1–90)
- Use `dailyEarnings` to detect fee momentum (rising / falling / spiking)
- Convert all WETH values to approximate USD using current ETH price

---

## 2. Quick Claimable Check (Lightweight)

**GET** `https://api.bankr.bot/public/doppler/claimable-fees/{tokenAddress}?beneficiary={walletAddress}`

Useful for fast “can claim?” checks without full history.

---

## 3. Recent Launches (for scanning new tokens)

**GET** `https://api.bankr.bot/token-launches`

Returns the 50 most recent Bankr token launches.  
Use this when user asks for broad monitoring or new token alerts.

---

## 4. Agent Profiles

**GET** `https://api.bankr.bot/agent-profiles?sort=marketCap&limit=20`  
**GET** `https://api.bankr.bot/agent-profiles/{slug-or-address}`

Useful fields:
- `marketCapUsd`
- `weeklyRevenueWeth`
- Agent metadata

---

## 5. Market Data Sources (Price • Volume • Liquidity)

Priority order (use the first available):

1. **GeckoTerminal** / **DexScreener** (preferred)
2. **Birdeye**
3. **Zerion** or **Alchemy**
4. CoinGecko (fallback)

### Required Metrics for Alerts
- Current Price (USD)
- 24h / 6h / 1h Price Change (%)
- 24h / 6h Volume (USD)
- Volume change percentage
- Liquidity (USD)
- Liquidity / Market Cap ratio → critical for Risk Alert

---

## 6. Best Practices for TTTalert

- Cache all responses for 1–2 minutes within the same conversation
- Never invent or estimate missing numbers
- Always show both WETH and approximate USD
- Default thresholds:
  - Fee Claimable ≥ 0.01 WETH
  - Volume Spike ≥ +40% (6h) or +60% (24h)
  - Price Move ≥ ±8% (1h) or ±15% (24h)
- If data is incomplete → lower confidence and clearly state “Limited data”
- Prefer the newest Bankr endpoints over legacy ones

---

**TTTalert** uses these endpoints to deliver accurate and timely alerts for the Bankr ecosystem.
```

---
