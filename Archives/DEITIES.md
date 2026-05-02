# Deities — Reputation & Favor System

> **Related**:
> [QUESTS.md](./QUESTS.md),
> [RULES.md](../param/rules/RULES.md)

## Overview

**The Grand Architect** ("Le Grand Architecte") — supreme deity above Kael, Erya, and Toran.

Three deities: **Kael** (war), **Erya** (knowledge), **Toran** (prosperity).  
Players build reputation and favor with each deity through quest rewards.  
One deity can be chosen as "allegiance" (unlocks deity-specific quests).

## Database

### `player_deity` Table

| Column | Type | Description |
|---|---|---|
| `player_id` | `VARCHAR(36) FK→players` | Owner |
| `deity` | `ENUM('kael','erya','toran')` | Deity ID |
| `is_allegiance` | `TINYINT DEFAULT 0` | 0=none, 1=allegiance |
| `allegiance_share` | `TINYINT DEFAULT 0` | 0, 50 or 100 (% of gained rep) |
| `reputation` | `INT DEFAULT 0` | Decreases over time |
| `favor` | `INT DEFAULT 0` | Consumable currency, does not decrease |
| `chosen_at` | `BIGINT NULL` | Timestamp of allegiance choice |

**Primary key**: `(player_id, deity)`  
**3 rows per player** (one per deity).

### Allegiance System

- **Single allegiance**: 1 row with `is_allegiance=1`, `allegiance_share=100`
- **Double allegiance**: 2 rows with `is_allegiance=1`, `allegiance_share=50` each

### `cities` Table — Sanctuaries

```sql
ALTER TABLE cities ADD COLUMN sanctuary_deity_primary ENUM('kael','erya','toran') NULL;
ALTER TABLE cities ADD COLUMN sanctuary_deity_secondary ENUM('kael','erya','toran') NULL;
```

Only **one sanctuary per player** (enforced application-side).

## Mechanics

### Reputation

- **Gain**: Awarded on quest claim (separate from resources)
- **Decay**: -0.5% per day (IRL), checked in `turn_manager`
- **Benefits**: Unlocks titles, access to miracles

### Favor

- **Gain**: Awarded on quest claim (separate from reputation)
- **Consumption**: Used for miracles/blessings
- **No decay**

### Sanctuaries

- Designated when player chooses allegiance
- Loss triggers reputation penalty hook (in city destruction handler)
- Primary + secondary deity allowed (for double allegiance)

### Miracles & Blessings

- Invoke via `INVOKE_BLESSING` handler
- Costs favor
- Effects defined in XML (`blessings.xml`)

## Integration Points

| File | Change |
|---|---|
| `common/includes/sql_objects/` | +`deity.php` BDDObject |
| `common/quests/quest_system.php` | +distribution of rep/favor on claim |
| `game/turn_manager.php` | +reputation decay logic |
| `www/includes/request_manager.php` | +`CHOOSE_DEITY`, `INVOKE_BLESSING` |

## Quest Rewards — Extended

XML `<rewards>` now supports:

```xml
<rewards>
    <resource name="gold" count="100"/>
    <reputation deity="kael" amount="50"/>
    <favor deity="erya" amount="25"/>
</rewards>
```

## Phases

| Phase | Features |
|---|---|
| 2 | Light divine quests (neutral), repeatable quests, rep/favor distribution |
| 3 | Allegiance choice, sanctuaries, miracles |
| 4 | End-game (out of scope) |

## Open Questions (to be decided before Phase 2)

| Question | Recommendation | Status |
|---|---|---|
| Cooldown par défaut des quêtes répétables | 288 TICs (≈24h IRL) | ? |
| Taux décroissance réputation | 0.5%/jour IRL | ? |
| La faveur diminue-t-elle ? | Non (sinon double pénalité) | ? |
| Bâtiments T2 existants ? | À vérifier dans buildings.xml | ?