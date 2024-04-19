Working with **battle** methods is only possible after entering a battle (for a situation when an event is triggered, see the "events" methods), otherwise methods do not return anything as information they handle is only available in battle. 

To handle events you need to use **events.onSFMEvent** (see the description below in the "events" methods), returned parameters of this event are "eventName" (an event name), "eventData" (a dict with event parameters).

## Available methods:

- [getPlayersInfo()](#getPlayersInfo)
- [getPlayerInfo(playerID)](#getPlayerInfoplayerID)
- [getSelfPlayerInfo()](#getSelfPlayerInfo)
- [getPlayerInfoByName(name)](#getPlayerInfoByNamename)
- [getPlayerShipInfo(playerID)](#getPlayerShipInfoplayerID)
- [getPlayerByVehicleId(shipID)](#getPlayerByVehicleIdshipID)
- [getAmmoParams(ammoID)](#getAmmoParamsammoID)
- [isVehicleBurning(shipID)](#isVehicleBurningshipID)
- [isVehicleFlooding(shipID)](#isVehicleFloodingshipID)
- [isBattleStarted()](#isBattleStarted)
- [cameraAltVision()](#cameraAltVision)
- [isObserverMode()](#isObserverMode)
- [getConsumableState(vehicleId, consumableType)](#getConsumableStatevehicleId-consumableType)
- [getConsumableNumber(vehicleId, consumableType)](#getConsumableNumbervehicleId-consumableType)
- [getDistanceInMeters(start, end)](#getDistanceInMetersstart-end)
- [getLearnedCrewSkills()](#getLearnedCrewSkills)
- [getSelfPlayer()](#getSelfPlayer)
- [getSelfPlayerShip()](#getSelfPlayerShip)
- [getObserverShip()](#getObserverShip)
- [getTorpedoOwnerById(ownerId)](#getTorpedoOwnerByIdownerId)
- [getAllShips()](#getAllShips)
- [getAllTorpedoes()](#getAllTorpedoes)
- [playOnAttentionSound()](#playOnAttentionSound)
- [getBattleStatistics()](#getBattleStatistics)
- [getSmokeScreens()](#getSmokeScreens)
- [getNearestEnemyIndication()](#getNearestEnemyIndication)

---

### getPlayersInfo()
This function returns a dict, where keys are "playerID", and values are dict "PlayerInfo" with various information about the player.
To view the result, you can pass it to the "World_of_Warships\profile\python.log" file via "print", or write it in a separate file "open('filename', 'w')".

![image](https://github.com/wgmods/Mods-API-Documentation/assets/167185926/be7eeaca-9e6b-4d75-a878-f4500789a862)

![image](https://github.com/wgmods/Mods-API-Documentation/assets/167185926/486b4d27-f7f9-4f34-985f-52b7930ad7cf)

---

### getPlayerInfo(playerID)
This function returns an object with player information.

#### Input parameters
- playerId - the player’s ID

#### Returns
- PlayerInfo object

---

### getSelfPlayerInfo()
This function returns an object with information about the player. The returned value is PlayerInfo.

#### Returns
- PlayerInfo object

---

### getPlayerInfoByName(name)
This function returns an object with information about the player.

#### Input parameters
- name - the player’s nickname

#### Returns
- PlayerInfo object

---

### getPlayerShipInfo(playerID)
This function returns an object with information about the player’s ship.

#### Input parameters
- playerId - the player’s ID

#### Returns
- ShipInfo object

---

### getPlayerByVehicleId(shipID)
This function returns an object with information about the player.

#### Input parameters
- shipId - the ship’s ID

#### Returns
- PlayerInfo object

---

### getAmmoParams(ammoID)
This function returns an object with information about the shell.

#### Input parameters
- ammoId - the shell ID, this value can be obtained in the event handler function "events.onReceiveShellInfo(func)" (see the description in the "events" methods).

#### Returns
- object

---

### isVehicleBurning(shipID)
This function returns True if the ship is on fire, or False if it isn’t; for example, you can use it in the event handler function "events.onReceiveShellInfo(func)" (see the description in the "events" methods).

#### Input parameters
- shipID - the ship's ID

#### Returns
- true or false

---

### isVehicleFlooding(shipID)
This function returns True if a shell hitting the ship caused flooding, or False if it’s not the case; it is recommended to use it in the same way as "isVehicleBurning".

#### Input parameters
- shipID - the ship's ID

#### Returns
- true or false

---

### isBattleStarted()
This function returns True if the battle has started.

#### Returns
- true or false

---

### cameraAltVision()
This function returns True if Alt key pressed in the battle.

#### Returns
- true or false

---

### isObserverMode()
This function returns True if player enters into the training room as Observer.

#### Returns
- true or false

---

### getConsumableState(vehicleId, consumableType)

This function returns the required consumable state.

#### Input parameters
- vehicleId - the vehicle’s ID
- consumableType - type of consumable:
  - CONSUMABLE_CRASH_CREW       = 0
  - CONSUMABLE_SCOUT            = 1
  - CONSUMABLE_AIR_DEFENSE_DISP = 2
  - CONSUMABLE_SPEED_BOOSTER    = 3
  - CONSUMABLE_TA_BOOSTER       = 4 deprecated
  - CONSUMABLE_MB_BOOSTER       = 5
  - CONSUMABLE_HANGAR_BOOSTER   = 6
  - CONSUMABLE_SMOKE_GENERATOR  = 7
  - CONSUMABLE_REGEN_CREW       = 9
  - CONSUMABLE_FIGHTER          = 10
  - CONSUMABLE_SONAR            = 11
  - CONSUMABLE_TA_RELOADER      = 12
  - CONSUMABLE_RLS              = 13

#### Returns
- consumable state:
  - READY = 0
  - SELECTED = 1
  - AT_WORK = 2
  - RELOAD = 3
  - NO_AMMO = 4
  - PREPARATION = 5

---

### getConsumableNumber(vehicleId, consumableType)

This function returns the required consumable number.

#### Input parameters
- vehicleId - the vehicle’s ID
- consumableType - type of consumable:
  - CONSUMABLE_CRASH_CREW       = 0
  - CONSUMABLE_SCOUT            = 1
  - CONSUMABLE_AIR_DEFENSE_DISP = 2
  - CONSUMABLE_SPEED_BOOSTER    = 3
  - CONSUMABLE_TA_BOOSTER       = 4 deprecated
  - CONSUMABLE_MB_BOOSTER       = 5
  - CONSUMABLE_HANGAR_BOOSTER   = 6
  - CONSUMABLE_SMOKE_GENERATOR  = 7
  - CONSUMABLE_REGEN_CREW       = 9
  - CONSUMABLE_FIGHTER          = 10
  - CONSUMABLE_SONAR            = 11
  - CONSUMABLE_TA_RELOADER      = 12
  - CONSUMABLE_RLS              = 13

#### Returns
- int

---

### getDistanceInMeters(start, end)

This function returns the distance in meters between two points in 3D space.

#### Input parameters
- start - start point, tuple(x, y, z)
- end - end point, tuple(x, y, z)

#### Returns
- float

---

### getLearnedCrewSkills()

This function returns the list with player's commander leaned skills names.
If player has no vehicle (observer), returns None.

#### Input parameters
- start - start point, tuple(x, y, z)
- end - end point, tuple(x, y, z)

#### Returns
- list or None

---

### getSelfPlayer()

This function returns the [Player](./Classes/Player.md) object.

#### Returns
- object [Player](./Classes/Player.md)

---

### getSelfPlayerShip()

This function returns the self player's [Ship](./Classes/Ship.md) object.

#### Returns
- object [Ship](./Classes/Ship.md)

---

### getObserverShip()

This function returns the observers's [Ship](./Classes/Ship.md) object (wich nearest to the screen center in observer mode).

#### Returns
- object [Ship](./Classes/Ship.md)

---

### getTorpedoOwnerById(ownerId)

This function returns the [Player](./Classes/Player.md) object by torpedo owner Id.

#### Input parameters
- ownerId - torpedo owner Id

#### Returns
- object [Player](./Classes/Player.md)

#### Example

 	torpedoes = battle.getAllTorpedoes()
	for torp in torpedoes:
		torpedoOwner = battle.getTorpedoOwnerById(torp.ownerId) 

---

### getAllShips()

This function returns list of all visible [Ship](./Classes/Ship.md) objects in battle.

#### Returns
- list of [Ship](./Classes/Ship.md) objects

#### Example

 	visibleShips = battle.getAllShips()

---

### getAllTorpedoes()

This function returns list of all visible [Torpedo](./Classes/Torpedo.md) objects in battle.

#### Returns
- list of [Torpedo](./Classes/Torpedo.md) objects

#### Example

 	visibleTorpedoes = battle.getAllTorpedoes()

---

### playOnAttentionSound()

This function plays OnAttention sound.

---

### getBattleStatistics()

This function returns [BattleStatistics](./Classes/BattleStatistics.md) objects in battle.

#### Returns
- [BattleStatistics](./Classes/BattleStatistics.md) objects

#### Example

 	battleStatistics = battle.BattleStatistics()

---

### getSmokeScreens()

This function returns list of all visible [SmokeScreen](./Classes/SmokeScreen.md) objects in battle.

#### Returns
- list of [SmokeScreen](./Classes/SmokeScreen.md) objects

#### Example

 	smokeScreens = battle.getSmokeScreens()

---

### getNearestEnemyIndication()

This function returns the [NearestEnemyIndication](./Classes/NearestEnemyIndication.md) object.

#### Returns
- object [NearestEnemyIndication](./Classes/NearestEnemyIndication.md)

#### Example

 	nearestEnemyIndication = battle.getNearestEnemyIndication() 

---
