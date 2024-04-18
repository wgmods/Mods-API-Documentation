**flash** methods are designed to work with the Flash part of the mod (a Main.swf file).

## Available methods:

- [onFlashReady(func)](#onFlashReadyfunc)
- [onSFMEvent(func)](#onSFMEventfunc)

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
