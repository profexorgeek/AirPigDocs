---
description: This page describes how to use AirPig's map editing functions.
icon: map
---

# Map Editor

The Map Editor is where everything comes together - drawing out a level's geometry and populating it with Entities, sprites, and Polygons. See the [Glossary](glossary.md) for a refresher on Maps, Layers, Tiles, and Polygons.

### Managing Maps

- **Open** loads an existing Map from your project.
- **Create** starts a brand new Map.
- **Resize** changes the current Map's dimensions.
- **Delete** permanently removes the current Map from your project.

Once a Map is loaded, you can rename it directly in the name field. **Is Starting Map** marks this Map as the one a new game begins on - checking it on one Map automatically unchecks it everywhere else in your project.

{% hint style="danger" %}
Screenshot needed: the map management toolbar and name/starting-map fields.
{% endhint %}

### Map Settings

- **Biome** - the tileset used to draw this Map. See [Creating Raw Content](creating-raw-content.md#biomes) for how Biomes work.
- **Background Color** - the color shown behind everything else on the Map.
- **Song** - the background music that plays on this Map. Use the set button to choose a track, or the clear button to remove it, and **Music Volume** to adjust its playback level.
- **Show Grid**, **Show Collision**, **Show Sprite Bounds**, **Show Nav Mesh** - overlay toggles that only affect what you see while editing; they don't change the published game.

### Painting Tiles

Choose a **Layer** (Background, Floor, Path, Wall, or Wall Tops) from the layer dropdown, then use one of the tile tools to paint it:

- **Pencil** paints one tile at a time.
- **Fill** paints every connected tile of the same type.
- **Rectangle** paints a rectangular area at once.

### Placing Entities

Use the entity list on the left, optionally narrowed with the filter box, to pick which Rig you want to place, then use the **Add Entity** tool to place instances of it on the Map. The **Edit Entity** tool lets you select and reposition instances already on the Map.

Selecting a placed Entity opens its instance details:

- **Variant** - which Variant of the Rig this specific instance uses.
- **Team** - which side this Entity is on (this also determines whether it can be assigned a Quest or configured as a shop).
- **Starting Cash** - how much currency this specific instance starts with, overriding its Variant's default.
- **Inventory** - Items this Entity carries but doesn't have equipped. Available for Character and Container Entities.
- **Equipped** - Items this Entity has equipped. Available for Character Entities.
- **Offered Quest** - the Quest this Entity offers, if any (only available for Entities on a non-Monster team).
- **Dialog** - add, edit, or remove Dialog entries this Entity can speak.
- **Configure Store** / **Remove Store** - turn this Entity into a shopkeeper with its own stock, or remove that configuration. A shorthand summary of the store's settings is shown once configured.

{% hint style="danger" %}
Screenshot needed: the entity list and the entity instance details panel (variant/team/inventory/equipped/dialog/store).
{% endhint %}

### Placing Sprites

Choose a sprite with the sprite chooser button, then use **Add Sprite** to place copies of it on the Map. **Edit Sprite** lets you select and reposition sprites already placed.

- **Placement Layer** decides which layer new sprites are added to, and filters which existing sprites the Edit tool can select.
- For layers that support manual stacking order, **Sort Layer** controls which sprites draw in front of others. This is disabled for the Entity layer, which is always sorted automatically by vertical position instead.

### Working with Polygons

Use **Add Polygon** to draw a new Polygon, and **Edit Polygon** to select and reshape an existing one by dragging its Nodes. See the [Glossary](glossary.md) for what a Polygon and its Nodes are.

Once a Polygon is selected, choose its **Behavior**:

- **None** - no special behavior; the shape is purely informational.
- **Collide** - acts as solid collision, blocking movement.
- **Damage** - deals damage to entities inside it. Set the **Damage Per Second** and which **Team** takes damage, and optionally attach a sound effect (with volume) that plays on damage.
- **Transition** - moves the player to another Map when they enter. Set the **Target Map**, the **Target** Polygon in that map to arrive at, an optional **Quest** that must be completed first, and whether this is the **Player Spawn** location used by default.
- **Spawn** - periodically spawns creatures. Set the **Spawn Rig** and **Spawn Variant** to create, how many spawn before the player encounters them (**Pre-Spawn**), and caps on **Active Creatures** and **Total Creatures**. Use the **Equipped** list to give spawned creatures starting equipment.

{% hint style="danger" %}
Screenshot needed: the Polygon properties panel for each Behavior (Damage, Transition, Spawn).
{% endhint %}

### Playtesting

The **Play** button launches the current Map for a quick in-editor playtest.
