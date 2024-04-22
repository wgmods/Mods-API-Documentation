Module **ui** contains methods for working with game's UI.

## Available methods:

- [createUiElement()](#createUiElement)
- [addDataComponent(uiID, initData)](#addDataComponentuiID-initData)
- [addDataComponentWithId(uiID, componentId, initData)](#addDataComponentWithIduiID-componentId-initData)
- [addWorldPositionComponent(uiID, position, yaw)](#addWorldPositionComponentuiID-position-yaw)
- [addScreenPositionComponent(uiID)](#addScreenPositionComponentuiID)
- [addMinimapAttentionComponent(uiID)](#addMinimapAttentionComponentuiID)

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

### addWorldPositionComponent(uiID, position, yaw)
The method adds the WorldPosition component to the ui element.

#### Input parameters
- uiID - ID of the ui element, to which component will be added, returned by [createUiElement()](#createUiElement) method, int
- position - position of the component in the game world (in the battle), Math.Vector3
- yaw - float

#### Example:
    uiElementID = ui.createUiElement()
    ui.addWorldPositionComponent(uiElementID, Math.Vector3(0.5, 0, 0), yaw)

---

### addScreenPositionComponent(uiID)
The method adds the ScreenPosition component to the ui element.

#### Input parameters
- uiID - ID of the ui element, to which component will be added, returned by [createUiElement()](#createUiElement) method, int

#### Example:
    uiElementID = ui.createUiElement()
    ui.addScreenPositionComponent(uiElementID)

---

### addMinimapAttentionComponent(uiID)
The method adds the MinimapAttentionPoint component to the ui element.

#### Input parameters
- uiID - ID of the ui element, to which component will be added, returned by [createUiElement()](#createUiElement) method, int

#### Example:
    uiElementID = ui.createUiElement()
    ui.addMinimapAttentionComponent(uiElementID)

---
