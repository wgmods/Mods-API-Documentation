Working with "battle" methods is only possible after entering a battle (for a situation when an event is triggered, see the "events" methods), otherwise methods do not return anything as information they handle is only available in battle. To handle events you need to use "events.onSFMEvent" (see the description below in the "events" methods), returned parameters of this event are "eventName" (an event name), "eventData" (a dict with event parameters).

## Available methods:

- [getPlayersInfo()](#getplayersinfo())
- [getPlayerInfo(playerID)](#getplayerpnfo(playerid))
- [getSelfPlayerInfo()](#getselfplayerinfo())
- [getPlayerShipInfo(playerID)](#getplayershipinfo(playerid))

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

### battle.getPlayerByVehicleId(shipID)
This function returns an object with information about the player.

The input parameter is shipId (the ship’s ID). The returned value is PlayerInfo.

### battle.getAmmoParams(ammoID)
This function returns an object with information about the shell.

The input parameter is ammoId (the shell ID, this value can be obtained in the event handler function "events.onReceiveShellInfo(func)" (see the description in the "events" methods).

### battle.isVehicleBurning(shipID)
This function returns True if the ship is on fire, or False if it isn’t; for example, you can use it in the event handler function "events.onReceiveShellInfo(func)" (see the description in the "events" methods).

The input parameter is ID (the ship ID).

### battle.isVehicleFlooding(shipID)
This function returns True if a shell hitting the ship caused flooding, or False if it’s not the case; it is recommended to use it in the same way as "isVehicleBurning".

The input parameter is ID (the ship ID).

### battle.isBattleStarted()
This function returns True if the battle has started.

### battle.cameraAltVision()
This function returns True if Alt key pressed in the battle.

### battle.isObserverMode()
This function returns True if player enters into the training room as Observer.





markdownLinkTest
================

# Contents

- [Title](#title)
- [Big Title](#big-title)
- [Medium Title](#medium-title) 
- [Small Title](#small-title) 

# Title

## Big Title

This tests links in Github markdown.

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum ac sapien vulputate, iaculis purus quis, commodo mauris. Maecenas id neque purus. Nullam a lacus porttitor, auctor diam nec, luctus sapien. Ut viverra sapien nec mauris luctus, ac molestie ante viverra. Mauris nisi nisl, commodo et condimentum non, eleifend et velit. Maecenas mollis semper massa a gravida. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Morbi pharetra accumsan luctus. Suspendisse vitae iaculis augue. Etiam ultrices massa sit amet augue laoreet, sit amet gravida nisi bibendum. Vivamus nulla eros, ullamcorper eu tellus at, malesuada vehicula tortor. Ut sollicitudin tincidunt dolor eget varius. Mauris commodo, ipsum eget tincidunt accumsan, quam massa porta massa, at mollis risus sem a lectus. Maecenas sapien dui, eleifend sed risus eu, laoreet mattis nisi. Nunc suscipit condimentum arcu, ut venenatis turpis suscipit non.

### Medium Title

Donec hendrerit nisl sed ipsum hendrerit, eget molestie ante porttitor. Ut sed congue magna, eget tristique felis. Vestibulum ut congue lacus, non iaculis dui. Sed nec cursus nulla. Pellentesque at risus sed eros tristique semper a eu lectus. Aliquam ut cursus eros. Donec non augue et enim ullamcorper rutrum ac nec lacus. Donec eu blandit leo, quis faucibus mi.

Morbi ultrices at mi a fringilla. Nulla magna risus, pellentesque in adipiscing at, fermentum ut dolor. Donec sollicitudin ut magna non aliquam. Aenean vulputate vitae est quis dapibus. Aenean laoreet diam justo, at consequat nisi pellentesque ut. Ut molestie vulputate urna eu viverra. Praesent id commodo nisl. Aliquam quis consectetur nibh. Aenean ultricies pellentesque elit lacinia gravida. Cras a auctor magna.

#### Small Title

Donec in elementum ante, eu aliquet orci. Maecenas non venenatis ante. Etiam vel sollicitudin diam, a sodales sem. Aenean interdum quam commodo porta sagittis. Curabitur non aliquam odio. Nam pharetra tempor purus, sit amet iaculis odio placerat id. Sed hendrerit consequat lorem quis faucibus. Aenean eu eros ante. Nulla nec nunc id eros consequat dictum.

Aliquam id dolor quis est dictum hendrerit rutrum sit amet eros. Sed vehicula posuere massa, vitae auctor purus ultricies ultricies. Quisque ac neque vitae velit varius fermentum tincidunt vitae enim. Phasellus eu venenatis orci. Nullam dignissim hendrerit arcu hendrerit auctor. Nunc dapibus lobortis enim, quis dictum ante accumsan vehicula. Nam tellus nisl, eleifend vel rhoncus ut, mollis ut tellus. Curabitur quis diam sit amet risus porttitor elementum. Suspendisse potenti.

Quisque elementum augue id ipsum viverra, vel dictum velit lacinia. Quisque eget porta dui. Morbi eget nulla ut purus blandit consectetur a nec nisi. Nam ac sodales enim, suscipit mollis neque. Fusce condimentum, augue vitae elementum pellentesque, tortor erat mollis enim, non molestie libero augue vel leo. Phasellus bibendum aliquet velit, ac commodo nulla vulputate vitae. Aliquam nibh nibh, suscipit ac tellus eget, eleifend pellentesque turpis. Nullam eu fermentum tortor. Vestibulum varius ac diam nec venenatis. Sed aliquam tempus ante eget placerat. Nullam mollis eget dui vel convallis. Morbi sed nibh et metus fringilla sagittis.

Praesent nec euismod erat. Etiam ullamcorper ultrices tempus. Quisque accumsan consequat augue, id consequat magna suscipit quis. Praesent gravida pellentesque quam at porta. In consectetur sollicitudin leo vitae adipiscing. Donec in varius tortor. Vivamus nec dictum est. Cras non turpis malesuada, congue erat sit amet, congue elit. Morbi dictum condimentum nulla vitae aliquet. Curabitur eros nisl, fringilla eget ultrices sed, ullamcorper nec quam. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Morbi pellentesque ultrices mi non interdum. Nulla non accumsan dolor. Curabitur eget tellus sapien.

Cras vulputate tortor sed nulla tristique condimentum in sit amet ipsum. Sed condimentum convallis eleifend. Donec pharetra, enim eu rutrum tincidunt, massa arcu consequat ipsum, sed posuere neque lorem in felis. Donec faucibus quam quis est tincidunt, id aliquam leo tempor. Quisque eget massa pretium, pharetra justo iaculis, pulvinar magna. Nam facilisis dictum dictum. Aliquam tristique, sem nec euismod cursus, purus justo consequat enim, in sollicitudin lacus arcu ultrices neque. Integer et enim imperdiet, eleifend est sed, interdum eros. Mauris vitae elit molestie, ultricies mi nec, ultricies purus.

