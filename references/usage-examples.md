# TTTalert — Usage Examples

This document contains real trigger examples and expected behavior for **TTTalert**.

---

## 1. Basic Single Token Alert

**User says:**
```
TTTalert for CLAWD
```
```
check alerts for this token
```
```
any alerts on Surplus?
```

**Expected behavior:**
- Fetch latest fees + market data
- Evaluate all default thresholds
- Output full TTTalert Report
- Highlight active alerts (if any)
- End with 1–3 suggested actions

---

## 2. Fee Claim Focus

**User says:**
```
when can I claim fees on CLAWD?
```
```
fee claim alert
```
```
is there claimable fees?
```

**Expected behavior:**
- Prioritize `claimableWeth`
- Show WETH + approximate USD
- Clearly say whether it meets threshold or not
- Strongly recommend claiming if ready

---

## 3. Volume & Momentum

**User says:**
```
volume spike on Bankr
```
```
is there momentum right now?
```
```
hot volume alerts
```

**Expected behavior:**
- Scan recent activity / watched tokens
- Detect significant volume changes
- Combine with fee generation trend
- Label strength (Mild / Strong / Extreme)

---

## 4. Watchlist Management

**User says:**
```
add CLAWD and Surplus to watchlist
```
```
watch this token
```
```
remove CLAWD from watchlist
```
```
my watchlist
```
```
TTTalert status
```

**Expected behavior:**
- Maintain watchlist in conversation memory
- Confirm add/remove actions
- On status request → show only tokens with active alerts
- Sort by urgency

---

## 5. Custom Threshold

**User says:**
```
set fee alert at 0.025 WETH
```
```
alert me if volume spikes 70%
```
```
price alert ±10%
```
```
change fee threshold to 0.015
```

**Expected behavior:**
- Confirm the new threshold
- Apply it for future checks in this conversation
- Show clear confirmation message

---

## 6. Risk Check

**User says:**
```
risk alert for this token
```
```
liquidity health check
```
```
any danger?
```

**Expected behavior:**
- Evaluate Liquidity / Market Cap ratio
- Check fee sustainability
- Output clear Risk Level + explanation

---

## 7. Combined / Natural Language

**User says:**
```
notify me when CLAWD fees are ready to claim
```
```
keep an eye on Surplus volume
```
```
alert me if anything important happens on these tokens
```

**Expected behavior:**
- Interpret intent correctly
- Set appropriate alerts / add to watchlist
- Confirm what is being monitored

---

## Quick Reference Triggers

| User Intent              | Example Phrases                          |
|--------------------------|------------------------------------------|
| Single check             | TTTalert for CLAWD, check alerts         |
| Fee claim                | when can I claim, fee alert              |
| Volume spike             | volume spike, hot volume                 |
| Watchlist                | add to watchlist, my alerts, status      |
| Custom threshold         | set fee alert at ..., alert me if ...    |
| Risk                     | risk alert, liquidity health             |

---

**TTTalert** should feel responsive, clear, and proactive.
```

---
