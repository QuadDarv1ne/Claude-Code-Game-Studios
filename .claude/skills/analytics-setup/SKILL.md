---
name: analytics-setup
description: "Design and configure game analytics — event tracking, funnels, cohorts, dashboards. Data infrastructure for informed design decisions."
argument-hint: "[focus: events|funnels|dashboards|full]"
user-invocable: true
allowed-tools: Read, Glob, Grep, Write, AskUserQuestion
---

When this skill is invoked:

1. **Parse the argument** for analytics focus area:
   - `events`: Event tracking schema and implementation
   - `funnels`: Conversion funnel definition and analysis
   - `dashboards`: KPI dashboard specification
   - `full`: Comprehensive analytics setup (default)

2. **Check for existing analytics work**:
   - Read `design/gdd/game-concept.md` for core loop and key mechanics
   - Read `design/gdd/monetization-design.md` for monetization KPIs
   - Read `design/gdd/tutorial-design.md` for onboarding funnel
   - Check `src/` for existing analytics implementations
   - Check for analytics SDK integration (Unity Analytics, GameAnalytics, Firebase, custom)

3. **Run through analytics design phases** interactively, using `AskUserQuestion`
   at key decision points. The goal is **actionable data** — every event tracked
   should answer a question or enable a decision.

---

### Phase 1: Analytics Strategy

**Business Intelligence Goals**:

- What are the **top 3 questions** you need data to answer?
  - Examples: "Where do players quit?", "What drives purchases?", "Is the tutorial working?"
- What decisions will you make **differently** with this data?
- What's your analytics maturity level? (none, basic events, funnels, predictive)

**Technical Constraints**:

- Target platforms? (PC, mobile, console — affects SDK choices)
- Online required or offline-first with batching?
- Data budget per user per session? (mobile: <100KB typical)
- Backend: Self-hosted, cloud service, or third-party SDK?

**Privacy & Compliance**:

- GDPR compliance required? (EU users)
- COPPA compliance required? (under 13, US)
- Data retention policy? (how long to keep raw events)
- Anonymization level? (hashed IDs, no PII, aggregated only)

**Analytics Stack Selection**:

| Solution | Best For | Cost | Complexity |
|----------|----------|------|------------|
| **GameAnalytics** | Mobile F2P, indie | Free tier | Low |
| **Unity Analytics** | Unity games | Free tier | Low |
| **Firebase** | Mobile, cross-platform | Free tier | Medium |
| **PlayFab** | Live service, multiplayer | Free tier | Medium |
| **Custom + BigQuery** | Full control, scale | Pay per query | High |
| **Mixpanel/Amplitude** | Product analytics | $$$ | Medium |

---

### Phase 2: Event Schema Design

**Event Categories** (use consistent naming):

```
session_*.started, session_*.ended, session_*.paused, session_*.resumed
progression.level_start, progression.level_complete, progression.level_fail, progression.quit
economy.currency_earn, economy.currency_spend, economy.item_acquire, economy.item_consume
combat.enemy_kill, combat.player_death, combat.damage_dealt, combat.ability_use
social.friend_add, social.message_send, social.gift_send, social.gift_receive
monetization.iap_offer, iap_view, iap_purchase, iap_refund, ad_view, ad_complete
tutorial.step_view, tutorial.step_complete, tutorial.step_skip, tutorial.fail
ui.screen_open, ui.screen_close, ui.button_click, ui.menu_navigate
error.crash, error.exception, error.warning, error.validation_fail
```

**Event Structure Template**:

```json
{
  "event_id": "uuid-v4",
  "event_type": "progression.level_complete",
  "timestamp": "2026-03-29T14:32:00Z",
  "session_id": "session-uuid",
  "user_id": "hashed-user-id",
  
  "device": {
    "platform": "Windows",
    "os_version": "11",
    "device_model": "Custom PC",
    "memory_gb": 16,
    "screen_resolution": "1920x1080"
  },
  
  "game_context": {
    "game_version": "0.3.0",
    "build_number": 1234,
    "scene_name": "Level_03_Forest",
    "game_mode": "campaign",
    "difficulty": "normal"
  },
  
  "player_state": {
    "player_level": 12,
    "playtime_minutes": 145,
    "session_number": 7,
    "days_since_install": 4,
    "last_ad watched": "2026-03-29T14:15:00Z",
    "last_iap_date": "2026-03-27T10:00:00Z",
    "total_iap_value_usd": 4.99,
    "guild_id": "guild-123",
    "current_streak_days": 3
  },
  
  "event_data": {
    "level_id": "level_03",
    "level_name": "Dark Forest",
    "completion_time_seconds": 342,
    "deaths": 2,
    "secrets_found": 2,
    "secrets_total": 5,
    "enemies_killed": 23,
    "items_collected": 15,
    "health_remaining_pct": 65,
    "stars_earned": 3
  }
}
```

**Event Design Principles**:

- **Immutable facts**: Events are append-only, never update past events
- **Granular data**: Record atomic events, aggregate later
- **Context richness**: Include enough state to reconstruct the situation
- **Consistent naming**: snake_case for event types, camelCase for properties
- **Enumerated values**: Use string enums, not magic numbers

---

### Phase 3: Core Funnel Definition

Define **conversion funnels** for key player journeys:

**Onboarding Funnel** (D1 retention driver):

```
1. App install/open
   ↓ (measure: install→tutorial start rate, target >90%)
2. Tutorial step 1 complete
   ↓ (measure: step 1→2 completion, target >85%)
3. Tutorial step N complete
   ↓ (measure: full tutorial completion, target >80%)
4. Core loop first pass
   ↓ (measure: tutorial→game start, target >75%)
5. First session natural close
   ↓ (measure: D1 return rate, target >40% mobile, >50% PC)
```

**Monetization Funnel** (revenue driver):

```
1. Player sees IAP offer (impression)
   ↓ (measure: impression→view click, target >10%)
2. Player opens IAP store
   ↓ (measure: store view→cart add, target >5%)
3. Player adds to cart / considers purchase
   ↓ (measure: cart→purchase complete, target >30%)
4. Purchase completed
   ↓ (measure: overall conversion, target >2% MAU)
```

**Engagement Funnel** (retention driver):

```
1. Session started
   ↓ (measure: session→core loop entry, target >95%)
2. Core loop entered
   ↓ (measure: core loop→meaningful progress, target >80%)
3. Meaningful progress made (level up, item earned, story beat)
   ↓ (measure: progress→session complete, target >70%)
4. Session completed naturally (not crash/quit)
   ↓ (measure: session length distribution, target 5-20 min mobile)
```

**Difficulty Funnel** (balance indicator):

```
Level N attempt started
   ↓ (measure: attempt→completion, target 60-80%)
Level N completed on first try
   ↓ (measure: first-try success rate, target 30-50%)
Level N failed N times
   ↓ (measure: fail→quit rate, target <20% after 5 fails)
Level N eventually completed
   ↓ (measure: eventual completion, target >90%)
```

---

### Phase 4: KPI Dashboard Specification

Define **dashboards** for different stakeholders:

**Executive Dashboard** (high-level health):

| Metric | Formula | Target | Frequency |
|--------|---------|--------|-----------|
| DAU | Unique users per day | Growth WoW | Daily |
| D1 Retention | D1 returning / D0 new | >40% mobile | Daily |
| D7 Retention | D7 returning / D0 new | >15% mobile | Weekly |
| D30 Retention | D30 returning / D0 new | >5% mobile | Monthly |
| ARPDAU | Revenue / DAU | $0.05-0.20 F2P | Daily |
| Conversion Rate | Purchasers / MAU | >2% | Weekly |

**Design Dashboard** (gameplay health):

| Metric | Formula | Target | Frequency |
|--------|---------|--------|-----------|
| Tutorial Completion | Finished / Started | >80% | Daily |
| Level Difficulty | Avg deaths per level | 1.5-3.0 | Per level |
| Session Length | Avg minutes per session | 5-20 min mobile | Daily |
| Sessions per DAU | Total sessions / DAU | 3-8 per day | Daily |
| Core Loop Engagement | Players completing 5+ loops | >60% | Daily |

**Monetization Dashboard** (revenue health):

| Metric | Formula | Target | Frequency |
|--------|---------|--------|-----------|
| Gross Revenue | Sum of all IAP + ads | Growth WoW | Daily |
| IAP Conversion | Purchasers / MAU | >2% | Weekly |
| ARPPU | Revenue / Purchasers | $20-50 | Weekly |
| Whale Concentration | Top 10% revenue / Total | <70% | Weekly |
| Ad Fill Rate | Ads served / Requests | >90% | Daily |
| eCPM | Ad revenue / Impressions * 1000 | $5-20 | Weekly |

**Live Ops Dashboard** (event health):

| Metric | Formula | Target | Frequency |
|--------|---------|--------|-----------|
| Event Participation | Participants / DAU | >30% | Per event |
| Event Completion | Completers / Participants | >20% | Per event |
| Event Revenue | Revenue during event | +50% vs baseline | Per event |
| Social Virality | Invites sent / Participant | >0.5 | Per event |

---

### Phase 5: Implementation Plan

**SDK Integration Checklist**:

```markdown
### Initial Setup
- [ ] Choose analytics provider(s)
- [ ] Create project and obtain API keys
- [ ] Add SDK to project (Package Manager / manual)
- [ ] Configure build variants (dev, staging, prod)
- [ ] Set up data pipelines to warehouse (if custom)

### Event Implementation
- [ ] Create event logging service/wrapper
- [ ] Implement session lifecycle events
- [ ] Implement progression events
- [ ] Implement economy events
- [ ] Implement monetization events
- [ ] Implement error/crash reporting

### Testing & Validation
- [ ] Test event firing in dev environment
- [ ] Validate event schema in analytics dashboard
- [ ] Verify data appears in real-time stream
- [ ] Test offline batching and replay
- [ ] Verify GDPR consent flow (if applicable)

### Dashboard Setup
- [ ] Create executive dashboard
- [ ] Create design dashboard
- [ ] Create monetization dashboard
- [ ] Set up automated reports (email/Slack)
- [ ] Configure alerts (crash spikes, revenue drops)
```

**Event Logging Best Practices**:

- **Batching**: Group events, send every 30-60 seconds or on session end
- **Compression**: Use gzip for large payloads
- **Retry logic**: Exponential backoff on failures
- **Graceful degradation**: If analytics fails, game continues
- **Debug mode**: Toggle to log events to console in dev builds

**A/B Testing Infrastructure**:

- Experiment assignment service (which variant is user in?)
- Event tagging (include experiment_id and variant in events)
- Statistical significance calculator
- Guardrail metrics (ensure no negative impact on retention)

---

### Phase 6: Documentation

Generate the analytics specification document:

```markdown
# Analytics Specification Document

## Executive Summary
[Analytics strategy and key goals]

## Analytics Stack
[Provider selection, integration approach]

## Event Schema

### Event Naming Convention
[Rules and examples]

### Event Catalog
| Event Name | Category | Trigger | Required Fields | Optional Fields |
|------------|----------|---------|-----------------|-----------------|

### Example Events
[JSON examples for key events]

## Funnel Definitions

### Onboarding Funnel
[Steps, targets, current performance]

### Monetization Funnel
[Steps, targets, current performance]

### Engagement Funnel
[Steps, targets, current performance]

## KPI Dashboards

### Executive Dashboard
[Metrics, formulas, targets]

### Design Dashboard
[Metrics, formulas, targets]

### Monetization Dashboard
[Metrics, formulas, targets]

### Live Ops Dashboard
[Metrics, formulas, targets]

## Implementation Plan

### SDK Integration
[Steps, owner, ETA]

### Event Implementation Priority
| Phase | Events | Sprint | Owner |
|-------|--------|--------|-------|
| 1 | Session lifecycle | Sprint 1 | |
| 2 | Progression core | Sprint 2 | |
| 3 | Economy + monetization | Sprint 3 | |
| 4 | Social + engagement | Sprint 4 | |

## Privacy & Compliance

### Data Collection Consent
[GDPR, COPPA flows]

### Data Retention Policy
[How long raw events are kept]

### Anonymization Approach
[Hashing, aggregation rules]

## Alert Configuration

### Critical Alerts
| Alert | Condition | Recipients |
|-------|-----------|------------|
| Crash spike | Crashes > 2x baseline | Dev team |
| Revenue drop | Revenue < 50% baseline | Producer |
| Pipeline failure | No events for 1 hour | DevOps |
```

---

4. **Save the document** to `design/gdd/analytics-spec.md`.

5. **Create an event catalog CSV** at `design/gdd/event-catalog.csv` with all
   event definitions for implementation tracking.

6. **Create a code template** for the event logging service at
   `src/core/analytics/AnalyticsService.cs` (or `.ts`, `.py` based on project).

7. **Suggest next steps**:
   - "Review with `analytics-engineer` agent for technical validation"
   - "Review with `producer` agent for KPI alignment with business goals"
   - "Implement analytics service with `/prototype analytics-integration`"
   - "Set up dashboard in [chosen provider] and configure data pipeline"
   - "Define A/B test framework for future experiments"

8. **Output a summary** with:
   - Analytics provider chosen
   - Number of events defined
   - Key funnels configured
   - Dashboard count and audiences
   - Implementation priority and ETA
   - File paths
