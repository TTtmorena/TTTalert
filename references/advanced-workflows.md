# TTTalert — Advanced Workflows

This document defines the exact decision logic and workflows used by **TTTalert**.

---

## 1. Single Token Alert Check (Core Workflow)

**Trigger examples:**
- “TTTalert for CLAWD”
- “check alerts for this token”
- “any alerts on 0x...”
- “fee claim alert for Surplus”

**Steps:**
1. Resolve token name → contract address (if needed)
2. Fetch Bankr fees:  
   `GET https://api.bankr.bot/token-launches/{address}/fees?days=30`
3. Fetch live market data (price, volume, liquidity, 24h/6h changes)
4. Evaluate against current thresholds:
   - Fee Claimable
   - Volume Spike
   - Price Move
   - Momentum Shift
   - Liquidity Risk
5. Output full TTTalert Report
6. Highlight the most urgent alert first
7. Always include 1–3 suggested next actions

---

## 2. Fee Claim Alert (Highest Priority)

**Trigger examples:**
- “when can I claim fees?”
- “fee alert”
- “claimable fees reminder”

**Logic:**
- If `totals.claimableWeth` ≥ threshold (default 0.01 WETH) → **Active Alert**
- Always show both WETH and approximate USD
- Strongly recommend claiming when ready
- Optional: mention last claim time if available

---

## 3. Volume Spike / Momentum Alert

**Trigger examples:**
- “volume spike alert”
- “is there momentum?”
- “hot volume right now”

**Logic:**
- Calculate volume change (6h and 24h)
- Analyze `dailyEarnings` trend (rising / falling / spiking)
- Label strength:
  - Mild
  - Strong
  - Extreme
- Combine volume + fee momentum for higher confidence

---

## 4. Multi-Token Watchlist

**Trigger examples:**
- “add CLAWD and Surplus to watchlist”
- “watch these tokens”
- “my watchlist”
- “TTTalert status”

**Steps:**
1. Maintain list of watched tokens in conversation memory
2. When user asks for status / alerts → scan all watched tokens
3. Only show tokens that currently have **active alerts**
4. Sort by urgency (Fee Claim > Volume Spike > Price Move > Risk)
5. Allow easy add/remove:
   - “add $TICKER to watchlist”
   - “remove $TICKER from watchlist”

---

## 5. Custom Threshold Setup

**Trigger examples:**
- “set fee alert at 0.025 WETH”
- “alert me if volume spikes 80%”
- “price alert ±12%”
- “change threshold”

**Rules:**
- Confirm the new threshold clearly
- Apply only to the current conversation (or specify permanent if possible)
- Show both old and new threshold when changing

---

## 6. Risk Warning Mode

**Trigger examples:**
- “risk alert”
- “liquidity health”
- “any danger?”

**Key Metrics:**
- Liquidity / Market Cap ratio
- Sudden drop in fee generation
- Extreme volume without price support

**Output:** Clear Risk Level + short explanation + suggested action.

---

## 7. Quick Status / Digest

**Trigger examples:**
- “TTTalert status”
- “my alerts”
- “what’s happening?”
- “daily digest”

**Output:**
- Summary of all active alerts
- Number of tokens being watched
- Most urgent action

---

## 8. Integration with Other Skills

- When deeper fee history needed → recommend **TTTracker**
- When trading decision needed → recommend **TTTsignal**
- Can automatically pull data and combine insights

---

**TTTalert Decision Principle:**  
Monitor → Detect → Alert clearly → Suggest action.
