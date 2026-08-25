---
layout: post
permalink: /escape-the-dungeon-maze-r48-released/
title: R4.8 Released - Bows, Crossbows, Throwable Ammo & Glowing Items
description: The August 2026 update brings ranged combat to the maze with seven distance weapons, five kinds of ammo, skill-driven throwing, glowing items, and the Level Editor tools to build them all
date: 2026-08-30 12:00:00 -0000
last_modified_at: 2026-08-30 12:00:00 -0000
publish: true
pin: false
categories:
- Escape The Dungeon Maze
- Game Development
tags: [ETM]
---

The August 2026 update <span style="background-color: #4CAF50; color: white; padding: 3px 8px; border-radius: 12px; font-size: 0.85em; margin-left: 5px;">R4.8 - August 2026</span> for "Escape The Dungeon Maze" and the corresponding Level Editor is now **officially released**!

Until now, every fight in the maze happened at arm's length. This release changes that: your heroes can shoot, sling and hurl. Seven new distance weapons, five kinds of ammunition, and a throwing system where the hero's own skills decide how far and how hard something lands — plus a way to make the truly special finds unmistakable.

## Take the Fight to a Distance

<div style="display: flex; gap: 10px; margin: 20px 0;">
  <img src="/assets/2026/08/IMG_0009.PNG" alt="The party facing a monster with a crossbow, bow and sling ready on the attack buttons, each showing its loaded ammo count" style="width: 100%;">
</div>

Seven **distance weapons** join the arsenal: a slingshot, three bows and three crossbows. A distance weapon is held in the weapon hand while its ammo rides in the off hand, and attacking fires a single piece rather than swinging. Each launcher accepts its own family of ammunition — **bows** take arrows, **crossbows** take bolts, and the **slingshot** takes stones — so what you carry decides what you can actually shoot.

A shot is scored as a proper weapon hit: the damage comes from the launcher rather than the projectile's weight, Hunter proficiency applies, monster armor reduces it, and the shot carries the launcher's full range. The three bows and three crossbows differ in reach and power, so there's a real choice between a light, quick launcher and a heavy one that hits harder. And an unloaded bow simply does nothing — no shot, no improvised club swing.

## A Quiver in Every Hand

<div style="display: flex; gap: 10px; margin: 20px 0;">
  <img src="/assets/2026/08/IMG_0010.PNG" alt="Valerian's inventory with a slingshot equipped in one hand and a stone in the other, and a bow, arrow, crossbow and bolt waiting in the backpack" style="width: 100%;">
</div>

Ammunition is a new kind of equippable item, and there are five to find: **arrows**, **bolts**, **stones**, **throwing stars** and **throwing daggers**. Ammo is the one equippable whose hand you never have to pick — it takes the free hand on its own, and equipping a weapon pushes the stack over to the off hand rather than dropping it, so the quiver simply changes hands.

A quiver is worn as a whole stack rather than piece by piece, and it never splits across two inventory slots. The attack button shows the loaded ammo ahead of the weapon and carries a **count badge** so you can see at a glance how many shots are left. Throwing stars and daggers need no launcher at all — they're simply thrown by hand.

## Throw Anything You Find

Ranged combat isn't limited to purpose-built weapons. Any item lying on the floor can now be picked up and **thrown forward**, and it behaves like flying magic on the way: it damages the monster group it hits, sets off an attack trigger on the wall it strikes, gets turned by rotators and carried through teleports. Wherever it stops, it ends up back on the floor — and stairs or an open pit will take it down to the level below.

How that throw lands is now the hero's business, not just the object's. **Strength** carries a throw further — every 50 points buys another tile of range — while **dexterity** decides how hard it hits, including the critical rolls that melee attacks already use. A trained thrower and an untrained one holding the same dagger will get visibly different results.

One more change to what ends up on the floor: **fallen heroes now drop their worn equipment too**. Helmets, shields and weapons used to stay on the corpse and were lost with it, but now the whole loadout stays behind for the rest of the party to recover.

## Glowing Finds

<div style="display: flex; gap: 10px; margin: 20px 0;">
  <img src="/assets/2026/08/IMG_0012.PNG" alt="A glowing skill potion lying on the dungeon floor, its coloured halo marking it as a permanent effect" style="width: 100%;">
</div>

Exceptional items can now carry a **glow** — a coloured halo that marks them out in the inventory, in every list and dialog, and on the model itself down in the dungeon, where it's visible well outside the torchlight. The new **Magic Sword** wears one, as does every permanent skill potion, each in a brighter version of its own liquid colour. "Glowing means permanent" reads instantly, without losing the colour code you already know.

The halo follows the item everywhere it appears: the inventory grid, the worn slots, chests, the item info sheet and the watch views all pick it up. An equipped glowing weapon even lends its colour to the attack button, which also gained a darker recess behind the icon — a small change that makes every weapon icon easier to read against the light stone, glowing or not.

## Building It All in the Level Editor

<div style="display: flex; gap: 10px; margin: 20px 0;">
  <img src="/assets/2026/08/IMG_0013.PNG" alt="The Level Editor's weapon model picker showing the new long bow, light and heavy crossbows and slingshot alongside the Magic Sword, with a Bolt placed on the level" style="width: 100%;">
</div>

The Level Editor gets everything it needs to author the new gear. **Ammo items** have their own attribute panel: base damage, the launcher they fit — bow, crossbow, sling or thrown — and the elemental damage they carry. **Distance weapons** are built by picking a bow, crossbow or slingshot model, which locks the weapon class and lets you choose the ammunition it fires, so the editor and the game can never disagree about what shoots what.

Item **glow colors** are editable too, with a toggle and colour picker in the appearance section, and the halo shows up in both the icon and the 3D preview as you work. Validation has grown a matching check: it now warns when a level pack ships a distance weapon but no ammunition that fits it — a bow nobody can fire.

Triggers gained a genuinely new combination as well. An **item-drop trigger** can now wait for one specific item *and* spawn a different one in return, using two independent slots — so a niche can accept an offering and produce something else for it. The dropped item is never revealed to the player: the dialog still lists the whole inventory, and only the right offering makes anything happen.

This release also brings the usual round of fixes on both sides — pit rendering at the ceiling, iOS landscape layout and iCloud sign-out handling in the game, and a trigger dialog that now refreshes properly when you change the trigger type in the editor.

---

Thank you for playing! More adventures await in the maze. Development is still ongoing — stay tuned for the next updates!

<div style="display: flex; justify-content: space-around; align-items: center;">
  <div style="text-align: center;">
    <a href="https://apps.apple.com/app/escapethemaze/id1502853397">
      <img src="/assets/Download.svg" alt="Download">
    </a>
  <p>Download the Game</p>
  </div>
  <div style="text-align: center;">
    <a href="https://apps.apple.com/app/etdm-level-editor/id1561041898">
      <img src="/assets/Download.svg" alt="Download" >
    </a>
    <p>Download the Level Editor</p>
  </div>
</div>
