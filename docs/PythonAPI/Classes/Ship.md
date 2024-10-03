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
- [isAlive()](#isAlive)
- [getModernizations()](#getModernizations)
- [getSignals()](#getSignals)
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
The length of list is equal of max number of modernizations for this ship.
If there is no modernization installed in some slot, there will be None in this list position.

#### Returns
- list of objects [_Modernization](./_Modernization.md) or None, if this data is not allowed for this current ship.

#### Example

 	vehicle = battle.getSelfPlayerShip()
	modernizations = vehicle.getModernizations()

---

### getSignals()

This function returns list of [_Signal](./_Signal.md) objects for ship.
The length of list is equal of max number of signals.
If there is no signal installed in some slot, there will be None in this list position.

#### Returns
- list of objects [_Signal](./_Signal.md) or None, if this data is not allowed for this current ship.

#### Example

 	vehicle = battle.getSelfPlayerShip()
	signals = vehicle.getSignals()

---

### getCommanderSkills()

This function returns list with four lists of [_CommanderSkill](./_CommanderSkill.md) objects for ship.
Each of the inner lists corresponds to the skill level of the commander.

#### Returns
- list

#### Example

 	vehicle = battle.getSelfPlayerShip()
	commanderSkills = vehicle.getCommanderSkills()
 		for skillsRaw in commanderSkills:
                    for skill in skillsRaw:
		        # do something with skill

---
