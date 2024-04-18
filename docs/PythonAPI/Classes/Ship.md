Class **Ship** provides some information about players ship.

You can get object of this type by following functions:

    battle.getAllShips()
    battle.getSelfPlayerShip()
    battle.getObserverShip()
    battle.getTorpedoOwnerById(ownerId)

### Athributes:

- uiId -int, id of the ship iu element
- teamId - int
- isPlayer - bool
- subtype - str
- isBot - bool
- name - str
- playerName - str

### Methods:

- [getTorpedoesModulesState()](#getTorpedoesModulesState)
- [getArtilleryModulesState()](#getArtilleryModulesState)
- [getConsumablesState()](#getConsumablesState)
- [getHealthData()](#getHealthData)
- [getRadarInfo()](#getRadarInfo)
- [getHydroAcousticSearchInfo()](#getHydroAcousticSearchInfo)
- [getSubmarineLocatorInfo()](#getSubmarineLocatorInfo)
- [getPosition()](#getPosition)
- [isAlive()](#isAlive)
- [getModernizations()](#getModernizations)
- [getCommanderSkills()](#getCommanderSkills)

---

### getTorpedoesModulesState()

This function returns list of [_ModuleState](./_ModuleState.md) objects for ships torpedoes modules.

#### Returns
- list of objects [_ModuleState](./_ModuleState.md)

#### Example

 	vehicle = battle.getSelfPlayerShip()
	torpedoesModulesStates = vehicle.getTorpedoesModulesState()

---

### getTorpedoesModulesState()

This function returns list of [_ModuleState](./_ModuleState.md) objects for ship guns.

#### Returns
- list of objects [_ModuleState](./_ModuleState.md)

#### Example

 	vehicle = battle.getSelfPlayerShip()
	artilleryModulesStates = vehicle.getArtilleryModulesState()

---

### getConsumablesState()

This function returns list of [_ConsumableState](./_ConsumableState.md) objects for ship.

#### Returns
- list of objects [_ConsumableState](./_ConsumableState.md)

#### Example

 	vehicle = battle.getSelfPlayerShip()
	consumablesState = vehicle.getConsumablesState()

---

### getHealthData()

This function returns [_HealthData](./_HealthData.md) object for ship.

#### Returns
- object [_HealthData](./_HealthData.md)

#### Example

 	vehicle = battle.getSelfPlayerShip()
	healthData = vehicle.getHealthData()

---

### getRadarInfo()

This function returns [_SearchConsumableInfo](./_SearchConsumableInfo.md) object for ship's radar (RLS).
Returns None if consumable is not installed on the ship.

#### Returns
- object [_SearchConsumableInfo](./_SearchConsumableInfo.md) or None

#### Example

 	vehicle = battle.getSelfPlayerShip()
	radarInfo = vehicle.getRadarInfo()

---

### getHydroAcousticSearchInfo()

This function returns [_SearchConsumableInfo](./_SearchConsumableInfo.md) object for ship's Hydro Acoustic Search.
Returns None if consumable is not installed on the ship.

#### Returns
- object [_SearchConsumableInfo](./_SearchConsumableInfo.md) or None

#### Example

 	vehicle = battle.getSelfPlayerShip()
	hydroAcousticSearchInfo = vehicle.getHydroAcousticSearchInfo()

---

### getSubmarineLocatorInfo()

This function returns [_SearchConsumableInfo](./_SearchConsumableInfo.md) object for ship's Submarine Locator.
Returns None if consumable is not installed on the ship.

#### Returns
- object [_SearchConsumableInfo](./_SearchConsumableInfo.md) or None

#### Example

 	vehicle = battle.getSelfPlayerShip()
	submarineLocatorInfo = vehicle.getSubmarineLocatorInfo()

---

### getPosition()

Return ship's current position.

#### Returns
- object Math.Vector3

#### Example

 	vehicle = battle.getSelfPlayerShip()
	position = vehicle.getPosition()

---

### isAlive()

Return ship's alive condition.

#### Returns
- true or false

#### Example

 	vehicle = battle.getSelfPlayerShip()
	isAlive = vehicle.isAlive()

---

### getModernizations()

This function returns list of [_Modernization](./_Modernization.md) objects for ship.

#### Returns
- list of objects [_Modernization](./_Modernization.md)

#### Example

 	vehicle = battle.getSelfPlayerShip()
	modernizations = vehicle.getModernizations()

---

### getCommanderSkills()

This function returns list of [_CommanderSkill](./_CommanderSkill.md) objects for ship.

#### Returns
- list of objects [_CommanderSkill](./_CommanderSkill.md)

#### Example

 	vehicle = battle.getSelfPlayerShip()
	commanderSkills = vehicle.getCommanderSkills()

---
