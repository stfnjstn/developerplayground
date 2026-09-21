---
layout: page
permalink: /ETMEditorTutorials/ETMEditorTutorial_Level_Settings_Tab/
title: Tutorial - Level Settings & Maze Generator
description: Level Settings
date: 2025-01-22 19:02:46 -0000
last_modified_at: 2026-09-13 12:00:00 -0000
publish: true
pin: false
categories: [Apps]
tags: [Games]
---
![LevelTileSettingsTab](/assets/ETMEditor/DetailIcons.jpg)

![Detail Level Setting](/assets/ETMEditor/DetailLevel.jpg)

- _Current level number_: You can change the level with the stepper.
- _Display name_: It is used for savegames, maps and inside the editor.
- _Rows/Cols_: Dimension of the current level (5 to 20). Can be changed with the steppers; new rows and columns are added as walls, removed ones are cut off.

## Maze Generator:

![Maze Generator](/assets/ETMEditor/MazeGenerator.jpg)

You can add specific elements randomly in the maze or generate a complete new random maze without special tiles (Warning: This will overwrite your existing maze). Set the quantities next to the elements and press **Generate Maze** to build a new maze with all of them at once, or press an element's own button to scatter only that element over the current maze. A generated maze has an odd size between 11 and 19; the level is resized if needed, and the start position moves to (1,1) if it no longer lies on a free tile. Pits need a level below to fall into, and monsters need at least one big and one small monster class — otherwise the generator tells you why it did nothing.

<hr>
**[Back to Tutorial Overview](/ETMEditorTutorials/ETMEditorTutorials)**
