---
layout: page
permalink: /ETMEditorTutorials/ETMEditorTutorial_Level_Detail_Tab/
title: Level Crafting
description: Create a Level
date: 2025-01-22 19:02:46 -0000
last_modified_at: 2026-09-13 12:00:00 -0000
publish: true
pin: false
categories: [Apps]
tags: [Games]
---

![Detail Screen](/assets/ETMEditor/DetailMain.jpg)

The Level Detail screen is the main workspace where you design and edit your dungeon levels. This screen provides all the tools you need to create intricate maze layouts, place monsters and items, configure triggers, and fine-tune every aspect of your dungeon.

## Interface Overview

The Level Detail screen is divided into three main areas:

1. **Drawing Area** (left): Visual representation of your level
2. **Edit Modes Panel** (right): Switch between settings, drawing, triggers, game items and monsters
3. **Header** (top): Navigation and utility buttons

## Drawing Area

The drawing area on the left displays your current level in a top-down view. This is where you can:

- **View your entire level layout** at a glance — the map is scaled to fit when a level opens
- **Select individual tiles** by tapping them (in Paint Mode a tap paints instead, see below)
- **Zoom** with a pinch gesture or the magnifier buttons in the header, and scroll the map when it is larger than the screen
- **See visual indicators** showing monsters, game items, triggers, ... based on the current edit mode

### Mode-Specific Indicators

Depending on which edit mode you have active, the drawing area displays different visual markers. The selected tile is always outlined in red.

- **Level Settings**: Shows everything at once — monsters (red **M**), tiles holding game items (yellow) and trigger targets (green)
- **Tile Mode**: Outlines the targets of all triggers in green; the targets of the selected tile's own triggers get a thick green outline. On the textures tab, tiles carrying a wall text are outlined in blue
- **Paint Mode**: Shows only the tiles, so you see what you paint
- **Monster Mode**: Marks tiles containing monsters with a red **M**
- **Item Mode**: Outlines tiles containing game items in yellow, and marks monsters

### Coordinate Display

Enable the coordinate display using the **X/Y** button in the header to show grid coordinates. This is particularly useful when:
- Setting up trigger actions that target specific tiles
- Documenting your level design
- Troubleshooting complex trigger chains

## Edit Modes

![Detail Tabs](/assets/ETMEditor/DetailIcons.jpg)

The right panel contains five different edit modes, each providing specialized tools for different aspects of level design:

### 1. Level Settings & Maze Generator

![Level Icon](/assets/ETMEditor/DetailLevel.jpg)

Configure basic level properties and use the maze generator.

[View Level Settings Tutorial](/ETMEditorTutorials/ETMEditorTutorial_Level_Settings_Tab)

### 2. Tile Editor
![Tile Icon](/assets/ETMEditor/DetailTile.jpg)

Place and configure individual tiles, set up triggers and actions.

[View Tiles, Triggers and Actions Tutorial](/ETMEditorTutorials/ETMEditorTutorial_Level_Tile_Tab)

### 3. Paint Mode
![Paint Icon](/assets/ETMEditor/DetailPaintSmall.jpg)

Quickly paint tiles using a tile palette for efficient level building.

[View Tile Paint Tutorial](/ETMEditorTutorials/ETMEditorTutorial_Level_Paint_Tab)

### 4. Monster Placement
![Monster Icon](/assets/ETMEditor/DetailMonster.jpg)

Add monsters to your level and configure their behavior.

[View Add Monsters Tutorial](/ETMEditorTutorials/ETMEditorTutorial_Level_Monster_Tab)

### 5. Item Placement
![Items Icon](/assets/ETMEditor/DetailItems4.jpg)

Place game items like keys, potions, weapons, and treasure throughout your dungeon.

[View Add GameItems Tutorial](/ETMEditorTutorials/ETMEditorTutorial_Level_Item_Tab)

## Header Controls

![Header Buttons](/assets/ETMEditor/DetailMenuButtons.jpg)

The header contains essential navigation and utility buttons:

### Back
Returns to the level pack screen. Your edits are kept; the level pack screen asks whether to save them when you leave it.

### Zoom In / Zoom Out
Scale the map up or down. You can also pinch the map directly.

### X/Y Coordinate Toggle
Shows or hides the column/row numbers on every tile of the drawing area. This is essential when working with triggers and actions that target specific tile positions.

### Revert Button (✕)
Discards all changes made since the level editor was opened or since the last save, and stays in the editor. Use this if you want to abandon your current edits.

**Warning**: All unsaved changes to the whole level pack will be lost when you revert.

### Save Button
Saves the level pack. Always save your work regularly to avoid losing progress.

**Best Practice**: Save frequently, especially after completing major changes or adding complex trigger systems.

### Help (?)
Opens the tutorial page for the edit mode you are currently in.

## Workflow Tips

Here are some recommended workflows for building effective dungeon levels:

### Starting a New Level
1. Use **Level Settings** to configure dimensions and basic properties
2. Switch to **Paint Mode** to lay out the basic maze structure
3. Add **Tiles** with special properties (doors, switches, pits)
4. Place **Monsters** at strategic locations
5. Add **Items** for players to discover
6. Set up **Triggers and Actions** for puzzles and traps
7. **Save** your work regularly

<hr>
**[Back to Tutorial Overview](/ETMEditorTutorials/ETMEditorTutorials)**

