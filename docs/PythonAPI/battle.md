Working with "battle" methods is only possible after entering a battle (for a situation when an event is triggered, see the "events" methods), otherwise methods do not return anything as information they handle is only available in battle. To handle events you need to use "events.onSFMEvent" (see the description below in the "events" methods), returned parameters of this event are "eventName" (an event name), "eventData" (a dict with event parameters).

## Available methods:

- [getPlayersInfo()](#getPlayersInfo)
- [getPlayerInfo(playerID)](#getPlayerInfoplayerID)
- [getSelfPlayerInfo()](#getSelfPlayerInfo)
- [getPlayerInfoByName(name)](#getPlayerInfoByNamename)
- [getPlayerShipInfo(playerID)](#getPlayerShipInfoplayerID)
- [getPlayerByVehicleId(shipID)](#getPlayerByVehicleIdshipID)
- [getAmmoParams(ammoID)](#getAmmoParamsammoID)
- [isVehicleBurning(shipID)](#isVehicleBurningshipID)
- [isVehicleFlooding(shipID)](#isVehicleFloodingshipID)
- [isBattleStarted()](#isBattleStarted)
- [cameraAltVision()](#cameraAltVision)
- [isObserverMode()](#isObserverMode)

### getPlayersInfo()
This function returns a dict, where keys are "playerID", and values are dict "PlayerInfo" with various information about the player.
To view the result, you can pass it to the "World_of_Warships\profile\python.log" file via "print", or write it in a separate file "open('filename', 'w')".

![image](https://github.com/wgmods/Mods-API-Documentation/assets/167185926/be7eeaca-9e6b-4d75-a878-f4500789a862)

![image](https://github.com/wgmods/Mods-API-Documentation/assets/167185926/486b4d27-f7f9-4f34-985f-52b7930ad7cf)

---

### getPlayerInfo(playerID)
This function returns an object with player information.

#### Input parameters
- playerId - the player’s ID

#### Returns
- PlayerInfo object

---

### getSelfPlayerInfo()
This function returns an object with information about the player. The returned value is PlayerInfo.

#### Returns
- PlayerInfo object

---

### getPlayerInfoByName(name)
This function returns an object with information about the player.

#### Input parameters
- name - the player’s nickname

#### Returns
- PlayerInfo object

---

### getPlayerShipInfo(playerID)
This function returns an object with information about the player’s ship.

#### Input parameters
- playerId - the player’s ID

#### Returns
- ShipInfo object

---

### getPlayerByVehicleId(shipID)
This function returns an object with information about the player.

#### Input parameters
- shipId - the ship’s ID

#### Returns
- PlayerInfo object

---

### getAmmoParams(ammoID)
This function returns an object with information about the shell.

#### Input parameters
- ammoId - the shell ID, this value can be obtained in the event handler function "events.onReceiveShellInfo(func)" (see the description in the "events" methods).

#### Returns
- object

---

### isVehicleBurning(shipID)
This function returns True if the ship is on fire, or False if it isn’t; for example, you can use it in the event handler function "events.onReceiveShellInfo(func)" (see the description in the "events" methods).

#### Input parameters
- shipID - the ship's ID

#### Returns
- true or false

---

### isVehicleFlooding(shipID)
This function returns True if a shell hitting the ship caused flooding, or False if it’s not the case; it is recommended to use it in the same way as "isVehicleBurning".

#### Input parameters
- shipID - the ship's ID

#### Returns
- true or false

---

### isBattleStarted()
This function returns True if the battle has started.

#### Returns
- true or false

---

### cameraAltVision()
This function returns True if Alt key pressed in the battle.

#### Returns
- true or false

---

### isObserverMode()
This function returns True if player enters into the training room as Observer.

#### Returns
- true or false





