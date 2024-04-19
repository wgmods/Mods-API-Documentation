Module **customPorts** allows you to add your own port.

## Available methods:

- [addCustomPort(portName, portDisplayName = DEFAULT_NAME, isPremium = False, peculiarities = None)](#addCustomPortportName-portDisplayName--DEFAULT_NAME-isPremium--False-peculiarities--None)
- [removeCustomPort(portName)](#removeCustomPortportName)

---

### addCustomPort(portName, portDisplayName = DEFAULT_NAME, isPremium = False, peculiarities = None)
This method adds a new port to the port selection menu.

#### Input parameters
- portName - a name, a port identifier, it must coincide with the space and port png-icon name, str
- portDisplayName - a displayed port name, str
- isPremium - if the port is premium or not, bool
- peculiarities - an array of the port’s peculiarities (e.g. peculiarities = [ 'arpeggio' ])

---

### removeCustomPort(portName)
This method removed the new port from the port selection menu.

#### Input parameters
- portName - a name of the uploaded port, str

---
