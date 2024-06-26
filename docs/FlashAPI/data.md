**Data Bridge Module** methods allow the mod to pass or receive data to/from the Python part of the mod.

## Available methods:

- [gameAPI.data.call(methodName:String, params:Array):void](#gameAPIdatacallmethodNameString-paramsArrayvoid)
- [gameAPI.data.addCallBack(methodName:String, func:Function):void](#gameAPIdataaddCallBackmethodNameString-funcFunctionvoid)
- [gameAPI.data.removeCallBack(methodName:String=null, callBack:Function=null):void](#gameAPIdataremoveCallBackmethodNameStringnull-callBackFunctionnullvoid)

---

### gameAPI.data.call(methodName:String, params:Array):void
The method allows you to pass information to the Python part of the mod.

#### Input parameters
- methodName - a name, callback key the Python function is subscribed to (in Python [flash.addExternalCallback(name, func)](../PythonAPI/flash.md/#addExternalCallbackname-func) where **name** corresponds to **methodName**)
- params – an array of passed parameters

---

### gameAPI.data.addCallBack(methodName:String, func:Function):void
The method adds a callback to get information from Python (in Python - [flash.call(name, args)](../PythonAPI/flash.md/##callname-args)) the Flash function is subscribed to.

#### Input parameters
- methodName – a name, callback key the function in the Flash part of the mod is subscribed to (Main.swf file)
- func – a callback handler function

---

### gameAPI.data.removeCallBack(methodName:String=null, callBack:Function=null):void
The method removes a callback the Flash function is subscribed to.

#### Input parameters
- methodName - callback key the function in the Flash part of the mod is subscribed to (Main.swf file)
- callBack - a callback handler function

---
