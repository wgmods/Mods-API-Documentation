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

---

### getTorpedoesModulesState()

This function returns list of [Player](./Classes/Player.md) objects.

#### Returns
- list of objects [Player](./Classes/Player.md)

#### Example

 	vehicle = battle.getSelfPlayerShip()
	torpedoesModulesStates = vehicle.getTorpedoesModulesState()

---


#### Input parameters
- ownerId - torpedo owner Id

getTorpedoesModulesState(self)
Returns list of ModuleState objects for ship torpedoes.

ModuleState contains fields:

type
currentHP
maxHP
state
critTimer
position

getArtilleryModulesState()
Returns list of ModuleState objects for ship guns.

getConsumablesState()
Returns list of ConsumableState objects for ship consumables.

ConsumableState contains fields:

icon - str
num - int
currentState
endTime

getHealthData()
Returns HealthData object for ship.

HealthData contains fields:

regenPerUsage
regenWorkTime - float
regenNum - int
regenWorkTimeLeft
regenerationHealth
maxHealth
health

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


