---
name: narrative-design
description: "Design narrative systems — branching dialogue, story structure, character arcs, world-building. Integrate story with gameplay seamlessly."
argument-hint: "[focus: dialogue|characters|world|branching|full]"
user-invocable: true
allowed-tools: Read, Glob, Grep, Write, AskUserQuestion
---

When this skill is invoked:

1. **Parse the argument** for narrative focus area:
   - `dialogue`: Branching dialogue systems, conversation design
   - `characters`: Character development, arcs, relationships
   - `world`: World-building, lore, factions, history
   - `branching`: Narrative branching, choice/consequence systems
   - `full`: Comprehensive narrative design (default)

2. **Check for existing narrative work**:
   - Read `design/gdd/game-concept.md` for story premise and pillars
   - Read `design/gdd/` for existing narrative documents
   - Check `design/narrative/` for character sheets, dialogue trees, lore bibles
   - Read `src/` for existing dialogue/narrative implementations

3. **Run through narrative design phases** interactively, using `AskUserQuestion`
   at key decision points. The goal is **integrated storytelling** — narrative
   that serves gameplay, not separate from it.

---

### Phase 1: Narrative Vision & Scope

**Story Role in Game**:

What role does narrative play in this game? (choose primary)

| Type | Description | Examples |
|------|-------------|----------|
| **Story-Driven** | Narrative is the core product | The Last of Us, Life is Strange |
| **Environmental** | Story through exploration | Dark Souls, BioShock |
| **Ludonarrative** | Story emerges from gameplay | RimWorld, Dwarf Fortress |
| **Framing Device** | Minimal story enables gameplay | Doom, Rocket League |
| **Emergent** | Player creates the story | Minecraft, Sims |

**Narrative Scope**:

- **Story Length**: How many hours of narrative content?
  - Short: 1-3 hours (indie experience)
  - Medium: 5-15 hours (AA game)
  - Long: 20-50+ hours (AAA RPG)

- **Content Volume**:
  - Dialogue lines: ___ (100, 500, 2000+, 10000+)
  - Characters with speaking roles: ___
  - Unique locations with narrative: ___
  - Quests/missions with story: ___

- **Branching Complexity**:
  - Linear: One path, no choices
  - Light branching: Minor choices, same ending
  - Moderate branching: 2-3 major branches, 2-4 endings
  - Heavy branching: Many branches, 6+ endings
  - Living world: Choices persist and compound across game

**Tone & Themes**:

- **Primary emotion**: What should players FEEL? (hope, dread, triumph, melancholy, wonder)
- **Themes**: What ideas does the story explore? (redemption, sacrifice, identity, power, family)
- **Tone consistency**: Consistent throughout, or intentional shifts? (comedy → drama, hope → despair)

**Narrative Pillars** (3-5 guiding principles):

Example from *The Last of Us*:
1. "Relationships are survival" — bonds matter more than skills
2. "Violence has consequences" — physical and emotional cost
3. "The world continues without you" — nature reclaims, life goes on

---

### Phase 2: Character Design

**Protagonist Design**:

| Aspect | Questions |
|--------|-----------|
| **Identity** | Who are they? (age, background, role) |
| **Want** | What do they consciously desire? (goal) |
| **Need** | What do they actually need? (growth arc) |
| **Ghost** | What past wound haunts them? |
| **Lie** | What false belief do they hold? |
| **Truth** | What truth must they learn? |

**Character Arc Type** (choose one):

| Arc Type | Description | Example |
|----------|-------------|---------|
| **Positive Change** | Character grows, overcomes flaw | Luke Skywalker |
| **Negative Change** | Character falls, corrupted | Walter White |
| **Flat Arc** | Character doesn't change, changes world | James Bond, Sherlock |
| **Disillusionment** | Character loses innocence | Frodo Baggins |

**Supporting Cast Design**:

For each major character, define:

```markdown
## [Character Name]

### Role in Story
[Protagonist/antagonist/mentor/ally/trickster/etc.]

### Surface Identity
[What players see first: appearance, mannerisms, public role]

### Deep Structure
[True motivations, secrets, contradictions]

### Relationship to Protagonist
[How they challenge/support the protagonist's arc]

### Character Arc
[How they change (or don't) across the story]

### Signature Elements
[Catchphrases, visual motifs, associated mechanics]

### Voice Profile
[Speech patterns, vocabulary, rhythm, topics they dominate/avoid]
```

**Character Relationship Map**:

Create a web showing:
- Who knows whom
- Alliance/rivalry/romance/family bonds
- Power dynamics (who has leverage over whom)
- Secrets (who knows what about whom)
- How relationships change across the story

---

### Phase 3: World-Building

**World Foundation**:

| Element | Questions to Answer |
|---------|---------------------|
| **Physical** | Geography, climate, resources, travel methods |
| **Social** | Classes, factions, power structures, laws |
| **Economic** | Currency, trade, scarcity, technology level |
| **Cultural** | Religion, art, customs, taboos, holidays |
| **Historical** | Key events, wars, disasters, golden ages |
| **Metaphysical** | Magic system, gods, afterlife, cosmology |

**The Iceberg Method**:

- **10% Visible**: What players directly experience (dialogue, cutscenes, explorable areas)
- **90% Hidden**: Lore documents, backstory, systems that explain the visible

**Faction Design**:

For each major faction:

```markdown
## [Faction Name]

### Public Identity
[What they claim to stand for]

### True Purpose
[What they actually do/stand for]

### Power Base
[Where their power comes from: military, wealth, knowledge, faith]

### Leadership
[Who leads, how succession works]

### Membership
[How one joins, ranks within faction]

### Resources
[What they control: territory, wealth, artifacts, information]

### Relationships
[Allies, enemies, neutrals, internal factions]

### Quest Hooks
[Why the player interacts with them]
```

**Lore Delivery Methods**:

| Method | Intrusiveness | Player Choice | Best For |
|--------|---------------|---------------|----------|
| **Cutscene** | High (forced) | None | Critical story beats |
| **Dialogue** | Medium | Skip option | Character moments |
| **Audio Log** | Low | Optional pickup | Environmental story |
| **Item Description** | Very low | Read or ignore | Deep lore for interested |
| **Environmental** | Passive | Notice or miss | Show-don't-tell |
| **Codex Entry** | Player-initiated | Seek out | Reference material |

---

### Phase 4: Branching Dialogue System

**Dialogue Structure**:

```
[Conversation Start]
       ↓
[Player chooses response A/B/C]
       ↓
[NPC reacts + may branch further]
       ↓
[Consequence: relationship change, quest update, unlock/lock options]
       ↓
[Conversation continues or ends]
```

**Branch Types**:

| Type | Description | Complexity |
|------|-------------|------------|
| **Illusion of Choice** | All paths converge quickly | Low |
| **Delayed Consequence** | Choice matters much later | Medium |
| **Immediate Consequence** | Choice changes next scene | Medium |
| **Stateful Branching** | Choice affects world state | High |
| **Flag-Based** | Multiple choices accumulate flags | High |
| **Web Structure** | Many interlocking branches | Very High |

**Dialogue Line Format** (for implementation):

```json
{
  "id": "conv_tavernkeeper_greeting",
  "speaker": "tavernkeeper_martha",
  "text": "Welcome to the Rusty Anchor, stranger. You look like you've seen some miles.",
  
  "conditions": [
    {"flag": "met_martha_before", "op": "!=", "value": true},
    {"time_of_day": "evening"}
  ],
  
  "responses": [
    {
      "id": "resp_a",
      "text": "Just passing through. Got a room?",
      "next_node": "room_available",
      "requirements": []
    },
    {
      "id": "resp_b", 
      "text": "Looking for information about the lighthouse.",
      "next_node": "lighthouse_warning",
      "requirements": [{"quest": "lighthouse_mystery", "state": "active"}]
    },
    {
      "id": "resp_c",
      "text": "[Flirt] For you, I'd travel a few more.",
      "next_node": "martha_flattered",
      "requirements": [{"relationship": "martha", "value": ">=", "threshold": 30}]
    }
  ],
  
  "effects": [
    {"relationship": "martha", "change": "+5", "if_response": "resp_c"}
  ]
}
```

**Conversation Design Principles**:

- **Three-beat rule**: Important information should appear 3 times before player must act
- **Fail-forward**: Failed checks create new paths, not dead ends
- **Player fantasy**: Responses should let player express character identity
- **Pacing**: Mix exposition with choices, don't info-dump
- **Subtext**: What characters DON'T say is as important as what they do

**Choice Architecture**:

| Choice Type | Player Question | Example |
|-------------|-----------------|---------|
| **Tactical** | "How do I approach this?" | [Lie] / [Tell truth] / [Deflect] |
| **Moral** | "What kind of person am I?" | [Save villager] / [Pursue villain] |
| **Strategic** | "What's my long-term goal?" | [Ally with mages] / [Ally with templars] |
| **Expressive** | "How do I feel?" | [Joke] / [Comfort] / [Anger] |
| **Information** | "What do I want to know?" | [Ask about past] / [Ask about goal] / [Ask about obstacle] |

---

### Phase 5: Quest/Narrative Mission Design

**Quest Structure**:

```markdown
## [Quest Name]

### Logline
[One sentence: "A [role] must [goal] before [stakes]."]

### Prerequisites
[What must be complete before this quest unlocks]

### Act Structure
| Act | Beats | Player Objectives |
|-----|-------|-------------------|
| Setup | Inciting incident, call to action | Talk to NPC, learn the problem |
| Confrontation | Rising action, complications | Gather resources, face obstacles |
| Climax | Final challenge, choice point | Boss fight, moral decision |
| Resolution | Aftermath, rewards | Collect reward, see consequences |

### Branching Points
[Where player choices change outcomes]

### State Changes
[What flags/variables this quest sets]

### Follow-Ups
[What quests this unlocks or modifies]
```

**Quest Types**:

| Type | Purpose | Structure |
|------|---------|-----------|
| **Story Quest** | Advance main narrative | Linear, mandatory |
| **Character Quest** | Develop companion arcs | Branching, optional |
| **Faction Quest** | Explore faction lore | Multi-stage, reputation-based |
| **Side Quest** | World-building, rewards | Self-contained, optional |
| **Radiant Quest** | Replayable content | Procedural, repeatable |
| **Fetch Quest** | Gate progression, teach mechanics | Simple, often tutorial |

**Narrative Pacing**:

Map emotional intensity across the game:
```
Intensity:  Low → High → Low → High → Peak → Resolution
            ↑      ↑      ↑      ↑       ↑        ↑
         Intro  First  Valley  Mid   Climax  Epilogue
                boss           boss
```

---

### Phase 6: Documentation

Generate the narrative design document:

```markdown
# Narrative Design Document

## Executive Summary
[Story premise, tone, themes in one paragraph]

## Narrative Vision
[Role of story, scope, pillars]

## Characters

### Protagonist(s)
[Identity, want, need, ghost, lie, truth, arc type]

### Supporting Cast
[Character sheets for each major character]

### Relationship Map
[Visual or table showing connections]

## World-Building

### World Foundation
[Physical, social, economic, cultural, historical, metaphysical]

### Factions
[Faction sheets for each major group]

### Lore Delivery Plan
[What story is told how: cutscenes, dialogue, environment, etc.]

## Story Structure

### Main Story Beats
[Act-by-act breakdown of the critical path]

### Quest List
| Quest | Type | Location | NPCs | Rewards | Branching |
|-------|------|----------|------|---------|-----------|

## Dialogue Systems

### Conversation Format
[JSON/schema for dialogue implementation]

### Branching Rules
[How choices work, consequence tracking]

### Key Conversations
[Script samples for important scenes]

## Implementation Guidelines

### Writing Style Guide
[Voice, tone, formatting standards]

### Localization Notes
[Text that may be hard to translate, cultural considerations]

### Technical Requirements
[Dialogue system features, save/load needs, UI requirements]

## Content Checklist

### Written Content
- [ ] Main story dialogue: ___ lines
- [ ] Side quest dialogue: ___ lines  
- [ ] Barks/combat lines: ___ lines
- [ ] Item descriptions: ___ items
- [ ] Lore documents: ___ documents
- [ ] UI text: menus, tutorials, hints

### Production Status
| Quest/Scene | Draft | Review | VO Record | Implementation | QA |
|-------------|-------|--------|-----------|----------------|-----|
```

---

4. **Save the document** to `design/gdd/narrative-design.md`.

5. **Create character sheets** in `design/narrative/characters/` for each major
   character (one markdown file per character).

6. **Create a dialogue template** at `design/narrative/templates/dialogue-node.json`
   with the JSON schema for implementation.

7. **Suggest next steps**:
   - "Review with `narrative-director` agent for story consistency"
   - "Review with `writer` agent for dialogue quality and voice"
   - "Review with `world-builder` agent for lore consistency"
   - "Create sample dialogue tree with `/prototype dialogue-system`"
   - "Run `/design-review design/gdd/narrative-design.md` for completeness"

8. **Output a summary** with:
   - Narrative type and scope
   - Number of major characters and factions
   - Branching complexity level
   - Estimated dialogue lines and content volume
   - Biggest risk (e.g., "scope too large", "branching unmanageable")
   - File paths
