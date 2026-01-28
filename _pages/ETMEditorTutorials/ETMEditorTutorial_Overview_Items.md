---
layout: page
permalink: /ETMEditorTutorials/ETMEditorTutorial_Overview_Items/
title: Tutorial - Create / Organize GameItems
description: Create / Organize GameItems
date: 2025-01-22 19:02:46 -0000
last_modified_at: 2026-01-28 22:16:14 -0000
publish: true
pin: false
categories: [Apps]
tags: [Games]
---

![Overview Items](/assets/ETMEditor/Items0Overview.png)

Game items bring depth and complexity to your dungeon gameplay. They can be keys for locks, food for healing, scrolls with messages or spells, and potions with various effects. Items reward exploration, enable puzzle solutions, and provide strategic choices for players.

## Built-in vs Custom Items

You have two options when working with game items:

### Built-in Items
- **Pre-configured**: Ready to use with established effects
- **Cannot be modified**: Their properties are locked
- **Quick to deploy**: Perfect for standard dungeon items
- **Tap to view**: You can view their details in read-only mode

### Custom Items
- **Fully customizable**: Control appearance, name, and effects
- **Unique designs**: Create items that fit your level pack's theme and story
- **Can be modified**: Adjust properties anytime
- **Can be deleted**: Remove custom items you no longer need

## Item Types

The Level Editor supports several types of game items:

- **Keys**: Unlock doors and chests with color-coded matching
- **Food**: Restore health and provide sustenance
- **Scrolls**: Display text messages or teach magic spells
- **Potions**: Provide temporary buffs, permanent upgrades, or healing effects

**Note**: Weapons and armor are planned for future updates!

### Filter Bar

![Filtered Items](/assets/ETMEditor/Items1Filtered.jpg)

Use the filter bar at the top of the item list to show only specific item types. This makes it easier to find the item you're looking for when you have many custom items.

## Create a New Item

To create a custom item:

1. Click the **+** button at the top of the item list
2. The item detail screen will open
3. Select the item type and configure all properties
4. Save your new item

To delete a custom item, swipe left on an item row and tap delete. **Note**: Only custom items can be deleted; built-in items are permanent.

## Tinting System

One of the most powerful features in the item system is **tinting** - the ability to create unlimited visual variations from a single 3D model by applying different colors.

### How Tinting Works

For tintable items (like potions and keys), you can customize:
- **Primary color**: Main body color
- **Secondary color**: Accent details
- **Tertiary color**: Additional highlights (model-dependent)

This means you can create countless unique items from one 3D model. For example:
- Multiple colored keys for complex puzzles
- Different colored potions for various effects
- Visually distinct food items

### Non-Tintable Items

Some items like scrolls and bread use fixed textures instead of tinting. For these items, you select the texture rather than choosing colors.

## Icon Selection

When creating an item, choose an icon that represents it in the game inventory. For tintable items, the icon will automatically match the colors you selected. The icon appears:
- In the item placement dialog in the Level Editor
- In the player's inventory during gameplay
- When items are displayed on the ground

## Custom Keys

![Custom Keys](/assets/ETMEditor/Items2Keys.jpg)

Keys are essential for dungeon puzzles. The key system uses the tinting feature to create color-coded matching:

### Creating Custom Keys
- Select the key 3D model
- Choose up to 3 colors for the key
- Give the key a descriptive name
- The key will only open doors/chests with matching colors

### Key Puzzle Design
- Use different colored keys for multi-stage puzzles
- Hide keys in hard-to-reach places or behind other puzzles
- Place keys as monster drops for combat-based progression

**Tip**: Use consistent color schemes across your level pack so players can recognize key-lock relationships at a glance.

## Custom Food Items

![Custom Food](/assets/ETMEditor/Items3Food.jpg)

Food items restore the player's health and provide strategic healing opportunities.

### Creating Custom Food
- Select a food 3D model (bread, apples, meat, etc.)
- Choose texture or colors depending on the model
- Set the healing amount
- Give it a descriptive name

### Food Design Tips
- Place basic food frequently for gradual healing
- Add powerful food items as rare rewards
- Use food strategically before difficult encounters
- Consider food as monster drops for sustained exploration

## Custom Scrolls

![Custom Scrolls](/assets/ETMEditor/Items4Scrolls.jpg)

Scrolls serve two purposes in the game:

### Spell Learning Scrolls
These teach the player new magic spells. **Note**: Built-in spell scrolls already exist for all spells, so custom spell scrolls are rarely needed.

### Text Scrolls
These display custom text messages to the player. Perfect for:
- **Story elements**: Tell your dungeon's backstory
- **Hints**: Provide puzzle solutions or directions
- **Lore**: Add flavor text and world-building
- **Instructions**: Guide players through complex mechanisms

### Creating Text Scrolls
1. Select the scroll item type
2. Choose "Text Scroll" mode
3. Enter your message text
4. Set the scroll texture
5. Name the scroll appropriately

**Creative Uses**:
- Diary entries from previous adventurers
- Riddles that hint at puzzle solutions
- Warnings about upcoming dangers
- Victory messages when puzzles are solved

## Custom Potions

Potions add strategic depth with three distinct types:

### Restore Potions (One-Time Use)

![Restore Potions](/assets/ETMEditor/Items5PotionRestore.jpg)

These provide immediate effects and are consumed:
- **Healing potions**: Restore hitpoints
- **Mana potions**: Restore magic energy
- **Cure potions**: Remove negative status effects

**Use Cases**: Emergency healing, preparing for boss fights, recovering after combat

### Permanent Potions

![Permanent Potions](/assets/ETMEditor/Items5PotionPermanent.jpg)

These provide lasting upgrades like:
- **Stat increases**: Permanently boost strength, defense, etc.
- **Max HP increases**: Permanently raise maximum hitpoints
- **Max Mana increases**: Permanently raise maximum mana

**Use Cases**: Character progression rewards, hidden treasures, quest completion bonuses

### Temporary Potions (Buffs)

![Temporary Potions](/assets/ETMEditor/Items5PotionTemp.jpg)

These provide time-limited enhancements:
- **Strength buffs**: Increased attack power for a duration
- **Defense buffs**: Reduced damage taken
- **Speed buffs**: Faster movement
- **Skill potions**: Special abilities and tactical advantages

**Use Cases**: Boss preparation, difficult combat sections, time-based challenges

### Creating Custom Potions
1. Select the potion 3D model
2. Choose colors using the tinting system
3. Select potion type (Restore, Permanent, or Temporary)
4. Configure the effect and duration (for temporary)
5. Name the potion to reflect its effect



## Using Items in Your Levels

Once you've created items, you need to place them in your levels. The process for adding items to specific tiles is covered in detail here:

[Add GameItems to a Level](/ETMEditorTutorials/ETMEditorTutorial_Level_Item_Tab)

<hr>
**[Back to Tutorial Overview](/ETMEditorTutorials/ETMEditorTutorials)**