---
layout: post
permalink: /escape-the-dungeon-maze-illumination-overhaul/
title: Fixing a Months-Long Lighting Bug - New Illumination System
description: How I finally tracked down a non-deterministic torch shadow bug in Escape The Dungeon Maze and rebuilt the entire illumination system
date: 2026-03-27 17:00:00 -0000
last_modified_at: 2026-03-27 17:00:00 -0000
publish: true
pin: false
categories:
- Escape The Dungeon Maze
- Game Development
tags: [ETM]
---

With a little help from Claude Code, I finally tracked down a bug that had been haunting me for months. Sometimes the torches would cast shadows, sometimes not — and occasionally everything in the dungeon was bathed in a flat, boring gray. Completely non-deterministic, nearly impossible to reproduce reliably.

The culprit? An omni light casting shadows requires **6 shadow maps** — one per cube face. A dungeon level with multiple torches quickly blows through SceneKit's shadow map budget, causing it to silently drop lights, sometimes including the player's own spotlight. The result: unpredictable lighting depending on how many torches were active at runtime.

## A Completely New Illumination System

Once the root cause was clear, the fix was straightforward: rebuild the illumination from the ground up, dropping the shadow-casting omni lights in favour of a new approach that stays within the hardware budget. Here is what the dungeon looks like now compared to before:

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

## Shadow Priority for Torches

I still wanted to keep those moody, atmospheric shadows in at least a few spots per level. To make this possible without blowing the shadow map budget, I added a **torch shadow priority** feature to the Level Editor. You can now assign up to 3 torches per level a shadow priority — and at runtime, depending on the device's hardware capabilities, 0 to 3 of those torches will actually cast shadows.

![Torch Shadow Priority in the Level Editor](/assets/2026/03/TorchShadowPriorityEditor.png)

This gives level designers fine-grained control over where the atmospheric shadow effect appears, while keeping performance stable across all supported devices.

The fix will ship with **R4.4 in April**. There is plenty more in the pipeline — new features, gameplay improvements, and surprises I can not wait to show you. Stay tuned!

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
