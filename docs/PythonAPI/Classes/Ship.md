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
- list of objects [_HealthData](./_HealthData.md)

#### Example

 	vehicle = battle.getSelfPlayerShip()
	healthData = vehicle.getHealthData()

---


getRadarInfo()
Returns RadarInfo object for ship.

RadarInfo contains fields:

distShip - int
state - int
workTimeLeft - int

getPosition()
Returns current ship position (Math.Vector3).

isAlive()
Returns True if ship is alive.

getHydroAcousticSearchInfo()
        Return class with ship's hydro acoustic search info:

distShip - int
state - int
workTimeLeft - int

        Example:
        vehicle = battle.getSelfPlayerShip()
        radarInfo = vehicle.getHydroAcousticSearchInfo()

getSubmarineLocatorInfo()
        Return class with ship's submarine locator info (underwater search):

distShip - int
state - int
workTimeLeft - int

        Example:
        vehicle = battle.getSelfPlayerShip()
        submarineLocatorInfo = vehicle.getSubmarineLocatorInfo()

getModernizations()
        Return list of ship's modernizations. Each modernization contains fields:

type - int
slotNumber - int
iconPath - str

        Example:
        vehicle = battle.getSelfPlayerShip()
        modernizations = vehicle.getModernizations()

getCommanderSkills()
       Return list of ship commander's skills. Each skill contains fields:

name - str
isLearned - bool
isEpic - bool

iconPath - str

        Example:
        vehicle = battle.getSelfPlayerShip()
        commanderSkills = vehicle.getCommanderSkills()


