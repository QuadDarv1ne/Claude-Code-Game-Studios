# Example: Narrative Design Workflow

This example demonstrates how to use `/narrative-design` to create a branching
dialogue system and character arc for an RPG.

## Context

**Game:** "The Last Covenant" — narrative-driven RPG  
**Platform:** PC + Console  
**Narrative Type:** Story-driven with branching dialogue  
**Goal:** Design companion character with meaningful relationship arc

---

## Session Transcript

### Step 1: Invoke the Skill

```
/narrative-design characters
```

### Step 2: Narrative Vision

The skill asks about story role:

> **Q:** What role does narrative play in this game?
>
> **A:** Story-Driven — narrative is the core product.

> **Q:** Primary emotion players should feel?
>
> **A:** Melancholy hope — bittersweet journey with meaningful connections.

> **Q:** Themes?
>
> **A:** Redemption, sacrifice, found family.

### Step 3: Character Design

The skill designs a companion character:

**Character: Elena, the Fallen Paladin**

| Aspect | Details |
|--------|---------|
| **Identity** | 35, former order leader, disgraced |
| **Want** | Restore her honor |
| **Need** | Forgive herself |
| **Ghost** | Failed to save her squad |
| **Lie** | "I don't deserve redemption" |
| **Truth** | "Redemption is earned through action, not the past" |

**Character Arc Type:** Positive Change (redemption arc)

### Step 4: Relationship System

The skill designs relationship progression:

```
Relationship Levels:
1. Stranger (0-20)   — Cold, professional
2. Acquaintance (21-40) — Guarded openness
3. Friend (41-60)   — Shares personal stories
4. Confidant (61-80) — Reveals her ghost
5. Bonded (81-100)  — Accepts redemption, unique ending
```

**Relationship Actions:**
| Action | Points | Trigger |
|--------|--------|---------|
| Support her decision | +5 | Dialogue choice |
| Complete her quest | +15 | Quest complete |
| Give her artifact | +10 | Gift |
| Contradict in public | -5 | Dialogue choice |

### Step 5: Branching Dialogue

The skill creates a dialogue tree:

**Node: START — Meeting Elena**

```
Speaker: Elena
Text: "You're the one they call the Covenant Bearer? I expected... more."

Responses:
  A: "And you're the disgraced Elena. How the mighty fall." [Sarcastic]
     → node_cold (relationship: -5)
  
  B: "I'm just trying to help. Maybe we can work together?" [Friendly]
     → node_warm (relationship: +5)
  
  C: "Your reputation precedes you. I'd hear your story." [Neutral]
     → node_neutral (relationship: 0)
  
  [LEAVE]: "Never mind."
     → END
```

**Node: node_warm — Elena responds warmly**

```
Speaker: Elena
Text: "Work together? You'd trust a fallen paladin?"
Emotion: Surprised, guarded

Responses:
  A: "Everyone deserves a second chance."
     → node_second_chance (relationship: +10, unlocks quest)
  
  B: "I judge people by their actions, not their past."
     → node_actions (relationship: +5)
```

### Step 6: Quest Integration

The skill integrates dialogue with quests:

**Quest: "The Weight of Honor"**

| Stage | Dialogue Trigger | Relationship Required |
|-------|------------------|----------------------|
| Start | Elena mentions her past | 20+ (Acquaintance) |
| Middle | She reveals her ghost | 40+ (Friend) |
| Climax | Redemption choice | 60+ (Confidant) |
| Ending | Unique based on relationship | 80+ = bonded ending |

### Step 7: Output Files

The skill creates:

1. `design/gdd/narrative-design.md` — full narrative design
2. `design/narrative/characters/elena.md` — character sheet
3. `design/narrative/dialogue/elena_first_meeting.json` — dialogue tree JSON

---

## Output: narrative-design.md (excerpt)

```markdown
# Narrative Design Document

## Executive Summary
The Last Covenant is a story-driven RPG about redemption and found family.
Players build relationships with companions through branching dialogue
and shared experiences.

## Characters

### Elena, the Fallen Paladin
- **Arc:** Positive Change (redemption)
- **Want:** Restore honor
- **Need:** Self-forgiveness
- **Ghost:** Failed to save her squad

## Relationship System
5-tier relationship with companions affecting:
- Dialogue options
- Combat support
- Quest outcomes
- Ending variations

## Dialogue System
Branching structure with:
- Relationship gates
- Flag-based consequences
- Quest integration
```

---

## Output: elena.md (character sheet excerpt)

```markdown
# Elena — Character Sheet

## Surface Identity
Armored paladin, scarred, cold demeanor, speaks formally

## Deep Structure
Guilt-ridden, protective of innocents, secretly yearns for connection

## Voice Profile
- Formal speech patterns ("I shall," "We must")
- Avoids talking about her past
- Becomes warmer at high relationship

## Key Moments
1. First meeting — guarded hostility
2. Campfire scene — shares ghost story (40+ relationship)
3. Redemption choice — forgive herself or fall (60+ relationship)
4. Ending — bonded or departed (80+ relationship)
```

---

## Output: elena_first_meeting.json (excerpt)

```json
{
  "conversation_id": "elena_first_meeting",
  "npc": "elena",
  "location": "camp_ruins",
  "nodes": {
    "START": {
      "speaker": "elena",
      "text": "You're the one they call the Covenant Bearer? I expected... more.",
      "responses": [
        {
          "id": "A",
          "text": "And you're the disgraced Elena. How the mighty fall.",
          "next_node": "node_cold",
          "effects": [{"relationship": "elena", "change": -5}]
        },
        {
          "id": "B",
          "text": "I'm just trying to help. Maybe we can work together?",
          "next_node": "node_warm",
          "effects": [{"relationship": "elena", "change": 5}]
        }
      ]
    }
  }
}
```

---

## Next Steps

After running `/narrative-design`:

1. **Review with `narrative-director`** — story consistency
2. **Review with `writer`** — dialogue quality and voice
3. **Review with `game-designer`** — quest integration
4. **Create sample dialogue** — `/prototype dialogue-system`
5. **Implement in engine** — dialogue system integration

---

## Key Learnings

- **Character arcs drive engagement** — players care about growth
- **Relationship systems** — quantify emotional connections
- **Branching dialogue** — choices must have meaningful consequences
- **Ludonarrative harmony** — gameplay and story reinforce each other
- **Voice consistency** — each character has distinct speech patterns

---

*This example shows how `/narrative-design` creates character sheets, relationship
systems, and branching dialogue trees ready for implementation.*
