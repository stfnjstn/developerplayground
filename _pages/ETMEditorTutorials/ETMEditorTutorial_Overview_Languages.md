---
layout: page
permalink: /ETMEditorTutorials/ETMEditorTutorial_Overview_Languages/
title: Tutorial - Create / Organize Languages
description: Create / Organize Languages
date: 2025-01-22 19:02:46 -0000
last_modified_at: 2026-09-13 12:00:00 -0000
publish: true
pin: false
categories: [Apps]
tags: [Games]
---

![Overview Languages](/assets/ETMEditor/OverviewLanguages.jpg)

The Language feature allows you to localize your level pack for players around the world. By adding translations, you can make your dungeons accessible to a global audience. The localization system is designed to be simple and efficient, focusing on the most important text elements that players will encounter.

**Note**: You must have at least one level created before you can add language translations.

## What Can Be Localized

The following elements in your level pack can be translated into different languages:

- **Level Names**: Used in save games and level selection screens
- **Custom Scroll Text**: Messages shown when players read or learn from scrolls
- **Custom Game Item Names**: Displayed in the game inventory
- **Wall Text**: Text that appears on walls throughout your dungeon

The system is intentionally kept simple because dungeon crawlers typically don't have extensive dialogue, focusing instead on exploration and combat.

## Add a Language

To add a new language to your level pack:

1. Open the **Languages** tab in the level pack overview
2. Click the **+** button to add a new language
3. Select the language you want to add from the language picker — the list shows every language by its own name and code, and the search field filters it
4. The new language will appear in the overview list

Once added, the language will be available for translation in your level pack.

## Manage Translations

![Overview Languages Detail](/assets/ETMEditor/OverviewLanguagesDetail.jpg)

To translate content for a specific language:

1. Tap on a language in the overview (e.g., "de" for German)
2. You'll see a list of all translatable elements from your level pack
3. Each element has an icon indicating its type (level name, scroll text, item name, or wall text)

### Translation Interface

Each translatable element is one row with two lines:

- **Small line (English)**: The original text in English (default language)
- **Text field (Translation)**: The translation, editable in place

If no translation has been entered, the English version will be used as the default fallback.

### Enter a Translation

Simply type into the row's text field. There is nothing to confirm: the translation is applied as you type and stored with the level pack when you save it. Clearing a field leaves the previous translation in place, so an accidental delete does not wipe a good value.

The translation is used in-game when a player selects that language.

<hr>
**[Back to Tutorial Overview](/ETMEditorTutorials/ETMEditorTutorials)**

