# Enum "ModCallbacks"
Execution order diagram: [![callback diagram](../../../images/infographics/Isaac Callbacks.svg){: width='500' }](../../../images/infographics/Isaac Callbacks.svg)


### MC_NPC_UPDATE {: .copyable } 
Called after an NPC is updated.

Returning any value will have no effect on later callback executions.

???- warning "Warning"
    This callback will NOT fire when the NPC is playing the "Appear" animation. For example, when a Gaper spawns, it will fire on frame 1, then on frame 31 and onwards. 

???- example "Example Code"
    This code will print "Hello World!" for every NPC Update. If the NPC is of the type "ENTITY_GAPER", it will also print "Gaper found".
    ```lua
    function mod:myFunction(entity) -- 'entity' contains a reference to the NPC
        print("Hello World!")
    end
    mod:AddCallback(ModCallbacks.MC_NPC_UPDATE, mod.myFunction)

    function mod:myFunction2(entity) -- 'entity' contains a reference to the NPC
        print("Gaper found!")
    end
    mod:AddCallback(ModCallbacks.MC_NPC_UPDATE, mod.myFunction2, EntityType.ENTITY_GAPER)
    ```

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|0 |MC_NPC_UPDATE {: .copyable } | ([EntityNPC](../../EntityNPC))|[EntityType](../EntityType) |

### MC_POST_UPDATE {: .copyable } 
Called after every game update. 

Returning any value will have no effect on later callback executions.

???- info "Execution informations"
    This callback is called 30 times per second. It will not be called, when its paused (for example on screentransitions or on the pause menu). 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|1 |MC_POST_UPDATE {: .copyable } | - | - |

### MC_POST_RENDER {: .copyable } 
Called after every game render (60 times per second). 

Returning any value will have no effect on later callback executions.

???- info  "Execution informations"
    It is highly recommended to only use this function when you want to render something. Its not recommended to use this function for things which are not frequently used or need constant recalculation. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|2 |MC_POST_RENDER {: .copyable } | - | - |

### MC_USE_ITEM {: .copyable } 
Called when a custom active item is used, after discharging it. 

The item [RNG](../../RNG) allows for the item's random events to be seeded. 

Return true to show the "use item" animation, otherwise false.Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|3 |MC_USE_ITEM {: .copyable } | ([CollectibleType](../CollectibleType),<br>[RNG](../../RNG))|[CollectibleType](../CollectibleType) |

### MC_POST_PEFFECT_UPDATE {: .copyable } 
Called for each player, each frame, after the player evaluates the effects of items that must be constantly evaluated.

Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|4 |MC_POST_PEFFECT_UPDATE {: .copyable } | ([EntityPlayer](../../EntityPlayer))|[PlayerType](../PlayerType) |

### MC_USE_CARD {: .copyable } 
Called when a card/rune is used.

Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|5 |MC_USE_CARD {: .copyable } | ([Card](../Card))|[Card](../Card) |

### MC_FAMILIAR_UPDATE {: .copyable } 
Called every frame for each familiar. 

Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|6 |MC_FAMILIAR_UPDATE {: .copyable } | ([EntityFamiliar](../../EntityFamiliar))|[FamiliarVariant](../FamiliarVariant) |

### MC_FAMILIAR_INIT {: .copyable } 
Called just after a familiar is initialized. 

Returning any value will have no effect on later callback executions.

???+ bug 
    This Callback provides incomplete data in the [EntityFamiliar](../../EntityFamiliar) attribute. For example, the Position is always equal to Vector(0,0). 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|7 |MC_FAMILIAR_INIT {: .copyable } | ([EntityFamiliar](../../EntityFamiliar))|[FamiliarVariant](../FamiliarVariant) |

### MC_EVALUATE_CACHE {: .copyable } 
Called one or more times when a player's stats must be re-evaluated, such as after picking up an item, using certain pills or manually calling EvaluateItems() on an [EntityPlayer](../../EntityPlayer). 

Returning any value will have no effect on later callback executions.

???- info "Hint"
    Use this to let custom items change the player's stats, familiars, flying, weapons, etc. Items tell the game which stats they affect using cache values in items.xml. Then the callback should respond to the [CacheFlag](../CacheFlag) by setting the corresponding player stat. Other items' stat modifiers, multipliers, etc are applied before this callback is called.  

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|8 |MC_EVALUATE_CACHE {: .copyable } | ([EntityPlayer](../../EntityPlayer),<br>[CacheFlag](../CacheFlag))|[CacheFlag](../CacheFlag) |

### MC_POST_PLAYER_INIT {: .copyable } 
Called after a Player Entity is initialized. 

The optional parameter can be used to specify a Player Variant. 0 = Player, 1 = Co-Op-Baby

Returning any value will have no effect on later callback executions.

???+ bug 
    This Callback provides incomplete data in the [EntityPlayer](../../EntityPlayer) attribute. For example, the Position is always equal to Vector(0,0). 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|9 |MC_POST_PLAYER_INIT {: .copyable } | ([EntityPlayer](../../EntityPlayer))|PlayerVariant* |

### MC_USE_PILL {: .copyable } 
Called when a pill is used.

Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|10 |MC_USE_PILL {: .copyable } | ([PillEffect](../PillEffect))|[PillEffect](../PillEffect) |

### MC_ENTITY_TAKE_DMG {: .copyable } 
Called before new damage is applied.

If the entity has a DAMAGE_COUNTDOWN flag, it will ignore any other DAMAGE_COUNTDOWN hits for the duration specified.

Return true or nil if the entity or player should sustain the damage, otherwise false to ignore it. If the entity is an [EntityPlayer](../../EntityPlayer), the DamageAmount is the integer number of half-hearts of damage that the player will take. Otherwise, DamageAmount is a number of hit points.

???+ bug 
    Returning any value besides nil will prevent later callbacks from being executed. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|11 |MC_ENTITY_TAKE_DMG {: .copyable } | (TookDamage [[Entity](../../Entity)],<br>DamageAmount [float],<br>DamageFlags [int],<br>DamageSource [[EntityRef](../../EntityRef)],<br>DamageCountdownFrames [int])|[EntityType](../EntityType) |

### MC_POST_CURSE_EVAL {: .copyable } 
Curses is a bitmask containing current curses. Called after the current Level applied it's curses. Returns the new curse bitmask. Use Isaac.GetCurseIdByName() to get the curseID.

If a number is returned, it will be the "Curses" arg for later executed callbacks.

???+ bug 
    Returning a value that is not an integer or nil will cause the game to crash.
    
???+ warning "Warning"
    The last callback to return a valid return value wins out and overwrites previous callbacks' return values 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|12 |MC_POST_CURSE_EVAL {: .copyable } | (Curses) | - |

### MC_INPUT_ACTION {: .copyable } 
It is called when game/game entities wants to read an action input. 

[Entity](../../Entity) can be nil if the input is not read from an entity class.

The [InputHook](../InputHook) value can be used to determine if this callback was called through Input.IsActionTriggered(), Input.IsActionPressed(), or Input.GetActionValue() 

Return nil if you don't want to overwrite the input or value.  

The return value can be bool if it's a IS_ACTION_XXX hook or float if it's an GET_ACTION_VALUE hook. Float values should be in range of 0.0 and 1.0 

Returning any value will have no effect on later callback executions.

???- info "Execution informations"
    This callback is called roughly 1470 times a second. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|13 |MC_INPUT_ACTION {: .copyable } | ([Entity](../../Entity),<br>[InputHook](../InputHook),<br>[ButtonAction](../ButtonAction))|[InputHook](../InputHook) |

### MC_LEVEL_GENERATOR  {: .copyable }  

???+ bug
    This callback doesn't work right now and will never be called by the game! 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|14 |MC_LEVEL_GENERATOR  {: .copyable }  | - | - |

### MC_POST_GAME_STARTED {: .copyable } 

This function gets called when you start a game. The boolean value is true when you continue a run, false when you start a new one.

This callback will be called after MC_POST_NEW_ROOM and after MC_POST_NEW_LEVEL.

Returning any value will have no effect on later callback executions.

???- example "Example code"
    ```lua
    local function onStart(_,bool)
    	print(bool)
    end
    mod:AddCallback(ModCallbacks.MC_POST_GAME_STARTED, onStart) 
    ```

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|15 |MC_POST_GAME_STARTED {: .copyable } | (IsContinued [bool]) | - |

### MC_POST_GAME_END {: .copyable } 

This function gets called when the game over screen appears, or when the an ending starts playing. The boolean value is true when you died and got a game over, false when you won and got an ending.

Returning any value will have no effect on later callback executions.

???- example "Example code"
    ```lua
    local function onEnd(_,bool)
        print(bool)
    end
    mod:AddCallback(ModCallbacks.MC_POST_GAME_END, onEnd)
    ``` 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|16 |MC_POST_GAME_END {: .copyable } | (IsGameOver [bool]) | - |

### MC_PRE_GAME_EXIT {: .copyable } 


This function gets called when you quit a run. The boolean value is true when the game would normally create a continuable save, false when it wouldn't. Called twice when the game plays an ending.

Returning any value will have no effect on later callback executions.

???- example "Example code"
    ```lua
    local function onExit(_,bool)
        print(bool)
    end
    mod:AddCallback(ModCallbacks.MC_PRE_GAME_EXIT, onExit) 
    ```

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|17 |MC_PRE_GAME_EXIT {: .copyable } | (ShouldSave [bool]) | - |

### MC_POST_NEW_LEVEL {: .copyable } 
This triggers after transitioning a level or stage. 

Its always called **after** MC_POST_NEW_ROOM.

Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|18 |MC_POST_NEW_LEVEL {: .copyable } | -  | - |

### MC_POST_NEW_ROOM {: .copyable } 
This triggers after entering a room.

Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|19 |MC_POST_NEW_ROOM {: .copyable } | -  | - |

### MC_GET_CARD {: .copyable } 
This callback is used for handling Card Pools.

Because not all cards have the same chance to spawn, use [RNG](../../RNG) for a seeded random selection.

You can use the boolean values as a filter for the selection.

The return value determines, what [Card](../Card) will be spawned. Return nil to not replace the spawned card. 

Returned values will not update the "[Card](../Card)" arg of later executed callbacks.

???+ bug
    Returning a value that is not an integer or nil will cause the game to crash.

???+ warning "Warning"
    The last callback to return a valid return value wins out and overwrites previous callbacks' return values 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|20 |MC_GET_CARD {: .copyable } | ([RNG](../../RNG),<br>[Card](../Card),<br>IncludePlayingCards [bool],<br>IncludeRunes [bool],<br>OnlyRunes [bool]) | - |

### MC_GET_SHADER_PARAMS {: .copyable } 
Returns a table containing a key -> value pair for custom shader parameters. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|21 |MC_GET_SHADER_PARAMS {: .copyable } | (ShaderName [string]) | - |

### MC_EXECUTE_CMD {: .copyable } 
Returns a string separated by `<br />` (newline) per output line CMD is the first word of the Console input.

The parameters are the rest of the Input.

???+ info "Important"
    This function is NOT called for default game commands like Spawn or Debug.

Returning a string will print it to the console.

Returning any value will have no effect on later callback executions.

???- example "Example code"
    ```lua
    function mod.oncmd(_, command, args)
        print(command)
        print(args)
    end
    mod:AddCallback(ModCallbacks.MC_EXECUTE_CMD, mod.oncmd)
    -- executing command "Test apple 1 Pear test" prints
    -- Test
    -- apple 1 Pear test 
    ```

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|22 |MC_EXECUTE_CMD {: .copyable } | (CMD [string],<br>Parameters [string]) | - |

### MC_PRE_USE_ITEM {: .copyable } 
Called before an item is used.

Return true to prevent the default code of an item to be triggered. This will still discharge the item.

???+ bug
    Returning any value besides nil will also prevent later callbacks from being executed. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|23 |MC_PRE_USE_ITEM {: .copyable } | ([CollectibleType](../CollectibleType),<br>[RNG](../../RNG))|[CollectibleType](../CollectibleType) |

### MC_PRE_ENTITY_SPAWN {: .copyable } 
Called right before an entity is spawned. 

Optional: Return a table with new values `{ Type, Variant, Subtype, Seed }` to override these values of the spawned entity.

???+ bug
    Returning a value that is not a table or nil will cause the game to crash.
    
???+ warning "Warning"
    The last callback to return a valid return value wins out and overwrites previous callbacks' return values 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|24 |MC_PRE_ENTITY_SPAWN {: .copyable } | ([EntityType](../EntityType),<br>Variant [int],<br>SubType [int],<br>Position [Vector],<br>Velocity [Vector],<br>Spawner [[Entity](../../Entity)],<br>Seed [int]) | - |

### MC_POST_FAMILIAR_RENDER {: .copyable } 
Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|25 |MC_POST_FAMILIAR_RENDER {: .copyable } | ([EntityFamiliar](../../EntityFamiliar),<br>RenderOffset [Vector])|[FamiliarVariant](../FamiliarVariant) |

### MC_PRE_FAMILIAR_COLLISION {: .copyable } 
The Low value is true, when the entity collided with the collider first. Its false if the collider collides first.

Return true to ignore collision, false to collide but not execute internal code and nil to continue with internal code (example: taking damage on contact). 

???+ bug
    This Callback can only be used ONCE across all mods! It is highly recommended to not use this Callback without defining a [FamiliarVariant](../FamiliarVariant) unless its absolutely nessesary! 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|26 |MC_PRE_FAMILIAR_COLLISION {: .copyable } | ([EntityFamiliar](../../EntityFamiliar),<br>Collider [[Entity](../../Entity)],<br>Low [bool])|[FamiliarVariant](../FamiliarVariant) |

### MC_POST_NPC_INIT {: .copyable } 
Returning any value will have no effect on later callback executions.

???+ bug
    This Callback provides incomplete data in the [EntityNPC](../../EntityNPC) attribute. For example, the Position is always equal to Vector(0,0). 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|27 |MC_POST_NPC_INIT {: .copyable } | ([EntityNPC](../../EntityNPC))|[EntityType](../EntityType) |

### MC_POST_NPC_RENDER {: .copyable } 
Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|28 |MC_POST_NPC_RENDER {: .copyable } | ([EntityNPC](../../EntityNPC),<br>RenderOffset [Vector])|[EntityType](../EntityType) |

### MC_POST_NPC_DEATH {: .copyable } 
Gets called after the Death animation is played.

Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|29 |MC_POST_NPC_DEATH {: .copyable } | ([EntityNPC](../../EntityNPC))|[EntityType](../EntityType) |

### MC_PRE_NPC_COLLISION {: .copyable } 
The Low value is true, when the entity collided with the collider first. Its false if the collider collides first.

Return true to ignore collision, false to collide but not execute internal code and nil to continue with internal code (example: taking damage on contact). 

???+ bug
    This Callback can only be used ONCE across all mods! It is highly recommended to not use this Callback without defining an [EntityType](../EntityType) unless its absolutely nessesary! 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|30 |MC_PRE_NPC_COLLISION {: .copyable } | ([EntityNPC](../../EntityNPC),<br>Collider [[Entity](../../Entity)],<br>Low [bool])|[EntityType](../EntityType) |

### MC_POST_PLAYER_UPDATE {: .copyable } 
The optional parameter can be used to specify a Player Variant. 0 = Player, 1 = Co-Op-Baby

Returning any value will have no effect on later callback executions.

???- info "Execution informations"
    This callback is called 60 times per second 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|31 |MC_POST_PLAYER_UPDATE {: .copyable } | ([EntityPlayer](../../EntityPlayer))|PlayerVariant* |

### MC_POST_PLAYER_RENDER {: .copyable } 
The optional parameter can be used to specify a Player Variant. 0 = Player, 1 = Co-Op-Baby

Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|32 |MC_POST_PLAYER_RENDER {: .copyable } | ([EntityPlayer](../../EntityPlayer),<br>RenderOffset [Vector])|PlayerVariant* |

### MC_PRE_PLAYER_COLLISION {: .copyable } 
The Low value is true, when the entity collided with the collider first. Its false if the collider collides first.

Return true to ignore collision, false to collide but not execute internal code and nil to continue with internal code (example: taking damage on contact).

The optional parameter can be used to specify a Player Variant. 0 = Player, 1 = Co-Op-Baby

???+ bug
    This Callback can only be used ONCE across all mods! It is highly recommended to not use this Callback unless its absolutely nessesary! 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|33 |MC_PRE_PLAYER_COLLISION {: .copyable } | ([EntityPlayer](../../EntityPlayer),<br>Collider [[Entity](../../Entity)],<br>Low [bool])|PlayerVariant* |

### MC_POST_PICKUP_INIT {: .copyable } 
Returning any value will have no effect on later callback executions.

???+ bug
    This Callback provides incomplete data in the [EntityPickup](../../EntityPickup) attribute. For example, the Position is always equal to Vector(0,0). 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|34 |MC_POST_PICKUP_INIT {: .copyable } | ([EntityPickup](../../EntityPickup))|[PickupVariant](../PickupVariant) |

### MC_POST_PICKUP_UPDATE {: .copyable } 
Returning any value will have no effect on later callback executions.

???- info "Execution informations"
    This callback will be called on the 1st frame that the entity exists. It will only be called on the 0th frame, when you enter a room that already contains a spawned pickup. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|35 |MC_POST_PICKUP_UPDATE {: .copyable } | ([EntityPickup](../../EntityPickup))|[PickupVariant](../PickupVariant) |

### MC_POST_PICKUP_RENDER {: .copyable } 
Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|36 |MC_POST_PICKUP_RENDER {: .copyable } | ([EntityPickup](../../EntityPickup),<br>RenderOffset [Vector])|[PickupVariant](../PickupVariant) |

### MC_POST_PICKUP_SELECTION {: .copyable } 
Called after a Pickup was choosen from a list of random pickups to be spawned.Return nil to continue with default game code. 

Return a table `{ Variant, Subtype }` to override the specified values. This does also affect later executed callbacks.

???+ bug
    Returning a value that is not a table or nil will cause the game to crash.
    
???+ warning "Warning"
    The last callback to return a valid return value wins out and overwrites previous callbacks' return values 

???+ bug
    [EntityPickup](../../EntityPickup) does contain the Type/variant of the pickup to spawn, but is otherwise an empty class with empty / zeroed values.

    This Callback is also called when entering a room that contains pickups that are already selected. It is also called when the player drops a card. Those facts make this callback useless to use for handling pickup pools. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|37 |MC_POST_PICKUP_SELECTION {: .copyable } | ([EntityPickup](../../EntityPickup),<br>Variant [int],<br>Subtype [int]) | - |

### MC_PRE_PICKUP_COLLISION {: .copyable } 
The Low value is true, when the entity collided with the collider first. Its false if the collider collides first.

Return true to ignore collision, false to collide but not execute internal code and nil to continue with internal code (example: taking damage on contact). 

???+ bug
    This Callback can only be used ONCE across all mods! It is highly recommended to not use this Callback without defining an [PickupVariant](../PickupVariant) unless its absolutely nessesary! 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|38 |MC_PRE_PICKUP_COLLISION {: .copyable } | ([EntityPickup](../../EntityPickup),<br>Collider [[Entity](../../Entity)],<br>Low [bool])|[PickupVariant](../PickupVariant) |

### MC_POST_TEAR_INIT {: .copyable } 
Returning any value will have no effect on later callback executions.

???+ bug
    This Callback provides incomplete data in the [EntityTear](../../EntityTear) attribute. For example, the Position is always equal to Vector(0,0). 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|39 |MC_POST_TEAR_INIT {: .copyable } | ([EntityTear](../../EntityTear))|[TearVariant](../TearVariant) |

### MC_POST_TEAR_UPDATE {: .copyable } 
Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|40 |MC_POST_TEAR_UPDATE {: .copyable } | ([EntityTear](../../EntityTear))|[TearVariant](../TearVariant) |

### MC_POST_TEAR_RENDER {: .copyable } 
Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|41 |MC_POST_TEAR_RENDER {: .copyable } | ([EntityTear](../../EntityTear),<br>RenderOffset [Vector])|[TearVariant](../TearVariant) |

### MC_PRE_TEAR_COLLISION {: .copyable } 
The Low value is true, when the entity collided with the collider first. Its false if the collider collides first.

Return true to ignore collision, false to collide but not execute internal code and nil to continue with internal code (example: taking damage on contact). 

???+ bug
    This Callback can only be used ONCE across all mods! It is highly recommended to not use this Callback without defining an [PickupVariant](../PickupVariant) unless its absolutely nessesary! 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|42 |MC_PRE_TEAR_COLLISION {: .copyable } | ([EntityTear](../../EntityTear),<br>Collider [[Entity](../../Entity)],<br>Low [bool])|[TearVariant](../TearVariant) |

### MC_POST_PROJECTILE_INIT {: .copyable } 
Returning any value will have no effect on later callback executions.

???+ bug
    This Callback provides incomplete data in the [EntityProjectile](../../EntityProjectile) attribute. For example, the Position is always equal to Vector(0,0). 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|43 |MC_POST_PROJECTILE_INIT {: .copyable } | ([EntityProjectile](../../EntityProjectile))|[ProjectileVariant](../ProjectileVariant) |

### MC_POST_PROJECTILE_UPDATE {: .copyable } 
Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|44 |MC_POST_PROJECTILE_UPDATE {: .copyable } | ([EntityProjectile](../../EntityProjectile))|[ProjectileVariant](../ProjectileVariant) |

### MC_POST_PROJECTILE_RENDER {: .copyable } 
Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|45 |MC_POST_PROJECTILE_RENDER {: .copyable } | ([EntityProjectile](../../EntityProjectile),<br>RenderOffset [Vector])|[ProjectileVariant](../ProjectileVariant) |

### MC_PRE_PROJECTILE_COLLISION {: .copyable } 
The Low value is true, when the entity collided with the collider first. Its false if the collider collides first.

Return true to ignore collision, false to collide but not execute internal code and nil to continue with internal code (example: taking damage on contact). 

???+ bug
    This Callback can only be used ONCE across all mods! It is highly recommended to not use this Callback without defining an [ProjectileVariant](../ProjectileVariant) unless its absolutely nessesary! 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|46 |MC_PRE_PROJECTILE_COLLISION {: .copyable } | ([EntityProjectile](../../EntityProjectile),<br>Collider [[Entity](../../Entity)],<br>Low [bool])|[ProjectileVariant](../ProjectileVariant) |

### MC_POST_LASER_INIT {: .copyable } 
Returning any value will have no effect on later callback executions.

???+ bug
    This Callback provides incomplete data in the [EntityLaser](../../EntityLaser) attribute. For example, the Position is always equal to Vector(0,0). 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|47 |MC_POST_LASER_INIT {: .copyable } | ([EntityLaser](../../EntityLaser))|LaserVariant |

### MC_POST_LASER_UPDATE {: .copyable } 
Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|48 |MC_POST_LASER_UPDATE {: .copyable } | ([EntityLaser](../../EntityLaser))|LaserVariant |

### MC_POST_LASER_RENDER {: .copyable } 
Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|49 |MC_POST_LASER_RENDER {: .copyable } | ([EntityLaser](../../EntityLaser),<br>RenderOffset [Vector])|LaserVariant |

### MC_POST_KNIFE_INIT {: .copyable } 
Returning any value will have no effect on later callback executions.


???+ note
    The optional parameter is a SubType and **NOT** a Variant!
    
???+ bug
    This Callback provides incomplete data in the [EntityKnife](../../EntityKnife) attribute. For example, the Position is always equal to Vector(0,0). 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|50 |MC_POST_KNIFE_INIT {: .copyable } | ([EntityKnife](../../EntityKnife))|KnifeSubType * |

### MC_POST_KNIFE_UPDATE {: .copyable } 
Returning any value will have no effect on later callback executions.

???+ note
    The optional parameter is a SubType and **NOT** a Variant! 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|51 |MC_POST_KNIFE_UPDATE {: .copyable } | ([EntityKnife](../../EntityKnife))|KnifeSubType * |

### MC_POST_KNIFE_RENDER {: .copyable } 
Returning any value will have no effect on later callback executions.

???+ note
    The optional parameter is a SubType and **NOT** a Variant! 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|52 |MC_POST_KNIFE_RENDER {: .copyable } | ([EntityKnife](../../EntityKnife),<br>RenderOffset [Vector])|KnifeSubType * |

### MC_PRE_KNIFE_COLLISION {: .copyable } 
The Low value is true, when the entity collided with the collider first. Its false if the collider collides first.

Return true to ignore collision, false to collide but not execute internal code and nil to continue with internal code (example: taking damage on contact).

???+ note
    The optional parameter is a SubType and **NOT** a Variant! 

???+ bug   
    This Callback can only be used ONCE across all mods! It is highly recommended to not use this Callback without defining an KnifeSubType unless its absolutely nessesary! 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|53 |MC_PRE_KNIFE_COLLISION {: .copyable } | ([EntityKnife](../../EntityKnife),<br>Collider [[Entity](../../Entity)],<br>Low [bool])|KnifeSubType * |

### MC_POST_EFFECT_INIT {: .copyable } 
Returning any value will have no effect on later callback executions.

???+ bug
    This Callback provides incomplete data in the [EntityEffect](../../EntityEffect) attribute. For example, the Position is always equal to Vector(0,0). 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|54 |MC_POST_EFFECT_INIT {: .copyable } | ([EntityEffect](../../EntityEffect))|[EffectVariant](../EffectVariant) |

### MC_POST_EFFECT_UPDATE {: .copyable } 
Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|55 |MC_POST_EFFECT_UPDATE {: .copyable } | ([EntityEffect](../../EntityEffect))|[EffectVariant](../EffectVariant) |

### MC_POST_EFFECT_RENDER {: .copyable } 
Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|56 |MC_POST_EFFECT_RENDER {: .copyable } | ([EntityEffect](../../EntityEffect),<br>RenderOffset [Vector])|[EffectVariant](../EffectVariant) |

### MC_POST_BOMB_INIT {: .copyable } 
Returning any value will have no effect on later callback executions.

???+ bug
    This Callback provides incomplete data in the [EntityBomb](../../EntityBomb) attribute. For example, the Position is always equal to Vector(0,0). 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|57 |MC_POST_BOMB_INIT {: .copyable } | ([EntityBomb](../../EntityBomb))|[BombVariant](../BombVariant) |

### MC_POST_BOMB_UPDATE {: .copyable } 
Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|58 |MC_POST_BOMB_UPDATE {: .copyable } | ([EntityBomb](../../EntityBomb))|[BombVariant](../BombVariant) |

### MC_POST_BOMB_RENDER {: .copyable } 
Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|59 |MC_POST_BOMB_RENDER {: .copyable } | ([EntityBomb](../../EntityBomb),<br>Offset [Vector])|[BombVariant](../BombVariant) |

### MC_PRE_BOMB_COLLISION {: .copyable } 
The Low value is true, when the entity collided with the collider first. Its false if the collider collides first.

Return true to ignore collision, false to collide but not execute internal code and nil to continue with internal code (example: taking damage on contact).

???+ bug
    This Callback can only be used ONCE across all mods! It is highly recommended to not use this Callback unless its absolutely nessesary! 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|60 |MC_PRE_BOMB_COLLISION {: .copyable } | ([EntityBomb](../../EntityBomb),<br>Collider [[Entity](../../Entity)],<br>Low [bool])|[BombVariant](../BombVariant) |

### MC_POST_FIRE_TEAR {: .copyable } 
Called when the player fires a tear.

It is not called for other weapons or tears fired with Incubus.

Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|61 |MC_POST_FIRE_TEAR {: .copyable } | ([EntityTear](../../EntityTear)) | - |

### MC_PRE_GET_COLLECTIBLE {: .copyable } 


This callback is called when the game needs to get a new random item from an item pool.

You can return an integer from this callback in order to change the returned collectible type.

It is not called for "scripted" drops (like Mr. Boom from Wrath) and manually spawned items.

Returned values will not alter args of later executed callbacks.

???+ bug
    Returning a value that is not a table or nil will cause the game to crash.
    
???+ warning "Warning"
    The last callback to return a valid return value wins out and overwrites previous callbacks' return values 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|62 |MC_PRE_GET_COLLECTIBLE {: .copyable } | ([ItemPoolType](../ItemPoolType),<br>Decrease [bool],<br>Seed [int]) | - |

### MC_POST_GET_COLLECTIBLE {: .copyable } 
This function is called right after MC_PRE_GET_COLLECTIBLE and determines the Collectible that will be spawned from the given [ItemPoolType](../ItemPoolType).

You can return an integer from this callback in order to change the returned collectible type.

Returned values will not update the "SelectedCollectible" arg of later executed callbacks.

???+ bug
    Returning a value that is not a table or nil will cause the game to crash.
    
???+ warning "Warning"
    The last callback to return a valid return value wins out and overwrites previous callbacks' return values 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|63 |MC_POST_GET_COLLECTIBLE {: .copyable } | (SelectedCollectible [[CollectibleType](../CollectibleType)],<br>[ItemPoolType](../ItemPoolType),<br>Decrease [bool],<br>Seed [int]) | - |

### MC_GET_PILL_COLOR {: .copyable } 

This function is called, when the game is spawning a pill and needs to determine its PillColor.

Return a PillColor to specify a Pillcolor that needs to be choosen. Return nothing to let it be handled by the game.

Returned values will not alter the args of later executed callbacks.

???+ bug
    Returning a value that is not a table or nil will cause the game to crash.
    
???+ warning "Warning"
    The last callback to return a valid return value wins out and overwrites previous callbacks' return values 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|64 |MC_GET_PILL_COLOR {: .copyable } | (Seed [int]) | - |

### MC_GET_PILL_EFFECT {: .copyable } 
Called every frames when the game get the [PillEffect](../PillEffect) of a pill. The effect of the pill can be choosed by returning the chosen [PillEffect](../PillEffect).

The effect is applied to every pill of the same PillColor, not to a single pill.

Returned values will not update the "SelectedPillEffect" arg of later executed callbacks.

???+ bug
    Returning a value that is not a table or nil will cause the game to crash.
    
???+ warning "Warning"
    The last callback to return a valid return value wins out and overwrites previous callbacks' return values 

???- example "Example code"
    This code turn "Bad Trip" pills into "Balls of Steel" pills.
    ```lua
    function mod:getPillEffect(pillEffect, pillColor)
        if pillEffect == PillEffect.PILLEFFECT_BAD_TRIP then
        return PillEffect.PILLEFFECT_BALLS_OF_STEEL
        end
    end
    mod:AddCallback(ModCallbacks.MC_GET_PILL_EFFECT, mod.getPillEffect) 
    ```

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|65 |MC_GET_PILL_EFFECT {: .copyable } | (SelectedPillEffect [[PillEffect](../PillEffect)],<br>PillColor) | - |

### MC_GET_TRINKET {: .copyable } 
Called when a [TrinketType](../TrinketType) of a Trinket needs to be determined. 

A [TrinketType](../TrinketType) can be returned to change the SelectedTrinket.

Returned values will not update the "SelectedTrinket" arg of later executed callbacks.

???+ bug
    Returning a value that is not a table or nil will cause the game to crash.
    
???+ warning "Warning"
    The last callback to return a valid return value wins out and overwrites previous callbacks' return values 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|66 |MC_GET_TRINKET {: .copyable } | (SelectedTrinket [[TrinketType](../TrinketType)],<br>[RNG](../../RNG)) | - |

### MC_POST_ENTITY_REMOVE {: .copyable } 
Called whenever an [Entity](../../Entity) gets removed by the game. This includes deaths, kills, removals and even unloading an entity on room transition or ending a run.

Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|67 |MC_POST_ENTITY_REMOVE {: .copyable } | ([Entity](../../Entity))|[EntityType](../EntityType) |

### MC_POST_ENTITY_KILL {: .copyable } 
Called right before a death animation is triggered for an [Entity](../../Entity).

Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|68 |MC_POST_ENTITY_KILL {: .copyable } | ([Entity](../../Entity))|[EntityType](../EntityType) |

### MC_PRE_NPC_UPDATE {: .copyable } 
Return true if the internal AI of an NPC should be ignored, false or nil/nothing otherwise.

???+ bug
    This Callback can only be used ONCE across all mods! It is highly recommended to not use this Callback unless its absolutely nessesary! 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|69 |MC_PRE_NPC_UPDATE {: .copyable } | ([EntityNPC](../../EntityNPC)) |[EntityType](../EntityType) |

### MC_PRE_SPAWN_CLEAN_AWARD {: .copyable } 
This function is triggered in every room that can be cleared, including boss and angel rooms, and even when it normally would not spawn a reward.

This Callback also handles special spawns like the spawning of Trapdoors after a boss is killed, therefore returning true here will also cancel those events.

Return true if the spawn routine should be ignored, false or nil/nothing otherwise.

???+ bug
    This Callback can only be used ONCE across all mods! It is highly recommended to not use this Callback unless its absolutely nessesary! 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|70 |MC_PRE_SPAWN_CLEAN_AWARD {: .copyable } | ([RNG](../../RNG),<br>SpawnPosition [Vector]) | - |

### MC_PRE_ROOM_ENTITY_SPAWN {: .copyable } 
This is called when entering a new room, before spawning entities which are part of its layout. Grid entities will also trigger this callback and their type will the same as the type used by the gridspawn command. Because of this, effects are assigned the type 999 instead of 1000 in this callback. 

Optional: Return a table with new values { Type, Variant, Subtype }. Returning such a table will override any replacements that might naturally occur i.e. enemy variants.

Returning any value will have no effect on later callback executions. 

|DLC|Value|Name|Function Args| Optional Args|
|:--|:--|:--|:--|:--|
|[ ](#){: .abrep .tooltip .badge }|71 |MC_PRE_ROOM_ENTITY_SPAWN {: .copyable } | ([EntityType](../EntityType),<br>Variant [int],<br>SubType [int],<br>GridIndex [int],<br>Seed [int]) | - |
