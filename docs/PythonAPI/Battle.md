Working with "battle" methods is only possible after entering a battle (for a situation when an event is triggered, see the "events" methods), otherwise methods do not return anything as information they handle is only available in battle. To handle events you need to use "events.onSFMEvent" (see the description below in the "events" methods), returned parameters of this event are "eventName" (an event name), "eventData" (a dict with event parameters).

## Available methods:

- [getPlayersInfo()](#getplayersinfo)
- [getPlayerInfo(playerID)](#getplayerpnfo)
- [getSelfPlayerInfo()](#getselfplayerinfo)
- [getPlayerShipInfo(playerID)](#getplayershipinfo)

- [isObserverMode()](#isobservermode)



### getPlayersInfo()
This function returns a dict, where keys are "playerID", and values are dict "PlayerInfo" with various information about the player.
To view the result, you can pass it to the "World_of_Warships\profile\python.log" file via "print", or write it in a separate file "open('filename', 'w')".

![image](https://github.com/wgmods/Mods-API-Documentation/assets/167185926/be7eeaca-9e6b-4d75-a878-f4500789a862)

![image](https://github.com/wgmods/Mods-API-Documentation/assets/167185926/486b4d27-f7f9-4f34-985f-52b7930ad7cf)

### getPlayerInfo(playerID)
This function returns an object with player information.

The input parameter is playerId (the player’s ID). The returned value is PlayerInfo.

### getSelfPlayerInfo()
This function returns an object with information about the player. The returned value is PlayerInfo.

battle.getPlayerInfoByName(name)
This function returns an object with information about the player.

The input parameter is name (the player’s nickname). The returned value is PlayerInfo.

### getPlayerShipInfo(playerID)
This function returns an object with information about the player’s ship.

The input parameter is playerId (the player’s ID). The returned value is ShipInfo.

### getPlayerByVehicleId(shipID)
This function returns an object with information about the player.

The input parameter is shipId (the ship’s ID). The returned value is PlayerInfo.

### getAmmoParams(ammoID)
This function returns an object with information about the shell.

The input parameter is ammoId (the shell ID, this value can be obtained in the event handler function "events.onReceiveShellInfo(func)" (see the description in the "events" methods).

### isVehicleBurning(shipID)
This function returns True if the ship is on fire, or False if it isn’t; for example, you can use it in the event handler function "events.onReceiveShellInfo(func)" (see the description in the "events" methods).

The input parameter is ID (the ship ID).

### isVehicleFlooding(shipID)
This function returns True if a shell hitting the ship caused flooding, or False if it’s not the case; it is recommended to use it in the same way as "isVehicleBurning".

The input parameter is ID (the ship ID).

### isBattleStarted()
This function returns True if the battle has started.

### cameraAltVision()
This function returns True if Alt key pressed in the battle.

### isObserverMode()
This function returns True if player enters into the training room as Observer.





