**events** methods allow you to work with different events in the game client (opening a window, pressing a button in the menu, pressing a keyboard button, going to battle, etc.).

Events are called from the outside and pass various parameters and functions subscribed to these events.

An example of subscription to an event: 

    events.eventName(myEventHandlerFunc).

Available methods:
