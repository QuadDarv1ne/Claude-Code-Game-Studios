# Event Catalog

## Overview

**Game:** [Game Name]  
**Version:** [Version]  
**Date:** [Date]  
**Author:** [Author]

This document defines all analytics events tracked in the game. Each event is
immutable, timestamped, and includes context for reconstruction.

---

## Event Naming Convention

- **Format:** `category.action` (snake_case)
- **Categories:** session, progression, economy, combat, social, monetization, tutorial, ui, error
- **Actions:** start, complete, fail, acquire, consume, view, click, purchase, error

---

## Session Events

### session.started

Fired when a game session begins.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| session_id | string | Yes | Unique session identifier |
| player_level | int | Yes | Current player level |
| days_since_install | int | Yes | Days since first launch |
| last_session_ago_sec | int | No | Seconds since last session |

**Example:**
```json
{
  "event_type": "session.started",
  "session_id": "sess_abc123",
  "player_level": 5,
  "days_since_install": 3,
  "last_session_ago_sec": 86400
}
```

### session.ended

Fired when a session ends (normal or crash).

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| session_id | string | Yes | Unique session identifier |
| duration_sec | int | Yes | Session length in seconds |
| end_reason | string | Yes | "quit", "crash", "idle_timeout" |

---

## Progression Events

### progression.level_start

Fired when a player begins a level/mission/stage.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| level_id | string | Yes | Level identifier |
| level_name | string | Yes | Display name |
| attempt_number | int | Yes | First try = 1, etc. |
| player_level | int | Yes | Player level at start |
| equipment_score | int | No | Gear power level |

### progression.level_complete

Fired on successful level completion.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| level_id | string | Yes | Level identifier |
| completion_time_sec | int | Yes | Time to complete |
| deaths | int | Yes | Times died in level |
| secrets_found | int | No | Optional collectibles |
| stars_earned | int | No | 0-3 star rating |
| health_remaining_pct | int | No | HP at completion |

### progression.level_fail

Fired when player fails a level.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| level_id | string | Yes | Level identifier |
| fail_reason | string | Yes | "death", "timeout", "objective_fail" |
| time_elapsed_sec | int | Yes | Time before fail |
| progress_pct | int | No | How far they got |

### progression.quit

Fired when player abandons a level mid-attempt.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| level_id | string | Yes | Level identifier |
| time_elapsed_sec | int | Yes | Time before quit |
| progress_pct | int | No | How far they got |
| quit_reason | string | No | "stuck", "frustrated", "afk" |

---

## Economy Events

### economy.currency_earn

Fired when player earns any currency.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| currency_type | string | Yes | "gold", "gems", "tokens" |
| amount | int | Yes | Amount earned |
| source | string | Yes | "quest", "purchase", "reward", "craft_sell" |
| source_id | string | No | Specific source (quest_id, etc.) |
| balance_after | int | Yes | Total balance after earn |

### economy.currency_spend

Fired when player spends any currency.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| currency_type | string | Yes | "gold", "gems", "tokens" |
| amount | int | Yes | Amount spent |
| sink | string | Yes | "upgrade", "consumable", "cosmetic", "convenience" |
| item_id | string | No | What was purchased |
| balance_after | int | Yes | Total balance after spend |

### economy.item_acquire

Fired when player obtains an item.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| item_id | string | Yes | Item identifier |
| item_name | string | Yes | Display name |
| item_type | string | Yes | "weapon", "armor", "consumable", "material" |
| rarity | string | No | "common", "rare", "epic", "legendary" |
| source | string | Yes | "loot", "craft", "purchase", "quest_reward" |
| quantity | int | Yes | Stack size |

### economy.item_consume

Fired when player uses/destroys an item.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| item_id | string | Yes | Item identifier |
| item_type | string | Yes | Type |
| consume_reason | string | Yes | "use", "craft", "sell", "discard" |
| quantity | int | Yes | Stack size consumed |

---

## Combat Events

### combat.enemy_kill

Fired when player defeats an enemy.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| enemy_id | string | Yes | Enemy type |
| enemy_level | int | Yes | Enemy level |
| damage_dealt | int | Yes | Total damage |
| damage_taken | int | No | Damage player took |
| time_to_kill_sec | float | No | Seconds to defeat |
| ability_used | array | No | Abilities used |

### combat.player_death

Fired when player dies.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| killer_id | string | No | What killed player |
| damage_source | string | No | "enemy", "trap", "environment" |
| location_id | string | No | Where death occurred |
| respawn_time_sec | int | No | Time to respawn |

### combat.ability_use

Fired when player uses an ability/skill.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| ability_id | string | Yes | Ability identifier |
| ability_name | string | Yes | Display name |
| target_type | string | Yes | "enemy", "self", "ally", "ground" |
| cooldown_remaining | float | No | If pressed early |
| hit_count | int | No | Targets hit |

---

## Monetization Events

### monetization.iap_offer

Fired when an IAP offer is shown.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| offer_id | string | Yes | Offer identifier |
| offer_type | string | Yes | "direct", "store", "popup", "reward" |
| item_id | string | Yes | What's being sold |
| price_usd | float | Yes | Price in USD |
| discount_pct | int | No | If on sale |

### monetization.iap_view

Fired when player opens IAP store.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| store_type | string | Yes | "main", "event", "daily" |
| items_visible | int | Yes | Number of offers shown |

### monetization.iap_purchase

Fired when player completes a purchase.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| product_id | string | Yes | Store product ID |
| item_id | string | Yes | What was purchased |
| price_usd | float | Yes | Actual price paid |
| currency_amount | int | Yes | Virtual currency received |
| is_first_purchase | bool | Yes | First ever IAP? |
| transaction_id | string | Yes | Platform transaction ID |

### monetization.ad_view

Fired when player views an ad.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| ad_type | string | Yes | "rewarded", "interstitial", "banner" |
| ad_network | string | Yes | "admob", "unity_ads", etc. |
| placement | string | Yes | Where ad appeared |
| completed | bool | No | For rewarded: did it finish? |
| reward_granted | string | No | What player received |

---

## Tutorial Events

### tutorial.step_view

Fired when a tutorial step is shown.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| tutorial_id | string | Yes | Tutorial identifier |
| step_id | string | Yes | Step identifier |
| step_type | string | Yes | "dialogue", "prompt", "highlight", "force" |

### tutorial.step_complete

Fired when player completes a tutorial step.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| tutorial_id | string | Yes | Tutorial identifier |
| step_id | string | Yes | Step identifier |
| time_spent_sec | int | No | Time on step |
| attempts | int | No | Times tried |

### tutorial.step_skip

Fired when player skips tutorial content.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| tutorial_id | string | Yes | Tutorial identifier |
| step_id | string | Yes | Step skipped |
| skip_type | string | Yes | "button", "timeout", "death" |

---

## UI Events

### ui.screen_open

Fired when a major screen opens.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| screen_id | string | Yes | Screen identifier |
| source | string | No | What opened it |

### ui.screen_close

Fired when a screen closes.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| screen_id | string | Yes | Screen identifier |
| time_open_sec | int | No | How long it was open |
| action_taken | string | No | What player did |

### ui.button_click

Fired for important button clicks.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| button_id | string | Yes | Button identifier |
| screen_id | string | Yes | Parent screen |
| click_count | int | No | Times clicked this session |

---

## Error Events

### error.crash

Fired when game crashes (sent on next launch).

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| crash_id | string | Yes | Crash identifier |
| error_message | string | Yes | Exception message |
| stack_trace | string | Yes | Call stack |
| memory_mb | int | No | Memory at crash |
| location_id | string | No | Where crash occurred |

### error.exception

Fired for caught exceptions.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| error_id | string | Yes | Error identifier |
| error_message | string | Yes | Exception message |
| severity | string | Yes | "warning", "error", "critical" |
| recovered | bool | Yes | Did game continue? |

---

## Event Implementation Checklist

| Event | Priority | Sprint | Status |
|-------|----------|--------|--------|
| session.started | P0 | 1 | |
| session.ended | P0 | 1 | |
| progression.* | P0 | 1 | |
| economy.* | P0 | 1 | |
| combat.* | P1 | 2 | |
| monetization.* | P0 | 1 | |
| tutorial.* | P1 | 2 | |
| ui.* | P2 | 3 | |
| error.* | P0 | 1 | |

---

*Template for event catalog. Add all events before implementation.*
