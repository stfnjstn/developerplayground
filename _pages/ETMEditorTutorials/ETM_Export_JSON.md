---
layout: page
permalink: /ETMEditorTutorials/ETM_Export_JSON
title: Escape the Dungeon Maze Level Editor
description: Tutorial aboutcreating own levels for my Dungeon Crawler
date: 2024-12-26
publish: true
pin: false
categories: [Apps]
tags: [Games]
---

# JSON Structure Documentation: Escape The Maze

## Top-Level Structure
- **`heroes`**: An array of objects representing game heroes.
- **`currentLevel`**: An integer indicating the current level of the game.
- **`displayName`**: A string, the name of the game.
- **`id`**: A string, the identifier for the game.
- **`playerPosition`**: An object specifying the player's current position.
- **`levels`**: An array of objects representing individual game levels.

---

## Key Properties

### **Heroes**
Each hero object contains:
- **`id`**: An integer unique to each hero.
- **`hitpoints`, `mana`, `stamina`**: Integers representing the hero's attributes.
- **`hitpointsRemaining`, `manaRemaining`, `staminaRemaining`**: Integers for remaining resources.
- **`positionInTile`**: An integer indicating the hero's position within a tile.

---

### **Player Position**
- **`row`**: An integer specifying the row in the game grid.
- **`col`**: An integer specifying the column in the game grid.

---

### **Levels**
Each level object contains:
- **`displayName`**: A string, the name of the level.
- **`monsterGroups`**: An object where each key is a unique identifier, and the value is an object describing a monster group.
- **`id`**: A string, the identifier for the level.
- **`cols`**: An integer specifying the number of columns in the grid.
- **`tileObjects`**: A 2D array of objects representing tiles in the game grid.

---

### **Monster Groups**
Each monster group object contains:
- **`id`**: A string identifier for the monster group.
- **`homePosition`**: An object with `row` and `col` keys for the group's home position.
- **`behavior`**: An integer representing behavior type.
- **`position`**: Similar to `homePosition`, indicates the current position.
- **`monsters`**: An object where each key is a monster ID, and the value describes the monster.

---

### **Monsters**
Each monster object contains:
- **`id`**: A string, the monster's unique ID.
- **`monsterClassID`**: A string, identifying the class of the monster.
- **`hitpointsRemaining`**: An integer, remaining hit points.
- **`positionInTile`**: An integer, the monster's position in the tile.
- **`monsterGroupID`**: A string, the group ID to which the monster belongs.

---

### **Tile Objects**
Each tile object contains:
- **`position`**: An object with `row` and `col` keys specifying the tile's position.
- **`blockType`**: An integer indicating the type of block.
- **`tileStatus`, `tileVisibleStatus`**: Integers representing the state of the tile.
- **`explored`**: A boolean indicating whether the tile is explored.
- **`direction`, `type`, `orientation`**: Integers for directional or type-related metadata.
- **`triggers`**: An array of objects, each specifying a trigger.

---

### **Triggers**
Each trigger object contains:
- **`trigger`**: An integer, the type of trigger.
- **`targetAction`**: An integer, the action to perform when triggered.
- **`targetPos3D`**: An object with `row`, `col`, and `level` keys for the target's position.
