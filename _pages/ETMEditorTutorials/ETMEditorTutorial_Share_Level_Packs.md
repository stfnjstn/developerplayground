---
layout: page
permalink: /ETMEditorTutorials/ETMEditorTutorial_Share_Level_Packs/
title: Tutorial - Share Level Packs
description: How to share your custom level packs with other players
date: 2026-01-25 12:00:00 -0000
last_modified_at: 2026-01-25 12:00:00 -0000
publish: true
pin: false
categories: [Apps]
tags: [Games]
---

## Sharing Your Level Packs

Once you've created an amazing dungeon experience, you can share it with other players! The Level Editor provides several ways to distribute your custom level packs.

## Export Your Level Pack

![Eport](/assets/ETMEditor/Share0.jpg)

To export and share your level pack:

1. Open your level pack in the editor
2. Click the **Export** button (the third icon in the top toolbar)
3. Choose where to save your exported level pack file
4. The editor will create a `.etdm` file containing all your levels, monsters, items, and settings

## Sharing Methods

![Share](/assets/ETMEditor/Share1.jpg)

You can share your level pack using:

- **Email**: Send the `.etdm` file directly to friends
- **Local or iCloud Storage**: Save to Files app for later access
- **AirDrop**: Share directly to nearby devices

### Opening Shared Level Packs

When someone receives your `.etdm` file:

![Play](/assets/ETMEditor/Share2.jpg)

1. Tap or open the `.etdm` file on their iOS/Mac device
2. The file uses Apple's URL scheme mechanism to automatically launch "The Dungeon - Get Out"
3. The game will automatically import the level pack
4. The imported levels will be ready to play immediately
5. When you start a new game, you can select the new level pack

Players can also save the `.etdm` file and import it later by opening it whenever they're ready.

## JSON Export (Advanced)

For advanced users who want to edit level packs programmatically:

1. Export your level pack as usual (creates a `.etdm` file)
2. Rename the file extension from `.etdm` to `.json`
3. Edit the JSON file with your favorite code editor
4. Make your changes following the JSON structure
5. Rename back to `.etdm` to use in the game

For details on the JSON structure and available fields, see the [JSON Export documentation](/ETMEditorTutorials/ETM_Export_JSON).

<hr>
**[Back to Tutorial Overview](/ETMEditorTutorials/ETMEditorTutorials)**
