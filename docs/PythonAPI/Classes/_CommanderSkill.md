#### Note
*Will be able from client version 13.5 !* 

Class **_CommanderSkill** provides some information about leaned skills of ship's commander.

You can get object of this type from ship by this way:

    vehicle = battle.getSelfPlayerShip()
    commanderSkills = vehicle.getCommanderSkills() # returns list of _CommanderSkill objects

### Athributes

- name - str
- isLearned - bool
- isEpic - bool
- iconPath - path to icon, str
