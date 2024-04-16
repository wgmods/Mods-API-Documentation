Working with "battle" methods is only possible after entering a battle (for a situation when an event is triggered, see the "events" methods), otherwise methods do not return anything as information they handle is only available in battle. To handle events you need to use "events.onSFMEvent" (see the description below in the "events" methods), returned parameters of this event are "eventName" (an event name), "eventData" (a dict with event parameters).

## Available methods:

- [getPlayersInfo()](#getplayersinfo())

### getPlayersInfo()
This function returns a dict, where keys are "playerID", and values are dict "PlayerInfo" with various information about the player.
To view the result, you can pass it to the "World_of_Warships\profile\python.log" file via "print", or write it in a separate file "open('filename', 'w')".

![image](https://github.com/wgmods/Mods-API-Documentation/assets/167185926/be7eeaca-9e6b-4d75-a878-f4500789a862)

![image](https://github.com/wgmods/Mods-API-Documentation/assets/167185926/486b4d27-f7f9-4f34-985f-52b7930ad7cf)

