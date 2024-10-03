Class **_Signal** provides some information about signals, installed on the ship.

You can get object of this type from ship by this way:

    vehicle = battle.getSelfPlayerShip()
    signals = vehicle.getSignals() # returns list of _Signal objects

### Athributes

- id - int
- sortOrder - int
- iconPath - path to icon, str
