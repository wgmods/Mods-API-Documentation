**events** methods allow you to work with different events in the game client (opening a window, pressing a button in the menu, pressing a keyboard button, going to battle, etc.).

Events are called from the outside and pass various parameters and functions subscribed to these events.

An example of subscription to an event: 

    events.eventName(myEventHandlerFunc).

## Available methods:

- [onReceiveShellInfo(func)](#onReceiveShellInfofunc)
- [onBattleStart(func)](#onBattleStartfunc)
- [onBattleQuit(func)](#onBattleQuitfunc)
- [onKeyEvent(func)](#onKeyEventfunc)
- [onMouseEvent(func)](#onMouseEventfunc)
- [onGotRibbon(func)](#onGotRibbonfunc)
- [onAchievementEarned(func)](#onAchievementEarnedfunc)
- [onBattleStatsReceived(func)](#onBattleStatsReceivedfunc)
- [onBattleShown(func)](#onBattleShownfunc)

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

### onBattleStart(func)

This event is triggered when a battle starts, after the timer countdown finishes before the battle.

#### Input parameters
- func - it’s a handler function for the event

---

### onBattleQuit(func)
This event is triggered when exiting a battle and/or exiting the game.

#### Input parameters
- func - it’s a handler function for the event, when handling an event, the function gets one argument - true

---

### onKeyEvent(func)

This method is triggered when keyboard or mouse buttons are pressed after entering the game (when the port is loaded).

#### Input parameters
- func - it’s a handler function for the event, the function gets the event object with different info about pressed keyboard/mouse buttons.
  
An example of  handler function:

    def func(event):

where **event** is the event object with the following properties:
- event.key - a code of the pressed keyboard key (import Keys – grants access to keyboard constants: Keys.KEY_F1 is "F1" key, Keys.KEY_Q is Q key, etc.)
- event.isKeyDown() - the function checks if any key is pressed and returns "True" or "False"
- event.isKeyUp() - the function checks if the key was unpressed after being pressed and returns "True" or "False"
- event.isShiftDown() - checks if "Shift" is on, returns "True" or "False"
- event.isCtrlDown() - checks if "Ctrl" is on, returns "True" or "False"
- event.isAltDown() - checks if  "Alt" is on, returns "True" or "False"

---

### onMouseEvent(func)

This method handles mouse cursor movements.

#### Input parameters
- func - the function gets an event object **event** with different information for handling
  
**event** - an event object with the following properties:
- event.dx - delta change of coordinates in X-direction
- event.dy - delta change of coordinates in Y-direction
- event.dz - the value is always 0

---

### onGotRibbon(func)

This event is triggered when the player gets a ribbon.

#### Input parameters
- func - it’s a handler function for the event, input parameters of the function are *args, **kwargs

The ***args** argument takes a ribbon constant value.

---

### onAchievementEarned(func)

This event is triggered when the player gets an achievement.

#### Input parameters
- func - it’s a handler function for the event, input parameters of the function are *args, **kwargs

---

### onBattleStatsReceived(func)

This event is triggered when the player gets post battle information.

#### Input parameters
- func - it’s a handler function for the event, input parameters of the function are arg

---

### onBattleShown(func)

This event is triggered after the timer countdown finishes and when a battle arena shown.

#### Input parameters
- func - it’s a handler function for the event

---
