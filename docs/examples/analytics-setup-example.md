# Example: Analytics Setup Workflow

This example demonstrates how to use `/analytics-setup` to configure comprehensive
game analytics for a Unity mobile game.

## Context

**Game:** "Dungeon Delver" — roguelike deck-builder  
**Platform:** iOS + Android  
**Analytics Provider:** Unity Analytics + GameAnalytics  
**Goal:** Track player behavior, funnels, and monetization

---

## Session Transcript

### Step 1: Invoke the Skill

```
/analytics-setup full
```

### Step 2: Analytics Strategy

The skill asks about goals and constraints:

> **Q:** What are the top 3 questions you need data to answer?
>
> **A:** 
> 1. Where do players quit in the tutorial?
> 2. What drives IAP purchases?
> 3. Is the difficulty curve balanced?

> **Q:** Technical constraints?
>
> **A:** Unity 2022 LTS, offline-first with batching, <100KB data budget per session.

> **Q:** Privacy requirements?
>
> **A:** GDPR compliant, no PII, 90-day retention for raw events.

### Step 3: Event Schema Design

The skill proposes an event taxonomy:

```
session.*      — started, ended, paused, resumed
progression.*  — level_start, level_complete, level_fail, quit
economy.*      — currency_earn, currency_spend, item_acquire
monetization.* — iap_offer, iap_view, iap_purchase, ad_view
tutorial.*     — step_view, step_complete, step_skip
```

### Step 4: Funnel Definition

**Onboarding Funnel:**

```
1. App install/open
   ↓ (target: >90%)
2. Tutorial step 1 complete
   ↓ (target: >85%)
3. Tutorial complete
   ↓ (target: >80%)
4. Core loop first pass
   ↓ (target: >75%)
5. First session natural close
   ↓ (target: D1 >40%)
```

### Step 5: KPI Dashboard

The skill defines dashboards:

**Executive Dashboard:**
| Metric | Formula | Target |
|--------|---------|--------|
| DAU | Unique users/day | Growth WoW |
| D1 Retention | D1 returning / D0 new | >40% |
| ARPDAU | Revenue / DAU | $0.10 |
| Conversion | Purchasers / MAU | >2% |

**Design Dashboard:**
| Metric | Formula | Target |
|--------|---------|--------|
| Tutorial Completion | Finished / Started | >80% |
| Session Length | Avg minutes | 10-20 min |
| Deaths per Level | Avg deaths | 1.5-3.0 |

### Step 6: Implementation Plan

The skill generates a checklist:

```markdown
### Sprint 1: Core Events
- [ ] session.started / session.ended
- [ ] progression.level_*
- [ ] economy.currency_*

### Sprint 2: Monetization
- [ ] monetization.iap_*
- [ ] monetization.ad_*

### Sprint 3: Dashboards
- [ ] Unity Analytics dashboard
- [ ] Automated daily reports
```

### Step 7: Output Files

The skill creates:

1. `design/gdd/analytics-spec.md` — full specification
2. `design/gdd/event-catalog.csv` — all events with properties
3. `src/core/analytics/AnalyticsService.cs` — code template

---

## Output: analytics-spec.md (excerpt)

```markdown
# Analytics Specification

## Event Schema

### session.started
Fired when a game session begins.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| session_id | string | Yes | Unique identifier |
| player_level | int | Yes | Current level |
| days_since_install | int | Yes | Days since first launch |

### progression.level_complete
Fired on successful level completion.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| level_id | string | Yes | Level identifier |
| completion_time_sec | int | Yes | Time to complete |
| deaths | int | Yes | Times died |
```

---

## Output: event-catalog.csv (excerpt)

```csv
event_name,category,priority,properties
session.started,session,P0,"session_id,player_level,days_since_install"
session.ended,session,P0,"session_id,duration_sec,end_reason"
progression.level_start,progression,P0,"level_id,attempt_number,player_level"
progression.level_complete,progression,P0,"level_id,completion_time,deaths"
economy.currency_earn,economy,P0,"currency_type,amount,source,balance_after"
monetization.iap_purchase,monetization,P0,"product_id,price_usd,is_first_purchase"
```

---

## Output: AnalyticsService.cs (excerpt)

```csharp
using Unity.Services.Analytics;

public class AnalyticsService : MonoBehaviour
{
    private static AnalyticsService _instance;
    
    public static void Init()
    {
        AnalyticsService.Instance.StartSession();
    }
    
    public static void TrackLevelComplete(string levelId, int timeSec, int deaths)
    {
        Analytics.CustomData("progression.level_complete", new Dictionary<string, object>
        {
            { "level_id", levelId },
            { "completion_time_sec", timeSec },
            { "deaths", deaths }
        });
    }
    
    // ... more methods
}
```

---

## Next Steps

After running `/analytics-setup`:

1. **Review with `analytics-engineer`** — validate event coverage
2. **Review with `technical-director`** — approve architecture
3. **Implement in Unity** — integrate AnalyticsService
4. **Test in dev build** — verify events appear in dashboard
5. **Configure alerts** — crash spikes, revenue drops

---

## Key Learnings

- **Event design first** — define schema before implementing
- **Funnel tracking** — measure player drop-off at each step
- **KPI dashboards** — different stakeholders need different views
- **Privacy by design** — GDPR compliance from day one
- **Offline-first** — batch events, retry on failure

---

*This example shows how `/analytics-setup` produces both design documentation
and implementation templates.*
