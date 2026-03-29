---
name: monetization-design
description: "Design ethical monetization systems — IAP, ads, battle passes, cosmetics. Balances revenue goals with player satisfaction and retention."
argument-hint: "[model: f2p|premium|hybrid] [focus: iap|ads|battlepass|cosmetics]"
user-invocable: true
allowed-tools: Read, Glob, Grep, Write, AskUserQuestion
---

When this skill is invoked:

1. **Parse the argument** for monetization model and focus area:
   - Models: `f2p` (free-to-play), `premium` (paid upfront), `hybrid` (paid + DLC/IAP)
   - Focus: `iap` (in-app purchases), `ads` (advertising), `battlepass` (season passes), `cosmetics` (visual items)
   - If unspecified, ask the user to clarify their model and primary monetization focus.

2. **Check for existing monetization work**:
   - Read `design/gdd/economy-model.md` if it exists
   - Read `design/gdd/game-concept.md` for core loop and player motivation context
   - Read `production/milestones/` for current development stage

3. **Run through monetization design phases** interactively, using `AskUserQuestion`
   at key decision points. The goal is **ethical monetization** that respects
   players while sustaining the business.

---

### Phase 1: Monetization Strategy Alignment

**Business Goals Discovery**:
- What are your revenue goals? (sustainable indie income, VC-scale returns, hobby project)
- What's your target ARPU (Average Revenue Per User)?
- What's your expected user acquisition cost and LTV (Lifetime Value)?
- Are you targeting whales, dolphins, or minnows? (spending tiers)

**Player Experience Constraints**:
- What monetization mechanics do YOU hate as a player? Why?
- What's your "ethical line" — what will you NOT do? (e.g., no pay-to-win, no loot boxes, no energy timers)
- How do you want players to feel after spending money? (excited, relieved, manipulated?)

**Market Positioning**:
- What comparable games exist in your genre? What are their monetization models?
- Are players in this genre accustomed to paying? (strategy/mobile vs. PC/console differences)
- What's your differentiation — why would players spend here vs. competitors?

**Synthesize** into a **Monetization Charter** — 3-5 principles that guide all
monetization decisions. Example:
> "Players should never feel forced to spend. All IAP should be 'thank you'
> purchases from engaged players, not 'pay or lose' coercion."

---

### Phase 2: Monetization Model Design

Based on the chosen model, design the specific implementation:

#### Free-to-Play (F2P)

**Currency Architecture**:
- Soft currency (earned): What's the source? What's it spent on?
- Hard currency (purchased): What's the exchange rate? What does it unlock?
- Premium currency (event/seasonal): How is it limited? What's the exclusivity?

**In-App Purchase Categories**:
| Type | Description | Price Range | Target Audience |
|------|-------------|-------------|-----------------|
| Consumables | Used once (potions, ammo, energy) | $0.99 - $9.99 | All players |
| Durables | Permanent (weapons, characters) | $4.99 - $29.99 | Engaged players |
| Cosmetics | Visual only (skins, emotes) | $2.99 - $19.99 | Expression-focused |
| Convenience | Time-savers (boosters, skips) | $1.99 - $14.99 | Time-poor players |
| Subscription | Recurring benefits (monthly) | $4.99 - $19.99/month | Dedicated players |

**Ad Integration** (if applicable):
- Rewarded video: What do players get? (currency, lives, bonuses)
- Interstitial: Where's the natural break? (between runs, after level)
- Placement rules: Never during core gameplay, always skippable after X seconds

**Battle Pass Design** (if applicable):
- Season length: (28-90 days typical)
- Free track rewards: What's available without paying?
- Premium track rewards: What's the upgrade incentive?
- Progression rate: How many hours to complete? Is it achievable?

#### Premium (Paid Upfront)

**Pricing Strategy**:
- What's the perceived value based on scope, quality, and genre norms?
- Platform pricing: Steam ($19.99 typical indie), mobile ($4.99 typical), console ($29.99 typical)
- Regional pricing: How will you adjust for different markets?

**DLC Strategy** (if applicable):
- Expansion DLC: Major content additions (new areas, story chapters)
- Cosmetic DLC: Skins, soundtracks, art books
- Season Pass: Bundle of planned DLC at discount
- Release cadence: How often? (quarterly, bi-annually)

#### Hybrid

**Base Game + IAP**:
- What's included in base price?
- What's reserved for post-launch IAP?
- How do you avoid "cut content" perception?

**Base Game + Subscription**:
- What recurring value justifies ongoing payment?
- Server costs, content updates, exclusive events?

---

### Phase 3: Economy Balance Design

**Source & Sink Analysis**:

For each currency/resource, map:
| Resource | Sources (inflow) | Sinks (outflow) | Expected Balance |
|----------|------------------|-----------------|------------------|
| Gold | Quests, daily login, achievements | Upgrades, consumables, crafting | Slight deficit |
| Gems | Purchase, event rewards, level-up | Cosmetics, convenience, gacha | Controlled scarcity |
| Energy | Time regen, purchase, gifts | Mission attempts, crafting | Hard cap |

**Progression Pacing**:
- Time-to-first-purchase: What's the expected playtime before first IAP consideration? (target: 3-7 days for F2P)
- Whale progression: How fast do top spenders progress? Should feel fast but not instant
- F2P progression: Can free players complete all content? (should be YES, just slower)

**Price Point Psychology**:
- Charm pricing: $4.99 vs. $5.00 (left-digit effect)
- Anchor pricing: Show "regular price" next to sale
- Decoy pricing: Add a third option to make target look better
- Bundle value: Show "you save X%" for bundles

---

### Phase 4: Ethical Safeguards

**Player Protection Systems**:

- **Spending Limits**:
  - Daily/weekly/monthly purchase caps?
  - Soft warnings at thresholds? ("You've spent $X this month")
  - Parental controls for minors?

- **Transparency**:
  - Drop rates disclosed? (required by law in some regions)
  - Clear value proposition? (no hidden costs)
  - Refund policy clear and fair?

- **Addiction Mitigation**:
  - No artificial urgency? ("Offer expires in 1 hour!" used manipulatively)
  - No exploiting FOMO excessively?
  - Energy systems: reasonable caps and regen rates?

- **Whale Protection**:
  - Monitor for problem spending patterns?
  - Self-exclusion options?
  - Customer service trained to identify at-risk players?

**Regulatory Compliance**:
- Loot box laws: Belgium, Netherlands, China have restrictions
- Age ratings: Monetization affects PEGI/ESRB ratings
- GDPR/CCPA: Data collection for personalization must comply

---

### Phase 5: Implementation Roadmap

**MVP Monetization**:
- What's the absolute minimum to launch and test?
- Which IAP items are essential vs. nice-to-have?
- What can be added post-launch based on data?

**Live Ops Calendar**:
- Weekly events: What repeats? (weekend bonuses, flash sales)
- Monthly events: What's the cadence? (seasonal themes, new content)
- Quarterly events: Major updates? (anniversaries, collaborations)

**A/B Testing Plan**:
- What will you test first? (price points, bundle composition, sale timing)
- What metrics define success? (conversion rate, ARPU, retention)
- Sample size requirements? (statistical significance)

**Analytics Requirements**:
- Purchase funnel: impression → click → cart → purchase
- Cohort analysis: D1, D7, D30 purchasers vs. non-purchasers
- LTV modeling: Predict lifetime value from early behavior

---

### Phase 6: Documentation

Generate the monetization design document following this structure:

```markdown
# Monetization Design Document

## Executive Summary
[One paragraph on the monetization strategy and ethical stance]

## Business Goals
- Revenue targets
- User acquisition strategy
- Target audience spending profile

## Monetization Model
[Detailed description of the chosen model: F2P, premium, or hybrid]

## Currency Architecture
[Soft/hard/premium currencies, exchange rates, sources and sinks]

## In-App Purchases
| ID | Name | Type | Price | Description | Target Audience |
|----|------|------|-------|-------------|-----------------|

## Battle Pass (if applicable)
[Season structure, free/premium tracks, progression rate]

## Advertising (if applicable)
[Ad types, placements, frequency caps, rewarded video rewards]

## Economy Balance
[Source/sink tables, progression pacing, price psychology]

## Ethical Safeguards
[Player protections, transparency measures, addiction mitigation]

## Regulatory Compliance
[Regional requirements, age ratings, data privacy]

## Implementation Roadmap
[MVP scope, live ops calendar, A/B testing plan]

## Analytics Requirements
[Key metrics, tracking events, reporting cadence]

## Risks and Mitigations
| Risk | Probability | Impact | Mitigation |
|------|------------|--------|------------|
```

---

4. **Save the document** to `design/gdd/monetization-design.md`.

5. **Create an economy model spreadsheet** (as markdown table or CSV) at
   `design/gdd/economy-balance.csv` with:
   - All currency sources and sinks
   - Expected daily earn rates
   - Price points for all IAP
   - Progression milestones

6. **Suggest next steps**:
   - "Review with `economy-designer` agent for balance validation"
   - "Run `/balance-check` on economy parameters once implemented"
   - "Create analytics events with `/analytics-setup` to track monetization KPIs"
   - "Implement MVP and A/B test with `/prototype monetization-flow`"

7. **Output a summary** with:
   - Chosen monetization model
   - Key IAP items and price ranges
   - Ethical safeguards implemented
   - Biggest risk (e.g., "conversion rate too low", "whale concentration")
   - File paths
