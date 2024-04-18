Class **_ModuleState** provides some information about state of any ship's module

You can get object of this type from ship by this way:

    vehicle = battle.getSelfPlayerShip()
    torpedoesModulesStates = vehicle.getTorpedoesModulesState() # returns list of _ModuleState objects
    artilleryModulesStates = vehicle.ArtilleryModulesState() # returns list of _ModuleState objects

### Athributes

- type - str
- currentHP - float
- maxHP - float
- state - int
- critTimer - float
- position - Vector(x,y,z)
