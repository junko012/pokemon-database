# Pokemon.db Schema Reference

## Species

Stores Pokémon species metadata and base stats.

| Column         | Type                |
| -------------- | ------------------- |
| SpeciesId      | INTEGER PRIMARY KEY |
| Name           | TEXT                |
| Height         | REAL                |
| Weight         | REAL                |
| GrowthRate     | TEXT                |
| CaptureRate    | INTEGER             |
| BaseExperience | INTEGER             |
| GenderRate     | INTEGER             |
| Habitat        | TEXT                |
| Color          | TEXT                |
| Shape          | TEXT                |
| BaseHP         | INTEGER             |
| BaseAttack     | INTEGER             |
| BaseDefense    | INTEGER             |
| BaseSpAttack   | INTEGER             |
| BaseSpDefense  | INTEGER             |
| BaseSpeed      | INTEGER             |

---

## SpeciesTypes

Stores Pokémon typing.

| Column    | Type    |
| --------- | ------- |
| SpeciesId | INTEGER |
| Slot      | INTEGER |
| TypeName  | TEXT    |

Primary Key:

```text
(SpeciesId, Slot)
```

---

## SpeciesAbilities

Stores Pokémon abilities.

| Column      | Type    |
| ----------- | ------- |
| SpeciesId   | INTEGER |
| AbilityName | TEXT    |
| IsHidden    | INTEGER |

Primary Key:

```text
(SpeciesId, AbilityName)
```

---

## Moves

Stores move metadata.

| Column      | Type                |
| ----------- | ------------------- |
| MoveId      | INTEGER PRIMARY KEY |
| Name        | TEXT                |
| TypeName    | TEXT                |
| DamageClass | TEXT                |
| Power       | INTEGER             |
| Accuracy    | INTEGER             |
| PP          | INTEGER             |
| Priority    | INTEGER             |
| EffectText  | TEXT                |
| Target      | TEXT                |
| Generation  | TEXT                |

---

## Abilities

Stores ability metadata.

| Column          | Type                |
| --------------- | ------------------- |
| AbilityId       | INTEGER PRIMARY KEY |
| Name            | TEXT                |
| Description     | TEXT                |
| LongDescription | TEXT                |
| Generation      | TEXT                |
| IsMainSeries    | INTEGER             |

---

## Items

Stores item metadata.

| Column      | Type                |
| ----------- | ------------------- |
| ItemId      | INTEGER PRIMARY KEY |
| Name        | TEXT                |
| Description | TEXT                |
| Category    | TEXT                |
| Cost        | INTEGER             |
| FlingPower  | INTEGER             |
| FlingEffect | TEXT                |

---

## TypeEffectiveness

Stores battle effectiveness multipliers.

| Column      | Type |
| ----------- | ---- |
| AttackType  | TEXT |
| DefenseType | TEXT |
| Multiplier  | REAL |

Primary Key:

```text
(AttackType, DefenseType)
```

---

## Games

Stores game identifiers.

| Column   | Type                |
| -------- | ------------------- |
| GameId   | INTEGER PRIMARY KEY |
| GameCode | TEXT UNIQUE         |

Examples:

```text
redgreen
yellow
crystal
emerald
platinum
blackwhite
scarletviolet
```

---

## Learnsets

Stores move acquisition data.

| Column      | Type    |
| ----------- | ------- |
| SpeciesId   | INTEGER |
| FormId      | INTEGER |
| GameId      | INTEGER |
| MoveId      | INTEGER |
| LearnMethod | TEXT    |
| LearnLevel  | INTEGER |
| LearnItem   | TEXT    |

Primary Key:

```text
SpeciesId
FormId
GameId
MoveId
LearnMethod
```

Indexes:

```text
IX_Learnsets_Species
IX_Learnsets_Move
```

---

## EvolutionChains

Stores evolution relationships.

| Column        | Type                              |
| ------------- | --------------------------------- |
| EvolutionId   | INTEGER PRIMARY KEY AUTOINCREMENT |
| FromSpeciesId | INTEGER                           |
| ToSpeciesId   | INTEGER                           |

Example:

```text
1 -> 2
2 -> 3
```

---

## EvolutionConditions

Stores evolution requirements.

| Column         | Type                              |
| -------------- | --------------------------------- |
| ConditionId    | INTEGER PRIMARY KEY AUTOINCREMENT |
| EvolutionId    | INTEGER                           |
| ConditionType  | TEXT                              |
| ConditionValue | TEXT                              |

Examples:

```text
min_level = 16
item = thunder-stone
trigger = trade
time_of_day = night
```

---

## Metadata

Stores database metadata.

| Column | Type             |
| ------ | ---------------- |
| Key    | TEXT PRIMARY KEY |
| Value  | TEXT             |

Suggested keys:

```text
SchemaVersion
DataVersion
BuildDate
BuilderVersion
```

---

# Entity Relationship Summary

```text
Species
├── SpeciesTypes
├── SpeciesAbilities
├── Learnsets
└── EvolutionChains

Moves
└── Learnsets

Games
└── Learnsets

EvolutionChains
└── EvolutionConditions
```

---

# Schema Version

```text
SchemaVersion: 1
```

# Database Engine

```text
SQLite 3
```

