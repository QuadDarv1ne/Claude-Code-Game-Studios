# Example: UI/UX Review Workflow

This example demonstrates how to use `/ui-ux-review` to conduct a comprehensive
usability and accessibility audit of a game's UI.

## Context

**Game:** "Dungeon Delver" — roguelike deck-builder  
**Platform:** PC + Mobile (cross-platform)  
**Review Scope:** Full game UI audit  
**Goal:** Identify usability issues before beta launch

---

## Session Transcript

### Step 1: Invoke the Skill

```
/ui-ux-review full-game
```

### Step 2: UI Inventory

The skill creates a screen map:

| Screen | Type | Status | Issues |
|--------|------|--------|--------|
| Main Menu | Root | ✅ | Minor |
| HUD | Overlay | ⚠️ | 3 issues |
| Inventory | Modal | ❌ | 7 issues |
| Shop | Modal | ⚠️ | 4 issues |
| Settings | Modal | ✅ | 1 issue |

### Step 3: Heuristic Evaluation

The skill evaluates against Nielsen's 10 heuristics:

**1. Visibility of System Status** — Rating: 3/5

| Issue | Screen | Severity |
|-------|--------|----------|
| No loading indicator on card purchase | Shop | P1 |
| Health bar doesn't show exact values | HUD | P2 |
| No confirmation when deck saved | Deck Builder | P2 |

**2. Match Between System & Real World** — Rating: 4/5

| Issue | Screen | Severity |
|-------|--------|----------|
| "Arcane" stat unclear to new players | Card Tooltip | P2 |
| Icon for "poison" looks like "disease" | Status Effects | P3 |

**3. User Control & Freedom** — Rating: 2/5 ⚠️

| Issue | Screen | Severity |
|-------|--------|----------|
| No way to undo card discard | Gameplay | P0 |
| Can't exit shop without purchase | Shop | P1 |
| Back button inconsistent | All screens | P1 |

### Step 4: Accessibility Audit

**WCAG 2.1 Level AA Compliance:**

| Criteria | Status | Issues |
|----------|--------|--------|
| 1.4 Distinguishable | ❌ Fail | Contrast ratios |
| 2.1 Keyboard Accessible | ✅ Pass | |
| 2.4 Navigable | ⚠️ Partial | Focus indicators |
| 3.2 Predictable | ❌ Fail | Inconsistent patterns |

**Color Contrast Issues:**

| Element | Current Ratio | Required | Severity |
|---------|---------------|----------|----------|
| White text on yellow button | 2.8:1 | 4.5:1 | P0 |
| Grey disabled text | 3.1:1 | 4.5:1 | P1 |
| Health bar red on dark bg | 4.2:1 | 4.5:1 | P2 |

**Colorblind Safety:**

- ❌ Red/green used as sole indicator (poison vs. buff)
- ❌ Team colors indistinguishable for deuteranopia
- ✅ Icons supplement color in most cases

### Step 5: Player Flow Analysis

**Critical Path: "First Card Purchase"**

| Step | Screen | Clicks | Time | Friction |
|------|--------|--------|------|----------|
| 1. Open shop | HUD | 1 | 0.5s | ✅ |
| 2. Browse cards | Shop | 3-5 | 15s | ⚠️ No filter |
| 3. Select card | Shop | 1 | 1s | ✅ |
| 4. View details | Shop | 1 | 5s | ⚠️ Stats unclear |
| 5. Confirm purchase | Shop | 1 | 1s | ❌ No price confirmation |
| 6. Receive card | Shop | 0 | 2s | ❌ No animation |

**Total:** 7-9 clicks, ~25 seconds  
**Target:** 5 clicks, 15 seconds  
**Friction Points:** Steps 4, 5, 6

### Step 6: Cognitive Load Assessment

| Screen | Elements | Decisions | Reading | Rating |
|--------|----------|-----------|---------|--------|
| Main Menu | 6 buttons | 1 | Low | ✅ Low |
| Inventory | 45 cards, 8 stats | 5+ | Medium | ⚠️ High |
| Shop | 24 cards, prices | 3+ | Medium | ⚠️ High |

### Step 7: Prioritized Recommendations

**P0 - Critical (Fix Before Beta):**

| ID | Issue | Screen | Recommendation |
|----|-------|--------|----------------|
| UI-001 | No undo for discard | Gameplay | Add undo button (1 turn window) |
| UI-002 | Low contrast text | All screens | Update color palette |
| UI-003 | Red/green only indicators | Status effects | Add icons + patterns |

**P1 - Major (Fix Before Launch):**

| ID | Issue | Screen | Recommendation |
|----|-------|--------|----------------|
| UI-004 | No loading feedback | Shop | Add spinner/progress bar |
| UI-005 | Inconsistent back button | All | Standardize navigation |
| UI-006 | No purchase confirmation | Shop | Add "Confirm" dialog |

**P2 - Minor (Polish Phase):**

| ID | Issue | Screen | Recommendation |
|----|-------|--------|----------------|
| UI-007 | Stats unclear | Tooltip | Add icon + description |
| UI-008 | No card acquisition animation | Shop | Add celebratory VFX |

### Step 8: Output Files

The skill creates:

1. `docs/ui-ux-review-2026-03-29.md` — full audit report
2. `design/ui/screenshots/audit/` — annotated screenshots
3. `design/ui/wireframes/proposed-fixes/` — mockups for key issues

---

## Output: ui-ux-review-report.md (excerpt)

```markdown
# UI/UX Audit Report

## Executive Summary
Overall Rating: 2.8/5 stars

Top 3 Strengths:
1. Clean visual design
2. Consistent iconography
3. Responsive controls

Top 3 Critical Issues:
1. No undo for card discard (P0)
2. Color contrast fails WCAG AA (P0)
3. Red/green color-only indicators (P0)

## Heuristic Evaluation
[Full 10 heuristics with ratings]

## Accessibility Audit
- WCAG 2.1 Level AA: FAIL (3 criteria)
- Colorblind Safety: PARTIAL
- Keyboard Navigation: PASS

## Prioritized Recommendations
### P0 - Critical
[3 issues with fixes]

### P1 - Major
[5 issues with fixes]

### P2 - Minor
[8 issues with fixes]
```

---

## Next Steps

After running `/ui-ux-review`:

1. **Review with `ux-designer`** — validate findings
2. **Review with `art-director`** — approve visual changes
3. **Review with `accessibility-specialist`** — compliance plan
4. **Create wireframes** — `/prototype ui-wireframes`
5. **Implement P0 fixes** — before beta launch
6. **Re-test** — `/ui-ux-review` after fixes

---

## Key Learnings

- **Early audits save time** — fix issues before they're baked in
- **Accessibility is not optional** — WCAG compliance is baseline
- **Player flows reveal friction** — count clicks, measure time
- **Cognitive load kills engagement** — simplify complex screens
- **Annotated screenshots** — show, don't just tell

---

*This example shows how `/ui-ux-review` produces a comprehensive audit with
prioritized recommendations ready for implementation.*
