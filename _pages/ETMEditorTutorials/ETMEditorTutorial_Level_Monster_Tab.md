---
layout: page
permalink: /ETMEditorTutorials/ETMEditorTutorial_Level_Monster_Tab/
title: Tutorial - Add Monsters to a Level
description: Add Monsters to a Level
date: 2025-01-22 19:02:46 -0000
last_modified_at: 2026-09-13 12:00:00 -0000
publish: true
pin: false
categories: [Apps]
tags: [Games]
---


## Monster Positioning

![Monster positioning](/assets/ETMEditor/DetailMonsterPos.jpg)

You can choose between two placement options:
- **One huge monster** placed in the center of the tile
- **Up to four small monsters** placed in a 4x4 grid 

Switching the placement empties the tile — a centre monster and corner monsters cannot share a tile.

## Add a New Monster

![Monster Selection](/assets/ETMEditor/DetailMonsterSelect0.jpg) | ![Monster Selection Dialog](/assets/ETMEditor/DetailMonsterSelect1.jpg)

To add a monster to your level:
1. Select a tile that allows monsters (such as __empty__, __floor switches__, __closed pits__, etc.)
2. Tap the __Empty__ row of the position you want to fill
3. The monster selection dialog will open, allowing you to choose from available monsters (only small monsters for the corner positions)

A placed monster shows its picture and name, an **info** button that opens its stats, spells and inventory, a **trash** button that removes it, and its skill level stepper.

## Monster Behaviours

![Monster behaviour](/assets/ETMEditor/DetailMonsterBehavior.jpg)

Choose how your monster behaves in the dungeon. The behaviour belongs to the tile's monster group, so it can be set once a monster has been placed:

- **Stay**: Remain at this position. Only attack when the party is nearer than the reaction distance.
- **Wait**: Wait at this position until the party is nearer than the reaction distance, then attack and chase the hero.
- **Patrol**: Patrol between this position and a target position until the party is nearer than the reaction distance, then attack and chase the hero. The target row and column appear below the behaviour when Patrol is selected.
- **Random**: Move randomly through the maze until the party is nearer than the reaction distance, then attack and chase the hero.

## Edit Monster Attributes, Spells, and Inventory

![Monster Stats](/assets/ETMEditor/DetailMonsterStats.jpg) | ![Monster Inventory](/assets/ETMEditor/DetailMonsterStatsAdd.jpg)

This screen displays the stats of the selected monster and allows you to customize it:

- **Left panel**: Shows the inventory of the monster class. These are default items that every monster of this type carries.
- **Middle panel**: Add specific game items for this individual monster instance.
- **Right panel**: View and manage the magic spells this monster can cast.

## Monster Skill Level

![Monster Skill Level](/assets/ETMEditor/DetailMonsterSkill.jpg)

The skill level feature provides a quick way to scale monster difficulty without creating multiple monster variants. Each skill level increase provides:

- **+50% Hitpoints**: Makes the monster more durable in combat
- **+50% Mana**: Allows the monster to cast more spells

This is particularly useful for creating difficulty progression in later levels, where you can reuse the same monster types but make them significantly more challenging by simply adjusting their skill level. 

<hr>
**[Back to Tutorial Overview](/ETMEditorTutorials/ETMEditorTutorials)**
