**events** methods allow you to work with different events in the game client (opening a window, pressing a button in the menu, pressing a keyboard button, going to battle, etc.).

Events are called from the outside and pass various parameters and functions subscribed to these events.

An example of subscription to an event: 

    events.eventName(myEventHandlerFunc).

## Available methods:

- [onFlashReady(func)](#onFlashReadyfunc)

## onFlashReady(func)

This event is triggered immediately after a Flash part of the "Main.swf" mod is loaded and initialized (if available).

The input parameter is func, it’s a handler function for the event (def func(modName): ), it gets modName as an input argument, it’s a name of the mod containing the loaded Flash part.
