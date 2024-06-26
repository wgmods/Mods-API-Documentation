**flash** methods are designed to work with the Flash part of the mod (a Main.swf file).

## Available methods:

- [call(name, args)](#callname-args)
- [addExternalCallback(name, func)](#addExternalCallbackname-func)
- [removeExternalCallback(name, func))](#removeExternalCallbackname-func)
- [loadFlashMod(modName))](#loadFlashModmodName)
- [loadPyMod(modName))](#loadPyModmodName)
- [reloadMod(modName, needToReloadPy))](#reloadModmodName-needToReloadPy)
- [unloadMod(modName, needToUnloadPy))](#unloadModmodName-needToUnloadPy)
- [getModsStatus())](#getModsStatus)
- [setUbMarkup(url, rootElement))](#setUbMarkupurl-rootElement)
- [setUbData(data))](#setUbDatadata)

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

#### Note
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

### reloadMod(modName, needToReloadPy)

This method reloads the mod.

#### Input parameters
- modName – a name, mod identifier
- needToReloadPy – if it is necessary to reload the Python part of the mod (False is a preset base value of the argument)

![image](https://github.com/wgmods/Mods-API-Documentation/assets/167185926/9c442ab3-a4bb-46a5-858b-1466b4cab0b3)

---

### unloadMod(modName, needToUnloadPy)

This method unloads (switches off) the mod.

#### Input parameters
- modName – a name, mod identifier
- needToUnloadPy- if it is necessary to unload the Python part of the mod (False is a base value of the argument)

---

### getModsStatus()

This method returns a dict containing keys (mod names) and values (their load statuses (True/False)).

#### Returns
- dict

![image](https://github.com/wgmods/Mods-API-Documentation/assets/167185926/5d55936d-4cb8-4b5c-ac02-289aef42a0ef)

---

### setUbMarkup(url, rootElement)

The method loads *.xml file with unbound markup.

#### Input parameters
- url - path to the xml file with markup, str
- rootElement - name of the item to load, str

---

### setUbData(data)

The method set data to element scope.

#### Input parameters
- data - a dictionary in which the key is the name of the variable, value is the value of the variable

#### Note

To get data in scope, you need to declare the controller "lesta.api.UbModController".

---
