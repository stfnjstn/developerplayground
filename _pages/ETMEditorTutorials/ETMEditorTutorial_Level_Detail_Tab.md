---
layout: page
permalink: /ETMEditorTutorials/ETMEditorTutorial_Level_Detail_Tab/
title: Level Crafting
description: Create a Level
date: 2025-01-22 19:02:46 -0000
last_modified_at: 2026-01-28 22:16:14 -0000
publish: true
pin: false
categories: [Apps]
tags: [Games]
---

![Detail Screen](/assets/ETMEditor/DetailMain.png)

The Level Detail screen is the main workspace where you design and edit your dungeon levels. This screen provides all the tools you need to create intricate maze layouts, place monsters and items, configure triggers, and fine-tune every aspect of your dungeon.

## Interface Overview

The Level Detail screen is divided into three main areas:

1. **Drawing Area** (left): Visual representation of your level
2. **Edit Modes Panel** (right): Switch between settings, drawing, triggers, game items and monsters
3. **Header** (top): Navigation and utility buttons

## Drawing Area

The drawing area on the left displays your current level in a top-down view. This is where you can:

- **View your entire level layout** at a glance
- **Select individual tiles** by clicking on them
- **See visual indicators** showing monsters, gamitems, ... based on the current edit mode

### Mode-Specific Indicators

Depending on which edit mode you have active, the drawing area displays different visual markers:

- **Tile Mode**: Shows all tile types and their current state
- **Monster Mode**: Highlights tiles containing monsters
- **Item Mode**: Highlights tiles containing game items
- **Trigger Mode**: Shows tiles with triggers and their action targets

### Coordinate Display

Enable the coordinate display using the **X/Y** button in the header to show grid coordinates. This is particularly useful when:
- Setting up trigger actions that target specific tiles
- Documenting your level design
- Troubleshooting complex trigger chains

## Edit Modes

![Detail Tabs](/assets/ETMEditor/DetailIcons.png)

The right panel contains five different edit modes, each providing specialized tools for different aspects of level design:

### 1. Level Settings & Maze Generator

![Level Icon](/assets/ETMEditor/DetailLevel.png)

Configure basic level properties and use the maze generator.

[View Level Settings Tutorial](/ETMEditorTutorials/ETMEditorTutorial_Level_Settings_Tab)

### 2. Tile Editor
![Tile Icon](/assets/ETMEditor/DetailTile.png)

Place and configure individual tiles, set up triggers and actions.

[View Tiles, Triggers and Actions Tutorial](/ETMEditorTutorials/ETMEditorTutorial_Level_Tile_Tab)

### 3. Paint Mode
![Paint Icon](/assets/ETMEditor/DetailPaintSmall.jpg)

Quickly paint tiles using a tile palette for efficient level building.

[View Tile Paint Tutorial](/ETMEditorTutorials/ETMEditorTutorial_Level_Paint_Tab)

### 4. Monster Placement
![Monster Icon](/assets/ETMEditor/DetailMonster.png)

Add monsters to your level and configure their behavior.

[View Add Monsters Tutorial](/ETMEditorTutorials/ETMEditorTutorial_Level_Monster_Tab)

### 5. Item Placement
![Items Icon](/assets/ETMEditor/DetailItems4.jpg)

Place game items like keys, potions, weapons, and treasure throughout your dungeon.

[View Add GameItems Tutorial](/ETMEditorTutorials/ETMEditorTutorial_Level_Item_Tab)

## Header Controls

![Header Buttons](/assets/ETMEditor/DetailMenuButtons.png)

The header contains essential navigation and utility buttons:

### X/Y Coordinate Toggle
Shows or hides the coordinate grid overlay on the drawing area. This is essential when working with triggers and actions that target specific tile positions.

### Cancel Button
Discards all changes made since the last save and returns to the level pack overview screen. Use this if you want to abandon your current edits.

**Warning**: All unsaved changes will be lost when you cancel.

### Save Button
Saves all changes made to the current level. Always save your work regularly to avoid losing progress.

**Best Practice**: Save frequently, especially after completing major changes or adding complex trigger systems.

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

