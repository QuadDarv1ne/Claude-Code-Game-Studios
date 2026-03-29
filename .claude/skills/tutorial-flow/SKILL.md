---
name: tutorial-flow
description: "Design player onboarding and tutorial systems — first-time user experience, progressive learning, retention optimization."
argument-hint: "[focus: first-time|progressive|contextual|all]"
user-invocable: true
allowed-tools: Read, Glob, Grep, Write, AskUserQuestion
---

When this skill is invoked:

1. **Parse the argument** for tutorial focus area:
   - `first-time`: First-time user experience (FTUE) — first 5-15 minutes
   - `progressive`: Progressive learning — unlocking mechanics over time
   - `contextual`: Contextual hints — just-in-time learning during gameplay
   - `all`: Comprehensive onboarding system (default)

2. **Check for existing onboarding work**:
   - Read `design/gdd/game-concept.md` for core loop and pillars
   - Read `design/gdd/` for any existing tutorial or level design docs
   - Check `src/` for existing tutorial implementations

3. **Run through tutorial design phases** interactively, using `AskUserQuestion`
   at key decision points. The goal is **invisible teaching** — players learn
   while having fun, not through lectures.

---

### Phase 1: Onboarding Strategy

**First Impressions Analysis**:

- What's the **emotional goal** for the first 60 seconds? (excitement, curiosity, comfort, challenge)
- What's the **single most important action** players must learn first?
- What's your **difficulty curve philosophy**? (gentle slope, steep challenge, player-choice)
- What's your **retention target**? (D1: 40% typical mobile, D7: 15%, D30: 5%)

**Player Skill Assumptions**:

- Target audience familiarity with genre? (veterans vs. newcomers)
- Platform conventions assumed? (WASD, controller, touch gestures)
- Minimum age / cognitive load considerations?

**Tutorial Design Philosophy** (choose primary approach):

| Approach | Description | Best For |
|----------|-------------|----------|
| **Show, Don't Tell** | Demonstrate through gameplay, minimal text | Action games, visual learners |
| **Sandbox First** | Safe space to experiment before stakes | Creative games, exploration |
| **Contextual Popups** | Just-in-time hints when mechanics appear | Complex games, RPGs, strategy |
| **Mandatory Training** | Required completion before main game | Competitive multiplayer, hardcore |
| **Optional Tutorial** | Skippable, accessible from menu | Casual games, accessible design |

**Failure State Design**:

- How punishing is early failure? (no penalty, soft penalty, hard reset)
- What's the retry flow? (instant restart, checkpoint, full level)
- How do you teach from failure? (hints after N failures, adaptive difficulty)

---

### Phase 2: First-Time User Experience (FTUE)

Design the **first 5-15 minutes** in detail:

**Minute 0-1: Hook**
- What's the first thing players see? (cinematic, gameplay, menu, title)
- What's the first interaction? (tap to start, create character, skip intro)
- How quickly do players reach the core loop? (target: under 2 minutes)

**Minute 1-3: First Verb**
- What's the first player verb taught? (move, jump, attack, build)
- How is it introduced? (forced use, guided choice, free discovery)
- What feedback confirms success? (visual, audio, haptic, progression)

**Minute 3-7: Core Loop Introduction**
- What's the first complete loop players experience?
- Example: "See enemy → Attack → Collect loot → Upgrade"
- How many repetitions before moving on? (target: 2-3 successful loops)

**Minute 7-15: First Complication**
- What's the first twist or added complexity?
- Examples: New enemy type, resource scarcity, time pressure, choice consequence
- How does this create "easy to learn, hard to master" tension?

**First Session Closure**:
- What's the natural stopping point? (first boss, base established, story beat)
- What progression is saved? (level, items, unlocks)
- What's the "come back" hook? (unstuck energy, daily reward, cliffhanger)

**FTUE Flow Document**:

```markdown
## First-Time User Experience Flow

### Pre-Game (0-30 seconds)
| Step | Screen | Player Action | System Response |
|------|--------|---------------|-----------------|

### First Interaction (30-90 seconds)
| Step | Screen | Player Action | Feedback |

### Core Loop First Pass (2-7 minutes)
| Step | Mechanic | Teaching Method | Success Criteria |

### First Complication (7-15 minutes)
| Complication | Introduction Method | Player Tools | Expected Outcome |

### Session End Hook
| Hook Type | Description | Retention Goal |
```

---

### Phase 3: Progressive Learning Design

Map out **mechanic unlocking** over the first hours/days:

**Mechanic Dependency Tree**:

Create a prerequisite graph:
```
Movement → Jump → Double Jump → Air Dash
   ↓
Combat → Attack → Block → Counter → Combo
   ↓
Progression → XP → Level Up → Skill Tree → Respec
```

**Pacing Schedule**:

| Time | New Mechanic | Practice Opportunity | Mastery Check |
|------|--------------|---------------------|---------------|
| 0-5 min | Move, interact | Navigate to goal | Reach first area |
| 5-10 min | Attack basic | Defeat 3 slimes | Combat encounter |
| 10-20 min | Block/parry | Enemy with telegraph | No damage taken |
| 20-40 min | Resource management | Limited potions | Boss fight |
| 1-2 hours | Skill tree | First level up | Choose first skill |
| 2-5 hours | Crafting | Gather + craft | First crafted item |

**Scaffolding Techniques**:

| Technique | Description | Example |
|-----------|-------------|---------|
| **I Do** | Show the action | NPC demonstrates, video, animation |
| **We Do** | Guided practice | "Hold [button] to..." with input overlay |
| **You Do** | Independent execution | Player performs alone, with safety net |
| **Mastery** | Unassisted application | Challenge requiring the skill |

**Cognitive Load Management**:

- One new concept at a time (no "input storms")
- Spacing: Time between new mechanics (target: 3-5 minutes early, 10+ minutes late)
- Reinforcement: Revisit mechanics every 15-30 minutes
- Chunking: Group related mechanics into "lessons"

---

### Phase 4: Contextual Hint System

Design **just-in-time teaching** for ongoing learning:

**Hint Trigger Conditions**:

| Trigger | Condition | Hint Type | Example |
|---------|-----------|-----------|---------|
| First encounter | New enemy/object in view | Introduction | "This is a Bomb Plant. It explodes when approached." |
| Struggle detection | N failures in X seconds | Assistance | "Try rolling behind the enemy to avoid fire." |
| Inaction timeout | No input for X seconds | Nudge | "Press [E] to interact with the lever." |
| Suboptimal play | Inefficient strategy detected | Optimization | "Fire attacks deal 2x damage to ice enemies." |
| Discovery moment | First collection/craft | Expansion | "You found Iron! Use it at the forge to craft weapons." |

**Hint Delivery Methods**:

- **UI Overlay**: Text box, arrow indicators, button prompts
- **Diegetic**: Character dialogue, in-world signs, audio logs
- **Environmental**: Level design that forces/encourages specific actions
- **Companion AI**: Helper character that comments and suggests
- **Journal/Codex**: Player-initiated reference, searchable database

**Hint Escalation Ladder**:

```
Level 1: Subtle environmental cue (no text)
Level 2: UI hint appears once
Level 3: Hint repeats after inaction
Level 4: Companion NPC verbal hint
Level 5: Direct instruction with input overlay
Level 6: Auto-complete option offered
```

**Hint Suppression Rules**:

- Don't hint if player recently succeeded with this action
- Don't hint during cutscenes or dialogue
- Don't hint in "challenge zones" (intended difficulty spikes)
- Allow players to disable hints (accessibility)

---

### Phase 5: Retention Optimization

**D1 Retention Hooks** (first day return):

- **Investment**: What have players built/earned that they'll want to return to?
- **Unfinished Business**: What cliffhanger or incomplete goal pulls them back?
- **Scheduled Rewards**: What time-gated content is now available?
- **Social Commitment**: Did they invite friends? Join a guild?

**D7 Retention Hooks** (first week):

- **Progression Milestone**: What major unlock happens around day 5-7?
- **Habit Formation**: What daily loop is now routine?
- **Content Unlock**: What new mode/area opens?
- **Event Participation**: What limited-time event is active?

**D30 Retention Hooks** (first month):

- **Mastery Goal**: What long-term skill/challenge are they working toward?
- **Social Bonds**: Guild relationships, rivalries, cooperation
- **Identity Investment**: Character customization, reputation, collection
- **Endgame Transition**: What happens after "completing" the main content?

**Onboarding Analytics**:

| Metric | Target (Mobile F2P) | Target (PC/Console) |
|--------|---------------------|---------------------|
| Tutorial completion rate | >85% | >95% |
| D1 retention | >40% | >50% |
| D7 retention | >15% | >25% |
| Time to core loop | <2 min | <5 min |
| First failure rate | <30% | <20% |
| Hint skip rate | <50% | <70% |

---

### Phase 6: Documentation

Generate the tutorial design document:

```markdown
# Tutorial & Onboarding Design Document

## Onboarding Philosophy
[Primary approach and rationale]

## First-Time User Experience (FTUE)

### Minute-by-Minute Flow
[0-15 minute detailed breakdown]

### First Session Arc
[Complete first session: hook, loop, complication, closure]

## Progressive Learning Schedule

### Mechanic Dependency Tree
[Prerequisite graph]

### Pacing Table
[Time, mechanic, practice, mastery check]

## Contextual Hint System

### Hint Triggers
[Conditions and responses]

### Delivery Methods
[UI, diegetic, environmental, companion, codex]

### Escalation Ladder
[6-level hint progression]

## Retention Strategy

### D1/D7/D30 Hooks
[Specific retention mechanics]

### Analytics Requirements
[Events to track, targets]

## Accessibility Considerations

### Difficulty Options
[Assist modes, skip options]

### UI/UX Accessibility
[Text size, colorblind modes, input remapping]

## Implementation Checklist

### Phase 1: FTUE
- [ ] Opening sequence
- [ ] First interaction
- [ ] Core loop introduction
- [ ] First complication

### Phase 2: Progressive Unlocks
- [ ] Mechanic dependency tree implemented
- [ ] Pacing schedule followed
- [ ] Mastery checks in place

### Phase 3: Hint System
- [ ] Trigger conditions coded
- [ ] Hint delivery methods implemented
- [ ] Escalation ladder working
- [ ] Suppression rules active

### Phase 4: Analytics
- [ ] Onboarding events tracked
- [ ] Funnel analysis configured
- [ ] A/B testing framework ready
```

---

4. **Save the document** to `design/gdd/tutorial-design.md`.

5. **Create a visual flowchart** (as Mermaid diagram in markdown) at
   `design/gdd/tutorial-flow.md` showing the FTUE progression.

6. **Suggest next steps**:
   - "Review with `ux-designer` agent for usability validation"
   - "Review with `game-designer` agent for pacing and difficulty curve"
   - "Implement FTUE prototype with `/prototype tutorial-flow`"
   - "Playtest with `/playtest-report` focusing on first-time players"
   - "Set up analytics tracking with `/analytics-setup` for onboarding funnel"

7. **Output a summary** with:
   - Onboarding philosophy chosen
   - FTUE duration and key beats
   - Number of mechanics taught and pacing
   - Biggest risk (e.g., "tutorial too long", "difficulty spike")
   - File paths
