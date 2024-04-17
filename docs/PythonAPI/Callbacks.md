"Callbacks" methods are designed for calling functions multiple times.

## Available methods:

- [perTick(func)](#perTickfunc)

### perTick(func)
This function calls a user function passed as a parameter every tick (several times per second).

### Input parameters
  func - user function that will be called by this method every tick.

### Returns
  “handle”, it’s a unique method identifier used to stop a call for a function by a tick.

![image](https://github.com/wgmods/Mods-API-Documentation/assets/167185926/f827ad4d-5aa2-4af1-ac7e-78d4f363644f)

Warning !!!
Be careful when using this method, it can bring to poor performance of the game client.

---
