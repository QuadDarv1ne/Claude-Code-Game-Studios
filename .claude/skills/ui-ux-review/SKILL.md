---
name: ui-ux-review
description: "Comprehensive UI/UX review — usability, accessibility, visual hierarchy, interaction design, player flow analysis."
argument-hint: "[path-to-ui-file-or-screen-name|full-game]"
user-invocable: true
allowed-tools: Read, Glob, Grep, Bash, AskUserQuestion
---

When this skill is invoked:

1. **Parse the argument**:
   - If a file path: Review specific UI file/screen
   - If a screen name (e.g., "inventory", "main menu"): Find and review that screen
   - If `full-game` or no argument: Comprehensive UI/UX audit of all screens

2. **Check for existing UI/UX work**:
   - Read `design/gdd/game-concept.md` for visual style and pillars
   - Read `.claude/rules/ui-code.md` for UI coding standards
   - Check `design/ui/` for mockups, wireframes, style guides
   - Read `src/ui/` or `src/` for UI implementations

3. **Run through UI/UX review phases** interactively, using `AskUserQuestion`
   at key decision points. The goal is **player-centered design** — interfaces
   that feel invisible, intuitive, and delightful.

---

### Phase 1: UI Inventory & Architecture

**Screen Map Creation**:

Create a comprehensive list of all UI screens:

| Screen Name | Type | Parent | Child Screens | Entry Points | Exit Points |
|-------------|------|--------|---------------|--------------|-------------|
| Main Menu | Root | - | Settings, Load, New Game | Game launch | Into game |
| HUD | Overlay | - | Pause, Inventory | Gameplay | N/A |
| Inventory | Modal | HUD | Item Detail, Equip | HUD, Pause | Back to HUD |
| ... | ... | ... | ... | ... | ... |

**Navigation Flow Analysis**:

For each major player goal, map the navigation path:
```
Goal: "Equip better sword"
1. Open Inventory (I key / button press)
2. Navigate to Weapons tab
3. Select current sword
4. Choose "Compare" or "Unequip"
5. Select new sword
6. Choose "Equip"
7. Confirm (if required)
8. Return to game

Total clicks: 4-6
Ideal: 3-4
Problem areas: Step 4 requires scrolling through context menu
```

**UI System Architecture Review**:

- [ ] Separation of concerns (data, logic, presentation)
- [ ] Event-driven updates (not polling)
- [ ] Proper lifecycle management (init, update, dispose)
- [ ] Input handling abstraction (keyboard, mouse, controller, touch)
- [ ] Localization-ready (text externalization, RTL support)
- [ ] Resolution independence (anchoring, scaling, safe areas)

---

### Phase 2: Usability Heuristics Evaluation

Evaluate against **Nielsen's 10 Heuristics** (adapted for games):

| Heuristic | Rating (1-5) | Issues Found | Severity |
|-----------|--------------|--------------|----------|
| **1. Visibility of System Status** | | | |
| **2. Match Between System & Real World** | | | |
| **3. User Control & Freedom** | | | |
| **4. Consistency & Standards** | | | |
| **5. Error Prevention** | | | |
| **6. Recognition Rather Than Recall** | | | |
| **7. Flexibility & Efficiency of Use** | | | |
| **8. Aesthetic & Minimalist Design** | | | |
| **9. Help Users Recognize/Recover From Errors** | | | |
| **10. Help & Documentation** | | | |

**Detailed Evaluation Criteria**:

#### 1. Visibility of System Status
- [ ] Player always knows current game state (health, resources, objectives)
- [ ] Loading states clearly indicated
- [ ] Actions have visible feedback (button presses, selections)
- [ ] Progress indicators for multi-step processes
- [ ] Network status shown (online/offline, latency)

#### 2. Match Between System & Real World
- [ ] Icons are recognizable (gear = settings, heart = health)
- [ ] Language matches player vocabulary (not dev jargon)
- [ ] Metaphors are consistent (inventory = container, tabs = folders)
- [ ] Numbers formatted appropriately (1,000 vs 1k vs 1,000.00)

#### 3. User Control & Freedom
- [ ] Easy to go back (consistent back button)
- [ ] Cancel options always available
- [ ] Destructive actions require confirmation
- [ ] Undo available where appropriate
- [ ] Player can exit any screen (no soft locks)

#### 4. Consistency & Standards
- [ ] Button styles consistent across screens
- [ ] Color meanings consistent (red = danger, green = go)
- [ ] Icon usage consistent (same icon = same meaning)
- [ ] Spacing and alignment follow grid
- [ ] Typography hierarchy consistent (H1 > H2 > body)

#### 5. Error Prevention
- [ ] Invalid actions disabled (grayed out), not hidden
- [ ] Confirmation for irreversible actions (delete save, spend currency)
- [ ] Input validation with helpful messages
- [ ] Dangerous zones have clear warnings
- [ ] Default choices are safe

#### 6. Recognition Rather Than Recall
- [ ] Options visible, not buried in menus
- [ ] Item stats shown on hover/click (not memorized)
- [ ] Quest objectives visible during gameplay
- [ ] Recent actions accessible (undo history, craft history)
- [ ] Comparison values shown side-by-side

#### 7. Flexibility & Efficiency of Use
- [ ] Keyboard shortcuts for power users
- [ ] Quick-select options (favorite items, recent screens)
- [ ] Batch operations (sell all, equip all)
- [ ] Customizable controls
- [ ] Accessibility options (text size, colorblind mode)

#### 8. Aesthetic & Minimalist Design
- [ ] Every element serves a purpose
- [ ] No decorative elements that compete for attention
- [ ] White space used effectively
- [ ] Information density appropriate for context
- [ ] Visual hierarchy guides eye to important elements

#### 9. Help Users Recognize/Recover From Errors
- [ ] Error messages in plain language
- [ ] Error messages suggest solutions
- [ ] Recovery paths clear (retry, load, contact support)
- [ ] System errors logged and traceable
- [ ] No blame language ("You failed" vs "Action failed")

#### 10. Help & Documentation
- [ ] Tutorial covers core UI interactions
- [ ] Help accessible from relevant screens
- [ ] Tooltips explain unclear elements
- [ ] Glossary/codex for game-specific terms
- [ ] Search function for large help systems

---

### Phase 3: Visual Hierarchy & Layout

**F-Pattern & Z-Pattern Analysis**:

For each screen, evaluate:
- Does important information follow natural eye movement?
- **F-Pattern** (text-heavy screens): Key info on left, headings scan-friendly
- **Z-Pattern** (action screens): Logo → main CTA → secondary → bottom action

**Visual Weight Assessment**:

| Element | Visual Weight | Should Be | Fix Needed? |
|---------|---------------|-----------|-------------|
| Primary action button | High | Highest | |
| Secondary actions | Medium | Lower than primary | |
| Decorative elements | Low | Lowest | |
| Critical info (health) | High | Highest | |
| Nice-to-know info | Medium | Lower than critical | |

**Spacing & Grid Analysis**:

- [ ] Consistent spacing scale (4px, 8px, 16px, 24px, 32px, 48px)
- [ ] Elements aligned to grid (no orphan pixels)
- [ ] Related items grouped (proximity = relationship)
- [ ] Unrelated items separated (white space = section break)
- [ ] Touch targets minimum 44x44px (mobile), 32x32px (desktop)

**Color & Contrast Review**:

- [ ] Sufficient contrast ratio (WCAG AA: 4.5:1 text, 3:1 large)
- [ ] Color not sole indicator of meaning (add icons/text)
- [ ] Colorblind-safe palette (deuteranopia, protanopia, tritanopia)
- [ ] Brand colors used consistently
- [ ] State colors clear (disabled, selected, hover, focus)

---

### Phase 4: Interaction Design

**Input Method Coverage**:

| Input | Supported? | Notes |
|-------|------------|-------|
| Mouse | | Click, hover, scroll, drag-drop |
| Keyboard | | Shortcuts, navigation, text input |
| Controller | | Gamepad navigation, button prompts |
| Touch | | Gestures, tap targets, swipe actions |

**Interaction Feedback**:

| State | Visual | Audio | Haptic |
|-------|--------|-------|--------|
| Hover | | | N/A |
| Focus | | | N/A |
| Press | | | |
| Selected | | | |
| Disabled | | | N/A |
| Loading | | | N/A |
| Complete | | | |
| Error | | | |

**Animation & Timing**:

| Animation | Duration | Easing | Purpose |
|-----------|----------|--------|---------|
| Button hover | 0.15s | ease-out | Feedback |
| Screen transition | 0.3s | ease-in-out | Context |
| Modal appear | 0.25s | ease-out | Focus |
| Loading spinner | 1s linear | infinite | Status |
| Success checkmark | 0.4s | ease-out | Confirmation |

**Microinteraction Review**:

- [ ] Buttons have hover/press states
- [ ] Toggles have clear on/off states
- [ ] Sliders show current value and range
- [ ] Progress bars animate smoothly
- [ ] Notifications appear/disappear gracefully
- [ ] Drag-and-drop has visual feedback
- [ ] Scroll indicators show position

---

### Phase 5: Accessibility Audit

**WCAG 2.1 Compliance** (target Level AA):

| Criteria | Status | Issues | Priority |
|----------|--------|--------|----------|
| **1.1 Text Alternatives** | | | |
| **1.2 Time-Based Media** | | | |
| **1.3 Adaptable Content** | | | |
| **1.4 Distinguishable** | | | |
| **2.1 Keyboard Accessible** | | | |
| **2.2 Enough Time** | | | |
| **2.3 Seizures** | | | |
| **2.4 Navigable** | | | |
| **3.1 Readable** | | | |
| **3.2 Predictable** | | | |
| **3.3 Input Assistance** | | | |
| **4.1 Compatible** | | | |

**Game-Specific Accessibility**:

| Category | Feature | Implemented? | Notes |
|----------|---------|--------------|-------|
| **Vision** | Text size options | | |
| **Vision** | Colorblind modes | | |
| **Vision** | High contrast mode | | |
| **Vision** | Screen reader support | | |
| **Hearing** | Subtitles/captions | | |
| **Hearing** | Visual audio cues | | |
| **Hearing** | Volume sliders (SFX/music/voice) | | |
| **Motor** | Remappable controls | | |
| **Motor** | Toggle vs hold options | | |
| **Motor** | Aim assist / auto-complete | | |
| **Motor** | Reduced QTE pressure | | |
| **Cognitive** | Simplified UI mode | | |
| **Cognitive** | Quest markers/navigation | | |
| **Cognitive** | Pause-anywhere | | |
| **Cognitive** | No time limits option | | |

**Inclusive Design Review**:

- [ ] Character creator includes diverse options (skin tone, body types, abilities)
- [ ] Pronoun options or gender-neutral language
- [ ] Cultural sensitivity in icons, colors, symbols
- [ ] Age-appropriate complexity (consider younger players)
- [ ] Literacy level appropriate for target audience

---

### Phase 6: Player Flow Analysis

**Critical Path Testing**:

For each critical player journey, document:

```
Flow: "First Purchase" (F2P game)
1. Player earns/needs currency
2. Player opens shop
3. Player browses items
4. Player selects item
5. Player confirms purchase
6. Transaction completes
7. Item received

Friction Points:
- Step 3: Shop has too many tabs, unclear organization
- Step 5: Confirmation dialog has tiny text
- Step 7: No animation showing item added to inventory

Time to Complete: ~45 seconds (target: 30 seconds)
Click Count: 7 clicks (target: 5 clicks)
```

**Cognitive Load Assessment**:

| Screen | Elements Visible | Decisions Required | Reading Load | Rating |
|--------|------------------|-------------------|--------------|--------|
| Main Menu | 8 buttons | 1 choice | Low | ✓ |
| Inventory | 45 items, 12 stats | Multiple | Medium | ⚠ |
| Skill Tree | 80 nodes, 6 tabs | Complex | High | ✗ |

**Emotional Journey Mapping**:

For key flows, map emotional state:
```
Boss Death Screen:
Frustration (died) → Confusion (what now?) → Relief (retry is instant) → Determination (try again)

Improvement: Add brief encouragement message, show progress made ("You dealt 80% damage - close!")
```

---

### Phase 7: Documentation

Generate the UI/UX review report:

```markdown
# UI/UX Review Report

## Executive Summary
[Overall assessment, top 3 issues, top 3 strengths]

## UI Inventory
[Screen map, navigation flows, architecture review]

## Usability Evaluation

### Heuristic Analysis
[10 heuristics with ratings and issues]

### Severity Summary
| Severity | Count | Must Fix Before |
|----------|-------|-----------------|
| Critical | | Launch |
| Major | | Beta |
| Minor | | Post-launch |
| Cosmetic | | Polish |

## Visual Design Review

### Hierarchy Assessment
[Visual weight, spacing, grid analysis]

### Color & Contrast
[Contrast ratios, colorblind safety]

### Typography
[Font choices, sizing, readability]

## Interaction Design

### Input Coverage
[Mouse, keyboard, controller, touch]

### Feedback Systems
[Visual, audio, haptic feedback audit]

### Animation Review
[Timing, easing, purpose]

## Accessibility Audit

### WCAG Compliance
[Level AA checklist results]

### Game-Specific Features
[Vision, hearing, motor, cognitive]

### Recommendations
[Priority accessibility improvements]

## Player Flow Analysis

### Critical Path Testing
[Key flows with friction points]

### Cognitive Load
[Element counts, decision fatigue]

### Emotional Journey
[Player emotion mapping]

## Prioritized Recommendations

### P0 - Critical (Fix Before Next Milestone)
| ID | Issue | Screen | Impact | Effort |
|----|-------|--------|--------|--------|

### P1 - Major (Fix Before Beta)
| ID | Issue | Screen | Impact | Effort |
|----|-------|--------|--------|--------|

### P2 - Minor (Polish Phase)
| ID | Issue | Screen | Impact | Effort |
|----|-------|--------|--------|--------|

## Positive Observations
[What's working well -- always include]
```

---

4. **Save the report** to `docs/ui-ux-review-[date].md`.

5. **Create a screenshot inventory** at `design/ui/screenshots/` with annotated
   images showing issues (arrows, callouts, before/after mockups).

6. **Suggest next steps**:
   - "Review with `ux-designer` agent for usability deep-dive"
   - "Review with `art-director` agent for visual consistency"
   - "Review with `accessibility-specialist` agent for accessibility audit"
   - "Create wireframes for fixes with `/prototype ui-wireframes`"
   - "Implement priority fixes and re-test with `/playtest-report`"

7. **Output a summary** with:
   - Overall rating (1-5 stars)
   - Critical issues count
   - Top 3 must-fix items
   - Top 3 strengths to preserve
   - Accessibility compliance level
   - File paths
