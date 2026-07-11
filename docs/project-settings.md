---
description: A reference for every setting stored in an AirPig project, useful for fine-tuning game feel without writing code.
icon: sliders
---

# Project Settings

### Intro to Project Settings

Every AirPig project has a `.pig` file in its root folder (see [Creating Raw Content](creating-raw-content.md)) - that's your main project file. Tucked inside it is a `Settings` section full of small numeric and color values that control game feel: things like how quickly the camera catches up to the player, how long a dash lasts, or what color a Polygon shows up as while you're editing a map.

Most creators will never need to touch these - AirPig ships with sensible defaults for everything. But if you want to fine-tune exactly how snappy dashing feels, how forgiving damage resistance is, or how fast the camera settles after the player stops moving, you can open your project's `.pig` file in a text editor and adjust the values under `Settings` directly. There's no in-editor screen for these yet, so changes mean hand-editing the JSON and reloading the project.

{% hint style="warning" %}
Make a backup of your `.pig` file before hand-editing it. A broken or malformed JSON file may fail to load.
{% endhint %}

The settings below are split into two groups:

- **Gameplay Settings** change how the game actually plays for everyone, including in the published game.
- **Editor-Only Settings** only change how things look while you're editing - mostly overlay colors for collision shapes, Polygons, and other markers that are invisible during real gameplay. These never affect the published game.

### Gameplay Settings

**CameraDrag**: `float`. Camera follow smoothing factor. Higher values make the camera track the player more tightly; lower values create more cinematic lag.

**CameraLerpDuration**: `float`. Duration in seconds over which the camera eases toward the player's position each frame. Lower is snappier; higher is more cinematic lag.

**DamageAnimSec**: `float`. How long, in seconds, an entity stays in its hurt/damaged animation after taking a hit.

**DashAnimSec**: `float`. Duration in seconds of the dash animation, which also locks out other input while it plays.

**DashCooldownSec**: `float`. Seconds an entity must wait before it can dash again.

**DashMultiplier**: `float`. Speed multiplier applied while dashing, on top of the entity's normal move speed (including any Armor speed modifiers).

**DeadFadeSec**: `float`. Seconds it takes a dead entity to fully fade out before it's removed from the map.

**DyingAnimSec**: `float`. Duration in seconds of the dying animation, played before an entity's death-fade begins.

**InteractAnimSec**: `float`. Duration in seconds of the interact animation, played when an entity interacts with something.

**MaxDamageResistance**: `float`. The highest fraction of incoming damage that Defense can absorb, from 0 to 1. Capped at 0.9 by default so a very high Defense value still can't grant full immunity.

**MaxSoundDistance**: `float`. Distance in pixels from the camera at which positional sound effects become inaudible.

**MoveAnimStridePx**: `float`. Pixel distance covered by one full walk-cycle stride. A faster entity plays its walk animation proportionally faster, so its feet stay grounded to its actual movement instead of sliding.

**MovementDrag**: `float`. How quickly entity movement decelerates each frame. Higher values stop entities faster; lower values feel more slippery, with more momentum.

**MoveThresholdFraction**: `float`. The fraction of an entity's top move speed below which it's considered "resting" instead of "moving," for animation purposes. For example, 0.1 means an entity stops playing its walk animation once it drops below 10% of its top speed.

**MusicMix**: `float`. Music volume multiplier, applied on top of the player's master and music volume settings.

**PitchVariance**: `float`. Random pitch offset range applied to sound effects so repeated sounds don't feel robotic. For example, 0.05 means pitch varies by up to ±5%.

**RestAnimSec**: `float`. Duration in seconds of one cycle of the resting/idle animation.

**SecondsBeforePlayerRespawn**: `float`. After the player has fully faded out from death, how many seconds pass (with the camera holding its position) before they respawn at their last transition point.

**SoundMix**: `float`. Sound effect volume multiplier, applied on top of the player's master and sound volume settings.

**SpawnAnimSec**: `float`. Duration in seconds of the spawn-in animation played when an entity appears.

**SpawnIntervalSec**: `double`. Minimum seconds between consecutive entity spawns at a single spawn Polygon.

**StickDeadzone**: `float`. Analog stick dead zone radius; controller input below this magnitude is ignored. Increase this if a player's controller has stick drift.

**StoreRefreshIntervalSec**: `double`. Seconds between rerolls of the shared world store seed, which determines every shopkeeper's stock and prices. The reroll is deterministic per seed, so quickly transitioning between maps can't be used to force a reroll on demand.

**TransitionCooldownSec**: `double`. Cooldown in seconds between map transitions, to prevent rapid or accidental chained transitions.

**UnarmedAttackAnimSec**: `float`. Duration in seconds of the unarmed attack animation (adjusted by the active Variant's attack speed modifier). Used instead of a Weapon's attack speed when no weapon is equipped.

**UnarmedAttackOffset**: `Vector2`. Center point of the unarmed attack's melee collision circle, relative to the rig's weapon bone. Used instead of a Weapon's collision offset when no weapon is equipped.

**UnarmedAttackRadius**: `float`. Radius, in world units, of the melee collision circle used for unarmed attacks. Used instead of a Weapon's collision radius when no weapon is equipped.

### Editor-Only Settings

**EntityBodyColor**: `Color (hex)`. Overlay color for an entity's Body Collision shape in the editor.

**EntityBoneColor**: `Color (hex)`. Overlay color for bone indicators in the Rig Editor.

**EntityFootprintColor**: `Color (hex)`. Overlay color for an entity's Footprint Collision shape in the editor.

**InactiveSpriteBoundsColor**: `Color (hex)`. Overlay color for sprite bounds on layers other than the one you're currently placing sprites on.

**MapPolyColor**: `Color (hex)`. Overlay color for map collision Polygon geometry in the editor.

**NavEdgeColor**: `Color (hex)`. Overlay color for the lines connecting Navigation Mesh points in the editor.

**NavMeshWarningColor**: `Color (hex)`. Overlay color used to flag Navigation Mesh problems, such as disconnected points, in the editor.

**NavPointColor**: `Color (hex)`. Overlay color for individual Navigation Mesh points in the editor.

**PolyHandleColor**: `Color (hex)`. Overlay color for a Polygon's Node handles while editing its shape.

**SelectedShapeColor**: `Color (hex)`. Overlay color for whichever shape is currently selected in the editor.

**SpriteBoundsColor**: `Color (hex)`. Overlay color for sprite bounds rectangles in the editor.

**TileCollisionColor**: `Color (hex)`. Overlay color for tile collision rectangles in the editor.

**ZoneCollideColor**: `Color (hex)`. Overlay color for Polygons with a Collide behavior (solid collision) in the editor.

**ZoneDamageColor**: `Color (hex)`. Overlay color for Polygons with a Damage behavior in the editor.

**ZoneNoneColor**: `Color (hex)`. Overlay color for Polygons with no behavior assigned yet, in the editor.

**ZoneSpawnColor**: `Color (hex)`. Overlay color for Polygons with a Spawn behavior in the editor.

**ZoneTransitionColor**: `Color (hex)`. Overlay color for Polygons with a Transition behavior in the editor.
