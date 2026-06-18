---
description: >-
  This page describes how to create sprites, music, audio, and other rw content
  for use in AirPig games.
icon: file-image
---

# Creating Raw Content

Most of the game development and game content creation happens within the AirPig editor experience. Content created by AirPig itself are often referred to as "assets" in documentation and the engine. However, "raw" assets such as sprites, sounds, and music, are authored in programs such as PhotoShop or Aseprite.

When a new project is created in AirPig, it will automatically create a folder structure on disk for the content types described below.

{% hint style="success" %}
AirPig regularly scans the game folder for new content but may not immediately pick up new content when added to folders outside of AirPig. You can click "Rescan Assets" from the editor menu at any time to pick up newly-added items including both raw content and assets such as rigs that were copied from another project!
{% endhint %}

### root

The root project directory should contain a `.pig` file that is your main project file loaded by AirPig to load and edit a game project. It will also include files that store item and quest data. Raw content assets should not be placed in the project root folder.

### biomes

The engine will look for "biome" files in the `biomes` folder.

An AirPig "biome" is a tileset used by a map to define the look of a map. There is a 1:1 relationship between map and biome - meaning each map can only have a single biome defined. A biome is a 256x256 pixel png file that has a specific layout. The game engine uses this layout to resolve the tiles based on the tile type defined on the map (Background, Floor, Path, Walls).

All tiles in AirPig are 16x16 pixels.

This means that you can "hot swap" the biome used by a map without redrawing any tiles or map geometry. This also allows you to duplicate a map and change the biome, reusing a map layout while changing the look of the map.

Each png placed in the `biomes` folder is expected to be a 256x256 pixel png file with the following layout.

{% hint style="danger" %}
WIP: biome layout diagram coming soon!
{% endhint %}

### maps

The engine will save game maps into the `maps` folder. You should not place any raw assets in this folder.

### music

The engine will look for song files in the `music` folder. Song files should be saved in OGG format.

### sounds

The engine will look for sound effect files in the `sounds` folder. Sound files should be saved in WAV format.

### sprites

The engine will look for sprite files in the `sprites` folder. Sprites are expected to be individual PNG files, not atlas, spritesheets, or animation strips.

AirPig will automatically pack all sprites into sprite atlases as part of the game publishing process for performance!

{% hint style="warning" %}
The texture packing/atlasing feature is not yet implemented and will be built in a future phase as part of the game publishing process.
{% endhint %}

### rigs

The engine will save rig files into the `rigs` folder. Raw content should not be placed in this folder.

