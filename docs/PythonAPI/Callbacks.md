"Callbacks" methods are designed for calling functions multiple times.

## Available methods:

- [perTick(func)](#perTickfunc)
- [callback(delaytime, func, *args, **kwargs)](#delaytime,-func)

### perTick(func)
This function calls a user function passed as a parameter every tick (several times per second).

#### Input parameters
* func - user function that will be called by this method every tick.

#### Returns
* handle - unique method identifier used to stop a call for a function by a tick.

![image](https://github.com/wgmods/Mods-API-Documentation/assets/167185926/f827ad4d-5aa2-4af1-ac7e-78d4f363644f)

#### Warning
Be careful when using this method, it can bring to poor performance of the game client.

---

### callback(delaytime,func)
This function also takes the user function "func" as a parameter that will be called each time (repeatedly, again and again) with a set delay (an interval in seconds).

#### Input parameters

* delaytime – a delay in seconds indicating when the func function will be called
* func – a function to be called
* *args – positional arguments that will be passed to the func function
* **kwargs – named arguments that will be passed to the func function

#### Returns
* handle - unique method identifier used to stop a call for a function by a tick.

![image](https://github.com/wgmods/Mods-API-Documentation/assets/167185926/61b0e222-2172-4621-b345-133dab2e38dd)

---
