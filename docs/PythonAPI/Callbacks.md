"Callbacks" methods are designed for calling functions multiple times.

## Available methods:

- [perTick()](#perTickfunc)

### perTick(func)
This function calls a user function passed as a parameter every tick (several times per second!)*.

The input parameter is the user function "func" that will be called by this method every tick.

The returned value is “handle”, it’s a unique method identifier used to stop a call for a function by a tick.

---
