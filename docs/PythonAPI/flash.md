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
