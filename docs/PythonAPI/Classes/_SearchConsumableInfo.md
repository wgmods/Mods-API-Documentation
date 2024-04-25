#### Note
*Will be able from client version 13.5 !* 

Class **_SearchConsumableInfo** provides some information about state of any ship's search consumable.

You can get object of this type from ship by this way:

    vehicle = battle.getSelfPlayerShip()
    radarInfo = vehicle.getRadarInfo() # returns list of _SearchConsumableInfo objects
    hydroAcousticSearchInfo = vehicle.getHydroAcousticSearchInfo() # returns list of _SearchConsumableInfo objects
    submarineLocatorInfo = vehicle.getSubmarineLocatorInfo() # returns list of _SearchConsumableInfo objects

### Athributes

- distShip - float
- state - int
- workTimeLeft - float
