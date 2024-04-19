Module **customPorts** allows you to add your own port.

## Available methods:

- [addCustomPort(portName, portDisplayName=DEFAULT_NAME, shipPositions=None, shipPositionsByShip=None)](#addCustomPortportName-portDisplayNameDEFAULT_NAME-shipPositionsNone-shipPositionsByShipNone)
- [removeCustomPort(portName)](#removeCustomPortportName)

---

### addCustomPort(portName, portDisplayName=DEFAULT_NAME, shipPositions=None, shipPositionsByShip=None)
This method adds a new port to the port selection menu.

#### Input parameters
- portName - a name, a port identifier, it must coincide with the space and port png-icon name, str
- portDisplayName - a displayed port name, str
- shipPositions
- shipPositionsByShip

---

### removeCustomPort(portName)
This method removed the new port from the port selection menu.

#### Input parameters
- portName - a name of the uploaded port, str

---
