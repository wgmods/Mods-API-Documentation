**events** methods allow you to work with different events in the game client (opening a window, pressing a button in the menu, pressing a keyboard button, going to battle, etc.).

Events are called from the outside and pass various parameters and functions subscribed to these events.

An example of subscription to an event: 

    events.eventName(myEventHandlerFunc).

## Available methods:

- [onFlashReady(func)](#onFlashReadyfunc)
- [onSFMEvent(func)](#onSFMEventfunc)
- [onReceiveShellInfo(func)](#onReceiveShellInfofunc)

---

### onFlashReady(func)

This event is triggered immediately after a Flash part of the "Main.swf" mod is loaded and initialized (if available).

#### Input parameters
- func - it’s a handler function for the event (def func(modName): ), it gets modName as an input argument, it’s a name of the mod containing the loaded Flash part

---

### onSFMEvent(func)

This method allows you to work with various SFM machine events, such as showing or hiding different windows, pressing some buttons, pressing a keyboard or mouse button, entering a battle, etc.

#### Input parameters
- func - it is a handler function for events that takes two parameters from the SFM machine, such as eventName (an event name), and eventData (dict with event parameters)

![image](https://github.com/wgmods/Mods-API-Documentation/assets/167185926/318b9986-b71f-4d9b-99f9-fc0613286fa3)

---

### onReceiveShellInfo(func)

This event is triggered when damage is dealt/received to the enemy/from the enemy by shells/torpedoes.

#### Input parameters
- func - the event handler function "func(*args, **kwargs)" handling the event receives the following parameters: 
    - victimID - shipID an identifier of the attacked ship
    - shooterID - shipID an identifier of the attacking ship
    - ammoID - a shell type
    - matID - a type of material that was hit
    - shootID - ID, a shot identifier
    - booleans - a type of damage after taking a hit (this value has a bit mask):
        - our ship was damaged
        - armor penetration
        - damage under water
        - the ship is destroyed
        - a shell went through the ship
        - a ricochet off the armor
        - splash damage
        - main caliber guns are destroyed
        - torpedo launchers are destroyed
        - secondary battery is destroyed
    - damage - the amount of dealt damage
    - shotPosition - a tuple with coordinates of the point of impact
    - yaw - yaw of the shell, its angle of impact
    - hlinfo - a tuple with the information about the salvo (list with damage info, salvo ID or salvo number)

![image](https://github.com/wgmods/Mods-API-Documentation/assets/167185926/79e4509c-2222-4452-b2b5-e89b81ff63d1)

---



