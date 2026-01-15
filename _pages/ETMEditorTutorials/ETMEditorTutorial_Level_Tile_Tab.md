---
layout: page
permalink: /ETMEditorTutorials/ETMEditorTutorial_Level_Tile_Tab/
title: Tutorial - Tiles, Triggers and Actions
description: Tiles, Triggers and Actions
date: 2025-01-22 19:02:46 -0000
last_modified_at: 2025-01-22 22:16:14 -0000
publish: true
pin: false
categories: [Apps]
tags: [Games]
---



The main concept about adding traps, riddles or other dynamic content in the game is about triggers and actions. You can specify triggers on a tile (depending on the selected tils) and actions on another or the same tile.
For example a _on_enter_ triggered on one tile calls an _open_ action on a door tile.

# Tile Settings

![Tile](/assets/ETMEditor/DetailTile.png) | ![Tile Triggers](/assets/ETMEditor/DetailTileTrigger.png)

In Progress

---

## Triggers

Defines the types of triggers that can activate tile actions in the game. Triggers are events that occur at specific tiles and execute associated actions on the same or another tile.

### Available triggers:
- ***onEnter:***
  Fires when the player enters the tile
- ***onLeave:***
  Fires when the player leaves the tile
- ***onEnterLeave:***
  Fires both when entering AND leaving the tile (combination trigger)
- ***onSwitch:***
  Fires when a switch on the tile is toggled (either on or off)
- ***onSwitchOn:***
  Fires only when a switch on the tile is turned ON
- ***onSwitchOff:***
  Fires only when a switch on the tile is turned OFF
- ***onAttacked:***
  Fires when the tile is attacked by the player
- ***onGameItemUsed:***
  Fires when a game item is used on the tile
- ***onGameItemDropped:***
  Fires when a game item is dropped on the tile
- ***onGameItemCollected:***
  Fires when a game item is collected/picked up from the tile
- ***onMagic:***
  Fires when magic is cast on the tile
- ***onTimer:***
  Fires after a specified timer delay (see timerDelayAvailable)
- ***onChestOpen:***
  Fires when a chest on the tile is opened
- ***onChestClose:***
  Fires when a chest on the tile is closed



### Available Actions: (Actions that can be performed on a tile)
- ***teleport:***
  Teleport action. Hero or game item will be teleported to the target position.
- ***openClose:***
  If the tile is closed, it will be opened. If it is open, it will be closed.
- ***open:***
  Open action. if the tile is closed, it will be opened. If it is open, it remains open. 
- ***close:***
  Close action. if the tile is open, it will be closed. If it is closed, it remains closed.
- ***hideUnhide:***
  If the tile is hidden, it will be unhidden. If it is unhidden, it will be hidden.
- ***hide:***
  Hide action. If the tile is visible, it will be hidden. If it is hidden, it remains hidden.
- ***unhide:***
  Unhide action. If the tile is hidden, it will be unhidden. If it is unhidden, it remains unhidden.
- ***showWallText:***
  Show a text on a wall. Text is specified in the wallText property of the tile.
- ***hideWallText:***
  Hide a text on a wall. Text is specified in the wallText property of the tile.
- ***castSpell:***
  A spell will be cast at the target position. The target psotition, the spell and for some spells like a fireball the direction must be specified 
- ***spawnGameItem:***
  A game item will be spawned at the target position. Target psotion and game must be selected.
- ***spawnMonster:***
  A monster will be spawned at the target position. Target psotion and monster must be selected. Behavior is randomChaseRandom which means the monster is wandering around and chases you if you come too close.
- ***gainExperience:***
  Used to gain some extra experience points, for example if a riddle is completed. You have to specify the experience points which should be added.

**Textures:**
![Tile Textures](/assets/ETMEditor/DetailTileTexture.png)
In Progress

<hr>
**[Back to Tutorial Overview](/ETMEditorTutorials/ETMEditorTutorials)**