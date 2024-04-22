Module **ui** contains methods for working with game's UI.

## Available methods:

- [createUiElement()](#createUiElement)
- [addDataComponent(uiID, initData)](#addDataComponentuiID-initData)
- [addDataComponentWithId(uiID, componentId, initData)](#addDataComponentWithIduiID-componentId-initData)

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
- uiID - ID of the ui element, to which DataComponent will be added, returned by [createUiElement()](#createUiElement) method, int
- initData - initialisation data for data component if needed, dict

#### Example:
    uiElementID = ui.createUiElement()
    ui.addDataComponent(uiElementID, {parameterOne = 1.0, parameterTeo = 10})

---

### addDataComponentWithId(uiID, componentId, initData)
The method adds the mods_DataComponent with ID to the ui element.

#### Input parameters
- uiID - ID of the ui element, to which DataComponent will be added, returned by [createUiElement()](#createUiElement) method, int
- componentId - ID of the adding component, int or str
- initData - initialisation data for data component if needed, dict

#### Example:
    uiElementID = ui.createUiElement()
    ui.addDataComponentWithId(uiElementID, 'my_mod_data', {parameterOne = 1.0, parameterTeo = 10})

---
