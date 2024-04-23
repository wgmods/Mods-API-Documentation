## Available methods:

- [gameAPI.data.call(methodName:String, params:Array):void](#gameAPIdatacallmethodNameString-paramsArrayvoid)

---

### gameAPI.data.call(methodName:String, params:Array):void
The method allows you to pass information to the Python part of the mod.

#### Input parameters
- methodName - a name, callback key the Python function is subscribed to (in Python - flash.addExternalCallback(name, func) where **name** corresponds to **methodName**)
- params – an array of passed parameters
- 
[addExternalCallback(name, func)](../PythonAPI/flash.md/#addExternalCallbackname-func)

---
