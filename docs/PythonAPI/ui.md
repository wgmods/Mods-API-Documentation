Module **ui** contains methods for working with game's UI.

## Available methods:

- [createUiElement()](#createUiElement)
- [addDataComponent(uiID, initData)](#addDataComponentuiID-initData)

---

### createUiElement()
The method creates the empty ui object and returns its ID.

#### Returns
- int

#### Example:
    uiElementID = ui.createUiElement()

---

### addDataComponent(uiID, initData)
The method adds the mods_DataComponent to the ui element.

#### Input parameters
- uiID - ID of the ui element, to which DataComponent will be added, returned by createUiElement() method, int
- initData - initialisation data for data component if needed, dict

#### Example:
    uiElementID = ui.createUiElement()
    ui.addDataComponent(uiElementID, {parameterOne = 1.0, parameterTeo = 10})

---

