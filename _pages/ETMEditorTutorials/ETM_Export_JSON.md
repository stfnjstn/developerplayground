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
- **`behavior`**: An integer representing behavior type. Behavior types are:
  - 
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
- **`tileStatus`**: Boolean representing the state of the tile. 0 not active, 1 active
- **`tileVisibleStatus`**: Boolean representing the visibility state of the tile.
- **`explored`**: A boolean indicating whether the tile is explored. Needed to show explored areas in the map.
- **`direction`, `type`, `orientation`**: Integers for directional or type-related metadata.
- **`triggers`**: An array of objects, each specifying a trigger.

Possible Tiles with there integer representation for `blockType`:
- undefined = 0
- free = 1
- wall = 2
- exit = 3
- floorSwitch = 4
- door = 5
- doorSwitch = 6: Door node with a switch to open/close the door
- wallSwitch = 7
- pit = 8
- alcoven = 9
- teleport = 10
- wallWithoutNode = 11 // Used to optimize 3D Scene
- rotatorLeft = 12
- cure = 13
- rotatorRight = 14
- wallFake = 15
- wallMovable = 16
- fountain = 17
- gameWon = 18
- torch = 19
- doorWithKey = 20
- wallWithKey = 21
- timer = 22

---

### **Triggers**
Each trigger object contains:
- **`trigger`**: An integer, the type of trigger.
  - none = 0
  - onEnter = 1
  - onLeave = 2
  - onSwitch = 3
  - onSwitchOn = 4
  - onSwitchOff = 5
  - onEnterLeave = 6
  - onAttacked = 7
  - onGameItemUsed = 8
  - onGameItemDropped = 9
  - onGameItemCollected = 10
  - onMagic = 11
  - onTimer = 12
- **`targetAction`**: An integer, the action to perform when triggered.
  - none = 0
  - teleport = 2
  - openClose = 3
  - case open = 4
  - close = 5
  - hideUnhide = 6
  - hide = 7
  - unhide = 8
  - custom = 9
  - showWallText = 10
  - hideWallText = 11
  - castSpell = 12
  - spawnGameItem = 13
  - spawnMonster = 14
- **`targetPos3D`**: An object with `row`, `col`, and `level` keys for the target's position.
