Class **_HealthData** provides some information about current health of any ship.

You can get object of this type from ship by this way:

    vehicle = battle.getSelfPlayerShip()
    healthData = vehicle.getHealthData() # returns list of _HealthData objects

### Athributes

- regenPerUsage - float
- regenWorkTime - float
- regenNum - int
- regenWorkTimeLeft - float
- regenerationHealth - float
- maxHealth - float
- health - health
