Class **_ConsumableState** provides some information about state of any ship's consumables.

You can get object of this type from ship by this way:

    vehicle = battle.getSelfPlayerShip()
    consumablesState = vehicle.getConsumablesState() # returns list of _ConsumableState objects

### Athributes

- icon - path to icon, str
- num - number of consumables, int
- currentState - int
- endTime - float
