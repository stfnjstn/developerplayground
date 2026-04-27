---
layout: post
permalink: /escape-the-dungeon-maze-r44-released/
title: R4.4 Released - Per-Hero Inventory, New Illumination & More
description: The April 2026 update brings per-hero inventory management, a completely overhauled lighting system, and a wave of bug fixes
date: 2026-04-27 12:00:00 -0000
last_modified_at: 2026-04-27 12:00:00 -0000
publish: true
pin: false
categories:
- Escape The Dungeon Maze
- Game Development
tags: [ETM]
---

The April 2026 update <span style="background-color: #4CAF50; color: white; padding: 3px 8px; border-radius: 12px; font-size: 0.85em; margin-left: 5px;">R4.4 - April 2026</span> for "Escape The Dungeon Maze" and the Level Editor is now **officially released**!

This release brings a long-requested inventory overhaul, a completely reworked illumination system, and a solid round of bug fixes.

## Per-Hero Inventory

<div style="display: flex; gap: 10px; margin: 20px 0;">
  <img src="/assets/2026/03/InventoryLS.png" alt="Per-Hero Inventory" style="width: 100%;">
</div>

Each hero now has their own dedicated inventory. A new hero selector lets you switch between party members to manage their items individually — making party management more strategic and flexible. Items can also be rearranged directly via **Drag & Drop** within the inventory.

## Improved Illumination

<table style="width: 100%; border-collapse: collapse; margin: 20px 0;">
  <thead>
    <tr>
      <th style="text-align: center; padding: 8px;">Before</th>
      <th style="text-align: center; padding: 8px;">After</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="padding: 8px;">
        <img src="/assets/2026/03/IlluminationOld1.png" alt="Old illumination 1" style="width: 100%;">
      </td>
      <td style="padding: 8px;">
        <img src="/assets/2026/03/IlluminationNew1.png" alt="New illumination 1" style="width: 100%;">
      </td>
    </tr>
    <tr>
      <td style="padding: 8px;">
        <img src="/assets/2026/03/IlluminationOld2.png" alt="Old illumination 2" style="width: 100%;">
      </td>
      <td style="padding: 8px;">
        <img src="/assets/2026/03/IlluminationNew2.png" alt="New illumination 2" style="width: 100%;">
      </td>
    </tr>
  </tbody>
</table>

After months of chasing a non-deterministic lighting bug — torches sometimes casting shadows, sometimes not, and the dungeon occasionally going flat gray — the root cause turned out to be SceneKit's shadow map budget. An omni light needs 6 shadow maps (one per cube face), and a dungeon with multiple torches silently exhausted that budget, dropping lights unpredictably.

The fix: a completely new illumination system with better lights and shadows that stays within the hardware budget. To preserve the atmospheric torch shadows in key spots, the Level Editor now lets you assign a **shadow priority** to up to 3 torches per level:

<div style="display: flex; gap: 10px; margin: 20px 0;">
  <img src="/assets/2026/03/TorchShadowPriorityEditor.png" alt="Torch Shadow Priority in the Level Editor" style="width: 100%;">
</div>

At runtime, 0–3 priority torches cast shadows depending on the device's hardware capabilities — giving level designers control over atmosphere without sacrificing performance.

## What else is New
- **Cure spells** now target a single hero
- **Drag & Drop items** in inventory

## Bug Fixes

- Fixed: Pit rendering artefacts
- Fixed: Glitches in menu navigation
- Fixed: Hit animations
- Fixed: Heal animation
- Fixed: Attack button rendering in phone landscape
- Various other improvements and fixes

---

More is on the way — new features, new content, and surprises are already in the works. Stay tuned and keep exploring the maze!

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
