---
tags:
  - File
---
# File "entities2.xml"

This page needs some content. You can contribute to it using the Edit Button!

old tutorial: [https://www.reddit.com/r/themoddingofisaac/comments/36o00t/entitys_explained_how_to_add_entity_variants/](https://www.reddit.com/r/themoddingofisaac/comments/36o00t/entitys_explained_how_to_add_entity_variants/)

**Resource-Folder**{: .xmlInfo }: Using this file in a resource folder of a mod is not tested yet.

**Content-Folder**{: .xmlInfo }: Using this file in a content folder of a mod is not tested yet.


| Variable-Name | Type | Description |
|:--|:--|:--|
| name | str ||
| id | int | Type of the entity. Max Value: 4095 |
| variant | int | Variant of the entity. The maximum value is 4095. If you leave this blank, then the game will automatically chose the next available number. |
| subtype | int | SubType of the entity. The maximum value is 255. (The reason for this is that the hash map generator of the .stb format expects a specific bit-depth.) |
| anm2path | string | Path to the [anm2 file](Anm2_files.md), relative to the given anm2root. Example: `001.000_Player.anm2` |
| baseHP | int ||
| boss | int | Entity is a boss. Possible values: ['0', '1'] |
| bossID | int ||
| champion | int | Allow champion variants of this entity. Possible values: ['0', '1'] |
| collisionDamage | float ||
| collisionMass | float | Entity weight: lighter entities deal less knockback and are more affected by it. |
| collisionRadius | float | Radius of the collision circle. This value is used for both entity <--> entity and entity <--> grid collisions. This changes the `Entity.Size` field. |
| collisionRadiusXMulti | float | Multiplier for the X direction of the collision circle. This can be used to grant an entity an elliptical hitbox |
| collisionRadiusYMulti | float | Multiplier for the Y direction of the collision circle. This can be used to grant an entity an elliptical hitbox |
| collisionInterval | int | Number of game ticks till the next collision should be evaluated. Default = 1 |
| numGridCollisionPoints | int | Number of points along the edge of the collision circle, which are used to detect collisions with grid entities. |
| friction | float | "Slippyness" of the entity. Default = 1. Lower values make them slide more, similar as they would standing on ice. Higher values make them slide less. A value of 0 makes them unable to move. |
| shadowSize | float | Scales down the size of the shadow. |
| stageHP | int | Scales the entity HPs: $\text{entityHP} = \text{baseHP} + \text{stageNumber} \times \text{stageHP}$ |
| tags | string | possible values: ['nodelirium', 'spider', 'explosive_soul', 'cansacrifice', 'ghost', 'brimstone_soul', 'homing_soul', 'fly', 'noreroll']<br>See Chapter below for in depth explanations of the tags. |
| gridCollision | string | possible values: ['nopits', 'ground', 'none', 'walls', 'floor'] |
| portrait | int | Death portrait ID. |
| hasFloorAlts | bool | If set to true, floor specific sprites should be used for this entity if they exist. See the chapter below for more informations |
| reroll | bool ||
| shutdoors | bool | If alive, force doors to be closed. |
| shieldStrength | int ||

## Tags explanation

| Stage-Name | Suffix |
|:--|:--|
| cansacrifice | Marks familiars on which sacrificial altar can be used on|
| nodelirium | Blacklists a boss from being used by Delirium|
| fly | Indicates enemies which should be neutralized by Skatole (does NOT affect Beelzebub)|
| spider | Indicates enemies which should be neutralized by Bursting Sack|
| ghost | Indicates enemies which Vade Retro can kill at <50% HP as a special interaction|
| noreroll | Immunity from D10 rerolls and the Ace cards|
| brimstone_soul | Friendly Ball wisps created by this enemy will fire Brimstone lasers|
| explosive_soul | Friendly Ball wisps created by this enemy will fire explosive tears|
| homing_soul | Friendly Ball wisps created by this enemy will fire homing tears|


## Floor specific sprites
If an entity has the attribute `hasFloorAlts` set to `true`, the game tries to load the spritesheet of the entity with an additional suffix, based on the current stage. The Suffix of a stage is defined in the `suffix` attribute in the stages.xml file. If no sprite can be found, it will load the default spritesheet.

**Example:**
Original Gaper sprite: monster_017_gaper.png

Downpour Sprite: monster_017_gaper_downpour.png

**Suffix per stage:**

| Stage-Name | Suffix |
|:--|:--|
|Flooded Caves|_downpour|
|Downpour|_downpour|
|Dross|_dross|
|Ashpit|_ashpit|
|Mausoleum|_mausoleum|
|Gehenna|_gehenna|

## `<gibs />` tag
The `<gibs />` tag is used to define the gibs that are spawned when an entity is killed or destroyed.

| Variable-Name | Possible Values | Description |
|:--|:--|:--|
| amount | int | How many gibs should be spawned|
| blood | int | Possible values: [0,1] where 0 is off and 1 is on|
| bone | int | Possible values: [0,1] where 0 is off and 1 is on|
| chain | int | Possible values: [0,1] where 0 is off and 1 is on|
| colorblood | int |Possible values: [0,1] where 0 is off and 1 is on|
| dust | int | Possible values: [0,1] where 0 is off and 1 is on|
| eye | int | Possible values: [0,1] where 0 is off and 1 is on|
| gut | int | Possible values: [0,1] where 0 is off and 1 is on|
| huge | int |Possible values: [0,1] where 0 is off and 1 is on|
| large | int |Possible values: [0,1] where 0 is off and 1 is on|
| poop | int |Possible values: [0,1] where 0 is off and 1 is on|
| rock | int |Possible values: [0,1] where 0 is off and 1 is on|
| rock_small | int |Possible values: [0,1] where 0 is off and 1 is on|
| small | int |Possible values: [0,1] where 0 is off and 1 is on|
| sound_baby | int |Possible values: [0,1] where 0 is off and 1 is on|
| sound_bone | int |Possible values: [0,1] where 0 is off and 1 is on|
| worm | int |Possible values: [0,1] where 0 is off and 1 is on|

## `<bestiary />` tag
The `<bestiary />` tag defines how is the entity is displayed in the game's bestiary.

| Variable-Name | Type | Description |
|:--|:--|:--|
| transform | string | Three numbers separated by commas: `x,y,size`. Where `x` and `y` are the coordinates of the sprite's center and `size` is a multiplies its size (0.5 = 50%, 1 = 100%, 2 = 200%, ...). |
| anim | string | The name of the animation played in the bestiary. Must be in the ANM2 specified by `anm2path`. |
| overlay | string | If specified, play this animation on top of the other one. |
| anm2path | string | If specified, search for `anim` in this file else use the one defined in `<entity>`. |
| alt | string | If specified, dispay a floor variant (see [this section](#floor-specific-sprites) for more information). |

## `<devolve />` tag
Defines the enemy the entity is rerolled into by the D10.

| Variable-Name | Type | Description |
|:--|:--|:--|
| id | int | The entity to devolve into: id.variant.subtype |
| weight | int | Unused. |


## `<preload-snd />` tag
A sound to preload. There may be multiple `<preload-snd />` per entity.

| Variable-Name | Type | Description |
|:--|:--|:--|
| id | int | The id of the sound (specified in sounds.xml). |