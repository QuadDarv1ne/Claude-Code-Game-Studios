# Example: Monetization Design Workflow

This example demonstrates how to use `/monetization-design` to create a complete
monetization plan for a free-to-play mobile game.

## Context

**Game:** "Dungeon Delver" — a roguelike deck-builder for mobile  
**Monetization Model:** F2P with IAP  
**Goal:** Design ethical monetization that respects players

---

## Session Transcript

### Step 1: Invoke the Skill

```
/monetization-design f2p iap
```

### Step 2: Strategy Alignment

The skill asks clarifying questions:

> **Q:** What are your revenue goals?
>
> **A:** Sustainable indie income (~$5k/month). Not trying to be a whale hunter.

> **Q:** What's your "ethical line"?
>
> **A:** No pay-to-win in ranked modes. No loot boxes. No energy timers blocking play.

> **Q:** Target player spending profile?
>
> **A:** Mostly minnows and dolphins. Maybe 2-3% conversion, $10-20 ARPPU.

### Step 3: Currency Architecture

The skill proposes a dual-currency system:

| Currency | Type | Source | Sink |
|----------|------|--------|------|
| Gold | Soft | Runs, daily quests | Card packs, upgrades |
| Gems | Hard | Achievements, IAP | Cosmetics, run modifiers |

**Decision point via AskUserQuestion:**

```
Currency Exchange Rate:
  ○ $1 = 50 Gems (premium, scarcity)
  ● $1 = 100 Gems (standard, recommended)
  ○ $1 = 200 Gems (generous, volume)
  ○ Custom rate
```

### Step 4: IAP Catalog Design

The skill generates an IAP table:

| ID | Name | Type | Price | Target |
|----|------|------|-------|--------|
| IAP001 | Starter Pack | Bundle | $4.99 | New players |
| IAP002 | Gem Pouch | Currency | $9.99 | All players |
| IAP003 | Cosmetic Skin | Cosmetic | $2.99 | Collectors |
| IAP004 | Battle Pass | Season | $9.99 | Engaged players |

### Step 5: Ethical Safeguards

The skill documents player protections:

- [x] Spending limits: $100/week hard cap
- [x] Drop rates disclosed: 100% transparent
- [x] No artificial urgency: all sales are cosmetic-only timers
- [x] F2P viability: all content accessible without paying

### Step 6: Output Files

The skill creates:

1. `design/gdd/monetization-design.md` — full design document
2. `design/gdd/economy-balance.csv` — currency faucet/sink table

---

## Output: monetization-design.md (excerpt)

```markdown
# Monetization Design Document

## Executive Summary
Dungeon Delver uses a dual-currency F2P model with cosmetic IAP and a battle pass.
All gameplay content is accessible without paying; monetization focuses on
convenience and self-expression.

## Currency Architecture
- Gold (soft): Earned from runs, spent on card packs
- Gems (hard): Purchased or earned slowly, spent on cosmetics

## IAP Catalog
[Full table with 12 items]

## Ethical Safeguards
- No pay-to-win in ranked mode
- Drop rates publicly disclosed
- Spending limits enforced
```

---

## Output: economy-balance.csv (excerpt)

```csv
currency,source,sink,rate_per_day,target_balance
gold,run_completion,card_pack,500,surplus_10pct
gold,daily_quest,upgrade,200,stable
gems,achievement,battle_pass,10,scarcity
gems,iap_purchase,cosmetic,variable,revenue_target
```

---

## Next Steps

After running `/monetization-design`:

1. **Review with `economy-designer`** — validate sink/faucet balance
2. **Run `/analytics-setup`** — configure IAP funnel tracking
3. **Implement MVP** — currency system + 3 IAP items
4. **A/B test pricing** — use `/analytics-setup` to define experiment

---

## Key Learnings

- **Ethical monetization** can still be profitable (2-3% conversion is sustainable)
- **Dual-currency systems** separate progression from premium purchases
- **Player protections** build trust and improve long-term retention
- **Transparency** (drop rates, no dark patterns) differentiates from competitors

---

*This example demonstrates the collaborative workflow: the skill asks questions,
presents options, and generates drafts — but the user makes all decisions.*
