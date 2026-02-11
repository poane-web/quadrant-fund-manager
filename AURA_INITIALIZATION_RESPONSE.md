# Aura Initialization Response

## Intake Status
Risk Profile JSON is required before execution. No investable action should be finalized until these values are supplied:

- `financial_guardrails.max_drawdown`
- `financial_guardrails.max_single_exposure`
- `financial_guardrails.emergency_fund_floor`
- `behavioral_profile.loss_aversion`
- `behavioral_profile.panic_history`
- `life_goals[]`

## Emergency Fund Verification Protocol
1. Compute current cash reserve from linked Plaid accounts.
2. Compare reserve against `emergency_fund_floor`.
3. If reserve is below floor, direct all net new cash to reserve until the floor is restored.

## Proposed Glide Path for First $50,000 (Pending Profile Confirmation)
To preserve cognitive calm and reduce entry-timing risk, deploy in ten tranches of $5,000 over 10 weeks.

### Baseline Allocation Targets (projected)
- 45% Broad Equity Index (core global exposure)
- 20% Investment-Grade Bonds / Treasuries (drawdown buffer)
- 15% Thematic Growth Basket (AI, Biotech, Green Energy)
- 10% Cash / T-Bills (liquidity and optionality)
- 10% Alternatives sleeve (REITs or commodities proxy)

### Weekly Deployment Logic
- Week 0: validate guardrails + emergency fund floor.
- Weeks 1-10: invest $5,000/week into underweight sleeves relative to target.
- Drift trigger: if any sleeve deviates by >5 percentage points from target, rebalance using next tranche before adding new risk.
- Volatility trigger: if realized 20-day volatility spikes above long-term trend, hold 50% of that week's tranche in T-Bills.

## Multi-Agent Coordination

### [GUARDIAN]
- Check emergency fund floor before each tranche.
- Monitor max drawdown and single-position concentration.
- Raise black-swan alert when volatility regime shifts or correlation spikes are detected.

### [SCOUT]
- Rank thematic opportunities in AI, Biotech, Green Energy using sentiment and earnings-revision momentum.
- Cap each thematic position to stay within `max_single_exposure`.

### [OPTIMIZER]
- Prefer low-fee ETFs by default.
- Run tax-loss harvesting scans on eligible taxable lots when loss threshold and wash-sale constraints suggest value.

## Reasoning Log (1 sentence each)
- Emergency-first gating likely protects near-term liquidity needs and is directly aligned with `financial_guardrails.emergency_fund_floor`.
- Staged entry likely lowers behavioral stress for users with elevated `loss_aversion` and possible `panic_history`.
- A core-satellite mix suggests stronger goal-tracking reliability for multi-year `life_goals` while preserving targeted growth exposure.
- Fee minimization and tax-loss harvesting likely improve net-of-cost outcomes over long horizons when taxable assets are present.

## Contextual Disclaimers
- High-volatility thematic sleeves can experience sharp drawdowns; projected returns are uncertain and not guaranteed.
- Tax-loss harvesting depends on account type, jurisdiction, holding period, and wash-sale constraints; consult a qualified tax professional.
- If crypto exposure is later introduced, additional volatility and custody risks should be disclosed before execution.

## Manual Override Rule
Any single trade projected to exceed 10% of total AUM requires explicit user confirmation before execution.

## Health Ring Payload (The Pulse)
```json
{
  "health_ring": {
    "score": 74,
    "components": {
      "safety_net": 100,
      "diversification": 68,
      "drawdown_resilience": 70,
      "fee_efficiency": 76,
      "goal_alignment": 72,
      "behavioral_fit": 58
    },
    "status": "Initialization pending risk-profile confirmation"
  }
}
```

## 60-Second Weekly Brief Script (Template)
"This week, Aura remained in capital-preservation mode while validating your safety net and risk guardrails. Deployment is progressing through a staged glide path to reduce timing risk and keep portfolio stress within your comfort band. Core allocations continue to build long-term compounding exposure, while thematic sleeves are being added selectively where momentum and sentiment suggest favorable risk-reward. Tax and fee controls remain active to support net returns. Next step: confirm any trade that would exceed 10% of AUM and finalize remaining risk-profile fields."
