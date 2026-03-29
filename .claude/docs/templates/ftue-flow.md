# FTUE Flow (First-Time User Experience)

## Overview

**Game:** [Game Name]  
**Version:** [Version]  
**Date:** [Date]  
**Author:** [Author]

---

## Design Goals

### Emotional Targets

| Time | Target Emotion | How |
|------|---------------|-----|
| 0-60 seconds | | |
| 1-5 minutes | | |
| 5-15 minutes | | |
| End of session | | |

### Learning Objectives

What must players learn in their first session?

1. 
2. 
3. 

---

## Minute-by-Minute Flow

### 0:00 - 1:00 (First 60 Seconds)

| Second | Screen | Player Action | System Response | Feedback |
|--------|--------|---------------|-----------------|----------|
| 0-10 | | | | |
| 10-30 | | | | |
| 30-60 | | | | |

**Goal:** 

**Success Metric:** % of players reach first interaction

---

### 1:00 - 3:00 (First Verb)

| Step | Mechanic | Teaching Method | Success Criteria |
|------|----------|-----------------|------------------|
| 1 | | | |
| 2 | | | |
| 3 | | | |

**Goal:** 

**Success Metric:** % complete first verb successfully

---

### 3:00 - 7:00 (Core Loop Introduction)

| Loop Iteration | Objective | Time Target | Rewards |
|----------------|-----------|-------------|---------|
| 1 | | <60 sec | |
| 2 | | <60 sec | |
| 3 | | <60 sec | |

**Goal:** 

**Success Metric:** % complete 3 full loops

---

### 7:00 - 15:00 (First Complication)

| Complication | Introduction Method | Player Tools | Expected Outcome |
|--------------|---------------------|--------------|------------------|
| | | | |

**Goal:** 

**Success Metric:** % overcome complication without quitting

---

## First Session Closure

### Natural Stopping Point

- **Trigger:** 
- **Message:** 
- **Save Point:** 

### Progression Saved

| Element | Value |
|---------|-------|
| Level/Stage | |
| Items Earned | |
| Unlocks | |
| Currency | |

### Return Hook

| Hook Type | Description | Available At |
|-----------|-------------|--------------|
| Energy Regen | | |
| Daily Reward | | |
| Story Cliffhanger | | |
| Event Timer | | |

---

## Tutorial Mechanics

### Teaching Methods Used

| Mechanic | Method | Location |
|----------|--------|----------|
| | [Show/Guide/Force/Allow] | |

### Hint System

| Trigger | Hint Type | Content | Escalation |
|---------|-----------|---------|------------|
| First encounter | | | Level 1 → 2 → 3 |
| N failures | | | Level 1 → 2 → 3 |
| Inaction (X sec) | | | Level 1 → 2 |

### Fail States

| Failure Condition | Response | Retry Flow | Learning Aid |
|-------------------|----------|------------|--------------|
| Player dies | | Instant restart | After 2 fails: show tip |
| Player stuck | | | After 30 sec: hint |
| Wrong path | | | Gentle redirect |

---

## Difficulty Curve

### Expected Performance

| Section | Target Success Rate | Avg Time | Deaths/Fails |
|---------|--------------------|----------|--------------|
| Intro | 100% | | 0 |
| First Verb | 90% | | 0-1 |
| Core Loop | 80% | | 1-2 |
| Complication | 60% | | 2-3 |
| Session End | 80% | | 0-1 |

### Adaptive Difficulty (if applicable)

| Condition | Adjustment |
|-----------|------------|
| 3+ fails in 2 min | Reduce enemy HP by 20% |
| No damage taken | Increase challenge |
| Stuck >60 sec | Spawn hint NPC |

---

## Accessibility Options

### FTUE-Specific Settings

| Option | Default | Alternatives |
|--------|---------|--------------|
| Tutorial Length | Standard | Short / Extended |
| Hint Frequency | Normal | Minimal / Frequent |
| Input Assistance | On | Off / Enhanced |
| Time Pressure | Normal | Relaxed / Removed |

### Skip Options

| Skippable? | Conditions | Consequences |
|------------|------------|--------------|
| [Yes/No] | | [Lock out feature / Show summary] |

---

## Analytics Events

### Funnel Tracking

| Event | Trigger | Required Fields |
|-------|---------|-----------------|
| `ftue_started` | Game launched | session_id, build |
| `ftue_step_complete` | Each step | step_id, duration |
| `ftue_first_verb` | First action | verb_type, success |
| `ftue_core_loop` | Loop complete | loop_count, time |
| `ftue_complete` | Session end | total_time, failures |
| `ftue_quit` | Early exit | quit_point, reason |

### Success Metrics

| Metric | Target | Current |
|--------|--------|---------|
| Tutorial Start → First Verb | >90% | |
| First Verb → Core Loop | >80% | |
| Core Loop → Complication | >70% | |
| FTUE Completion Rate | >60% | |
| D1 Retention (FTUE complete) | >45% | |
| D1 Retention (FTUE quit) | <20% | |

---

## Content Checklist

### Assets Required

| Asset | Type | Status | Due |
|-------|------|--------|-----|
| | [Art/Audio/Code/Design] | | |

### Scripts Required

| Dialogue/Script | Character | VO Required? |
|-----------------|-----------|--------------|
| | | [Yes/No] |

### UI Screens

| Screen | Purpose | Mockup |
|--------|---------|--------|
| | | |

---

## Risks & Mitigations

| Risk | Probability | Impact | Mitigation |
|------|------------|--------|------------|
| Tutorial too long | | | Add skip option |
| Difficulty spike | | | Adaptive tuning |
| Confusing objective | | | Better signposting |
| Technical issues | | | Fallback path |

---

## Playtest Plan

### Test Goals

1. 
2. 
3. 

### Recruitment

| Player Type | Count | Criteria |
|-------------|-------|----------|
| Genre新手 | 5 | Never played [genre] |
| Genre veteran | 5 | 100+ hours in [similar game] |
| Target audience | 5 | [demographic] |

### Data Collection

- [ ] Screen recording
- [ ] Think-aloud protocol
- [ ] Post-session survey
- [ ] Analytics review

### Success Criteria

- Players understand core verb within 2 minutes
- Players complete first loop without external help
- Players can articulate what to do next at each step
- D1 retention target: >%

---

*Template for FTUE design. Complete before implementation begins.*
