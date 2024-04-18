**flash** methods are designed to work with the Flash part of the mod (a Main.swf file).

## Available methods:

- [call(name, args)](#callname-args)
- [addExternalCallback(name, func)](#addExternalCallbackname-func)
- [removeExternalCallback(name, func))](#removeExternalCallbackname-func)
- [loadFlashMod(modName))](#loadFlashModmodName)
- [loadPyMod(modName))](#loadPyModmodName)

---

### call(name, args)

This method calls a callback allowing you to call a function in the mod’s Flash file.

#### Input parameters
- name – a name, callback key to which the function in the Flash part must be subscribed
- args – a list containing passed parameters (or an empty list without parameters) that will be passed to the called function for further handling

![image](https://github.com/wgmods/Mods-API-Documentation/assets/167185926/e3480155-0d78-4ac1-a321-97d94b91d8c9)

---

### addExternalCallback(name, func)

This method adds a callback that signs and calls the function "func" handler in the Python part of the mod. This function accepts a call from the Flash part of the mod, similar to the previous method.

#### Input parameters
- name - a name, callback key
- func - a callback handler function

![image](https://github.com/wgmods/Mods-API-Documentation/assets/167185926/11f2c700-6499-42b3-a116-53b4a6d00aa5)

---

### removeExternalCallback(name, func)

This method removes a callback with a "name" identifier for the "func" handler function.

#### Input parameters
- name - a name, callback key
- func - a callback handler function

### Note
When calling this function without parameters, the handler function list for the current mod will be fully cleared.

---

### loadFlashMod(modName)

This method loads the Flash part of the mod if it wasn’t loaded earlier or was unloaded.

#### Input parameters
- modName - the name of the mod (the name of the folder containing the mod)

---

### loadPyMod(modName)

This method loads the Python part of the mod if it wasn’t loaded earlier or was unloaded. This method will also load the Flash part of the mod.

#### Input parameters
- modName - the name of the mod (the name of the folder containing the mod)

---
