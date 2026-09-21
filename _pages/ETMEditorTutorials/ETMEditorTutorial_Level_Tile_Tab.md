---
layout: page
permalink: /ETMEditorTutorials/ETMEditorTutorial_Level_Tile_Tab/
title: Tutorial - Tiles, Triggers and Actions
description: Tiles, Triggers and Actions
date: 2025-01-22 19:02:46 -0000
last_modified_at: 2026-09-13 12:00:00 -0000
publish: true
pin: false
categories: [Apps]
tags: [Games]
---




## Tile Settings

![Tile Settings](/assets/ETMEditor/TileSettings.jpg)

The tile tab has two pages, switched with the gear and the palette icon at the top: the **tile settings and triggers**, and the **textures & wall text** of the tile. Only the settings a tile type supports are shown.

---
### Selected Tile & Position:
Shows the selected tile type and position

![Tile Position](/assets/ETMEditor/TilePos.jpg)

### Orientation
Uses to specify on which side for example a torch, an alcove, a fountain, a switch ... is rendered

![Tile Orientation](/assets/ETMEditor/TileOrientation.jpg)
### ActiveOpen / InactiveClosed state
For example for teleports, switches, pits, torches, ...

![Tile State](/assets/ETMEditor/TileState.jpg)
### Visibility
Is an element like a teleport visible or hidden. Hidden tiles can still be active. So a hidden switch can still teleport you to somewhere else.

![Tile Visibility](/assets/ETMEditor/TileVisibility.jpg)
### Direction
Needed for special tiles like stairs to specify if they go up or down

![Tile Direction](/assets/ETMEditor/TileDirection.jpg)
### Item:
Some tiles like a door with a key lock require the use of a specific item to open them. Tap the key row to pick the item.

![Tile Item](/assets/ETMEditor/TileItem.jpg)

### Torches shadow priority: <span style="background-color: #4CAF50; color: white; padding: 3px 8px; border-radius: 12px; font-size: 0.85em; margin-left: 5px;">R4.4</span>
Torches have a property if they should cast shadows or not. Due to limitations of SceneKit the number of torches casting shadows is limited. The number is calculated during runtime, depending on platform and how modern the device is. You can specify up to 3 torches in the editor with a priority. 
Supported shadow torches per platform: Apple Watch: 0, Apple TV 0-1, Mac, iPhone, iPad: 0-3

![Tile Torch Shadow](/assets/ETMEditor/TileTorchShadowPrio.jpg)

---

## Triggers & Actions

The main concept about adding traps, riddles or other dynamic content in the game is about triggers and actions. Triggers are events that occur at specific tiles and execute associated actions on the same or another tile. The available triggers and actions depend on the selected source and target tile.
For example an _on_enter_ trigger on a floor switch tile calls an _open_ action on a door tile.

The triggers of the selected tile are listed at the bottom of the tile settings. Tap **+** in the list header to add one, tap a trigger to edit it, and swipe it to the left to delete it. The trigger dialog has three parts: the **trigger** (with its extra settings, e.g. the spell for _onMagic_, delay and tick for _onTimer_, the expected item for _onGameItemDropped_), the **target tile** (level, row and column — the level is fixed for _castSpell_), and the **target action**, whose choices depend on the tile at the target position. Confirm with **OK**; **Cancel** leaves the trigger as it was.

![Trigger 1](/assets/ETMEditor/Trigger1.jpg) | ![Trigger 2](/assets/ETMEditor/Trigger2.jpg) | ![Trigger 3](/assets/ETMEditor/Trigger3.jpg) | ![Trigger 4](/assets/ETMEditor/Trigger4.jpg) | ![Trigger 5](/assets/ETMEditor/Trigger5.jpg)

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
  Used to gain some extra experience points, for example if a riddle is completed. You have to specify the experience points which should be added. Keep in mind to deactive the trigger element (a floor switch or whatever). Otherwise the player could level up again and again.

---

## Textures & Wall Text

On some tiles, like doors and wall switches, you can select another 3D model. On other tiles like walls you can select textures per side and/or a wall text; free tiles offer floor and ceiling. Each side is a section with the current texture, a **+** to pick one and a trash button to go back to the default. The wall text field has an eye button that shows or hides the text in the game (a hidden text can be revealed by a _showWallText_ action) and a trash button to clear it.

![Tile Textures](/assets/ETMEditor/TextureDoor.jpg) | ![Tile Textures](/assets/ETMEditor/TextureWall.jpg)

<hr>
**[Back to Tutorial Overview](/ETMEditorTutorials/ETMEditorTutorials)**