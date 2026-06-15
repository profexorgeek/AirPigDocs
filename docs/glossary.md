---
description: This page is a glossary of common terms used in the AirPig engine.
icon: book-open-lines
---

# Glossary

**AirPig** : The bestest game engine in the whole wide world.

**Animation**: A sequence of Keyframes that moves a Rig's bones over time, making an Entity walk, attack, or perform other actions.

**Bone**: A part of a Rig that can be positioned, rotated, and given attachments like a Sprite. Bones form the skeleton that brings an Entity to life.

**Body Collision**: A collision shape that defines a character's outline or total body shape. Body collision is used to determine what part of an object is clickable when editing items on a map, and also used to determine where an object can be hit during gameplay to take damage.

**Collision**: An invisible shape used to detect when objects touch or overlap, used for things like blocking movement or taking damage.

**Entity**: A generic term for a game object that typically has some kind of behavior. Examples include NPCs, monsters, chests, and the player character. Specifically, anything that has a Rig is a game Entity.

**Footprint Collision**: A collision shape that defines how much space an entity, such as a monster or barrel, takes up in space. Footprint collision is used by the engine to prevent objects from moving through each other. Footprint collision can be edited in AirPig's Rig Editor.

**Gear**: A weapon or a piece of armor. Gear is a more specific type of Item. Gear is created using AirPig's Item Editor.

**Geometry**: In the context of AirPig, geometry usually means the components of a map that determine how characters can move. A map's geometry includes the collision for the walls, the Navigation Mesh, and the definitions of the type of each tile.

**Instance**: A specific single object in the game, created from a more general concept. For example, you may have the concept of a Human Entity in your game. When you place that Entity in a map and name it "Sally", Sally is now a specific Instance of a Human.

**Item**: Anything that can be placed in the inventory of a player, NPC, or monster. A sword, helmet, or other piece of Gear are Items. Items are created using AirPig's Item Editor.

**Keyframe**: A specific point in time within an Animation where a bone's position or rotation is set. AirPig blends smoothly between keyframes to create movement.

**Layer**: One of several stacked parts of a Map, such as Background, Floor, Path, Wall, or Wall Tops, that together define how a map looks and works.

**Map**: A game level. Maps are composed of layers including the Background, Floor, Path, Wall, and Wall Tops layers. Maps are created using AirPig's Map Editor.

**Navigation Mesh:** This may also be shortened to Nav Mesh. Navigation Mesh determines where characters can walk on a map - especially NPC characters. A Navigation Mesh is just a bunch of points linked by lines. When an NPC needs to find a path, they use the Navigation Mesh to avoid obstacles and move to the target point.

**Rig**: Rigs are the foundation of all game entities. Rigs define bones that can have attachments such as a Sprite or an Item. Rigs have animations that determine how bones are positioned and rotated at specific keyframes. Every Entity in the game has a Rig that defines how it looks and moves.

**Sprite**: A small image, loaded from a PNG file, that represents a basic visual element in the game, like an item, or icon.

**Tile**: AirPig maps are made up of 16x16 pixel tiles. Each tile has a specific type including Background, Floor, Path or Wall. The tile types are used to determine which Sprite is used for each tile, and also whether the tile can be walked on by characters in the game.

**Variant**: A unique version, or variation, of a Rig. For example, a "humanoid" Rig might define walking, attacking, and other animations but have multiple types of humanoid creatures such as Humans, Goblins, Skeletons, or Zombies that are all Variants of the Rig. When you place a Rig into a map, you can define which Variant the Rig should be, such as Human for a friendly NPC or Zombie for a monster.
