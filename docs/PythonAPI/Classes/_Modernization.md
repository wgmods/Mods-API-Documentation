Class **_Modernization** provides some information modernizations, installed on the ship.

You can get object of this type from ship by this way:

    vehicle = battle.getSelfPlayerShip()
    modernizations = vehicle.getModernizations() # returns list of _Modernization objects

### Athributes

- type - str
- slotNumber - int
- iconPath - path to icon, string
