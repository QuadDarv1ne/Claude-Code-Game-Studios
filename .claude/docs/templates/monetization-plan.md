# Monetization Plan

## Executive Summary

**Game:** [Game Name]  
**Version:** [Version]  
**Date:** [Date]  
**Author:** [Author]

---

## Monetization Model

### Primary Model

- [ ] Free-to-Play (F2P)
- [ ] Premium (Paid Upfront)
- [ ] Hybrid (Paid + DLC/IAP)
- [ ] Subscription

### Revenue Goals

| Metric | Target | Notes |
|--------|--------|-------|
| Monthly Revenue | $ | |
| ARPU (Average Revenue Per User) | $ | |
| ARPPU (Average Revenue Per Paying User) | $ | |
| Conversion Rate (Payers / MAU) | % | |
| LTV (Lifetime Value) | $ | |

---

## Currency Architecture

### Currencies

| Currency | Type | Source | Sink | Exchange Rate |
|----------|------|--------|------|---------------|
| [e.g., Gold] | Soft | Quests, daily login | Upgrades, consumables | N/A |
| [e.g., Gems] | Hard | Purchase, events | Cosmetics, convenience | $1 = 100 |
| [e.g., Event Tokens] | Premium | Limited events | Exclusive items | N/A |

### Faucet & Sink Balance

| Resource | Daily Inflow (Avg) | Daily Outflow (Avg) | Balance Target |
|----------|-------------------|---------------------|----------------|
| Gold | 500 | 450 | Slight surplus |
| Gems | 10 (F2P) / 500 (paid) | Variable | Controlled scarcity |

---

## In-App Purchases

### IAP Catalog

| ID | Name | Type | Price (USD) | Description | Target Audience |
|----|------|------|-------------|-------------|-----------------|
| IAP001 | Starter Pack | Bundle | $4.99 | 500 Gems + Exclusive Weapon | New players |
| IAP002 | Gem Pouch | Currency | $9.99 | 1000 Gems | All players |
| IAP003 | Battle Pass | Season | $9.99 | 30-day premium rewards | Engaged players |
| IAP004 | Skin Bundle | Cosmetic | $14.99 | 5 exclusive skins | Collectors |
| IAP005 | Time Saver | Convenience | $2.99 | 2x speed for 1 hour | Time-poor players |

### Pricing Strategy

- **Charm Pricing:** $X.99 instead of $X+1.00
- **Anchor Pricing:** Show "regular price" next to sale
- **Bundle Value:** "Save X%" for bundles
- **Regional Pricing:** Adjust for [regions]

---

## Battle Pass (if applicable)

### Season Structure

| Parameter | Value |
|-----------|-------|
| Season Length | days |
| Free Track Rewards | items |
| Premium Track Rewards | items |
| Progression Rate | levels/day |
| Completion Time | days |

### Reward Tiers

| Level | Free Reward | Premium Reward |
|-------|-------------|----------------|
| 1-10 | | |
| 11-20 | | |
| 21-30 | | |
| 31-40 | | |
| 41-50 | | |

---

## Advertising (if applicable)

### Ad Types

| Type | Placement | Frequency | Reward |
|------|-----------|-----------|--------|
| Rewarded Video | After level fail | Unlimited | +100 Gold |
| Interstitial | Between sessions | 1 per 30 min | N/A |
| Banner | Main menu (optional) | Always-on | N/A |

### Ad Economy

| Metric | Target |
|--------|--------|
| Ad View Rate | % of DAU |
| eCPM | $ |
| Ad Revenue / DAU | $ |

---

## Economy Balance

### Progression Pacing

| Player Type | Time to First Purchase | Progression Speed |
|-------------|----------------------|-------------------|
| F2P Casual | N/A | Baseline (1.0x) |
| F2P Engaged | 3-7 days | 1.2x with grinding |
| Minnow ($5/mo) | Weekly | 1.5x |
| Dolphin ($20/mo) | Bi-weekly | 2.0x |
| Whale ($100+/mo) | Weekly | 3.0x (capped) |

### Source & Sink Analysis

```
[Insert diagram or table showing all currency sources and sinks]
```

---

## Ethical Safeguards

### Player Protections

- [ ] Spending limits (daily/weekly/monthly)
- [ ] Soft warnings at thresholds
- [ ] Parental controls for minors
- [ ] Drop rates disclosed
- [ ] Clear refund policy
- [ ] No artificial urgency ("Offer expires in 1 hour!")
- [ ] Self-exclusion options

### Regulatory Compliance

| Region | Requirement | Status |
|--------|-------------|--------|
| EU | GDPR, loot box disclosure | |
| US | COPPA (under 13), state laws | |
| China | Play time limits, spending caps | |
| Belgium | Loot box restrictions | |

---

## Implementation Roadmap

### MVP Scope

| Feature | Priority | Sprint |
|---------|----------|--------|
| Currency system | P0 | 1 |
| Basic IAP store | P0 | 2 |
| Purchase flow | P0 | 2 |
| Receipt validation | P0 | 2 |
| Battle Pass | P1 | 3 |
| Daily deals | P2 | 4 |

### Live Ops Calendar

| Event | Type | Frequency | Duration |
|-------|------|-----------|----------|
| Weekend Bonus | Recurring | Weekly | 48 hours |
| Seasonal Event | Themed | Quarterly | 2 weeks |
| Flash Sale | Surprise | Monthly | 24 hours |
| Anniversary | Special | Yearly | 1 week |

---

## Analytics Requirements

### Key Metrics

| Metric | Event | Formula |
|--------|-------|---------|
| IAP Impressions | `iap_offer_viewed` | Count |
| Store Opens | `iap_store_opened` | Count |
| Cart Adds | `iap_item_carted` | Count |
| Purchases | `iap_purchase_complete` | Count |
| Conversion Rate | Derived | Purchases / Store Opens |
| ARPPU | Derived | Revenue / Purchasers |

### Funnel Tracking

```
IAP Offer → Store Open → Item View → Cart → Purchase → Complete
    ↓           ↓            ↓         ↓        ↓          ↓
  track     track        track     track    track      track
```

### A/B Testing Plan

| Test | Variant A | Variant B | Success Metric |
|------|-----------|-----------|----------------|
| Price Point | $4.99 | $6.99 | Conversion rate |
| Bundle Composition | 500 Gems + Item | 700 Gems | Revenue per user |
| Sale Timing | Weekend | Weekday | Conversion rate |

---

## Risks & Mitigations

| Risk | Probability | Impact | Mitigation |
|------|------------|--------|------------|
| Low conversion rate | Medium | High | A/B test pricing, improve value proposition |
| Whale concentration >70% | Medium | High | Broaden mid-tier offers, improve retention |
| Negative reviews (P2W) | Low | High | Ensure F2P viability, communicate value |
| Regulatory changes | Low | High | Monitor legislation, prepare compliance updates |

---

## Success Criteria

| Milestone | Metric | Target Date |
|-----------|--------|-------------|
| Soft Launch | Conversion >1.5% | |
| Global Launch | D1 Retention >40% | |
| Month 1 | Revenue $/month | |
| Month 3 | LTV > CPI x 3 | |

---

*Template for monetization design. Fill in all sections before implementation.*
