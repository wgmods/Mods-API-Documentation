Module **ui** contains methods for working with game's UI.

## Available methods:

- [createUiElement()](#createUiElement)
- [addDataComponent(uiID, initData)](#addDataComponentuiID-initData)
- [addDataComponentWithId(uiID, componentId, initData)](#addDataComponentWithIduiID-componentId-initData)
- [addWorldPositionComponent(uiID, position, yaw)](#addWorldPositionComponentuiID-position-yaw)
- [addScreenPositionComponent(uiID)](#addScreenPositionComponentuiID)
- [addMapPositionComponent(uiID)](#addMapPositionComponentuiID)
- [removeUiElementFromMiniMap(uiID)](#removeUiElementFromMiniMapuiID)
- [addMinimapAttentionComponent(uiID)](#addMinimapAttentionComponentuiID)
- [addRelationComponent(uiID, relation)](#addRelationComponentuiID-relation)
- [addParameterComponent(uiID, parameterId)](#addParameterComponentuiID-parameterId)
- [hasComponent(uiID, componentId)](#hasComponentuiID-componentId)
- [updateUiElementData(uiID, data)](#updateUiElementDatauiID-data)
- [deleteComponent(uiID, componentId)](#deleteComponentuiID-componentId)
- [getUiElementByComponentId(componentId)](#getUiElementByComponentIdcomponentId)
- [getLengthOnMiniMap(length)](#getLengthOnMiniMaplength)
- [setUiPreference(hideInBattleStatus=None)](#setUiPreferencehideInBattleStatusNone)
- [getUserPrefs(sectionName, parameterName, defaultValue)](#getUserPrefssectionName-parameterName-defaultValue)
- [clearData()](#clearData)

## Available components:

- [mods_DataComponent](#mods_DataComponent)

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

#### Note
*Will be able from client version 13.5 !* 

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

### addMapPositionComponent(uiID)
The method adds the MapPosition  component to the ui element. It's shows ui element on the battle mini map.

#### Input parameters
- uiID - ID of the ui element, to which component will be added, returned by [createUiElement()](#createUiElement) method, int

#### Example:
    uiElementID = ui.createUiElement()
    ui.addMapPositionComponent(uiElementID)

---

### removeUiElementFromMiniMap(uiID)
The method removes ui element from the battle mini map.

#### Input parameters
- uiID - ID of the ui element, returned by [createUiElement()](#createUiElement) method, int

#### Example:
    uiElementID = ui.createUiElement()
    ui.removeUiElementFromMiniMap(uiElementID)

---

### addMinimapAttentionComponent(uiID)
The method adds the MinimapAttentionPoint component to the ui element.

#### Input parameters
- uiID - ID of the ui element, to which component will be added, returned by [createUiElement()](#createUiElement) method, int

#### Example:
    uiElementID = ui.createUiElement()
    ui.addMinimapAttentionComponent(uiElementID)

---

### addRelationComponent(uiID, relation)
The method adds the Relation component to the ui element.

#### Input parameters
- uiID - ID of the ui element, to which component will be added, returned by [createUiElement()](#createUiElement) method, int
- relation - value of Relation to the Player, int

#### Example:
    uiElementID = ui.createUiElement()
    ui.addRelationComponent(uiElementID, value = ([constants](/.constants).PlayerRelation.ENEMY)

---

### addParameterComponent(uiID, parameterId)
The method adds the Parameter component to the ui element.

#### Input parameters
- uiID - ID of the ui element, to which component will be added, returned by [createUiElement()](#createUiElement) method, int
- parameterId - ID of Parameter componentstr, str

#### Example:
    uiElementID = ui.createUiElement()
    ui.addParameterComponent(uiElementID, 'modParametersList')

---

### hasComponent(uiID, componentId)
The method returns True if the ui element contains required component

#### Input parameters
- uiID - ID of the ui element, returned by [createUiElement()](#createUiElement) method, int
- omponentId - ID of the required component, int

#### Returns
- bool

#### Example:
    uiElementID = ui.createUiElement()
    elementHasScreenPosition = ui.hasComponent(uiElementID, constants.UiComponents.screenPosition)

---

### updateUiElementData(uiID, data)
The method updates data of the dataComponent of ui element.

#### Input parameters
- uiID - ID of the ui element, returned by [createUiElement()](#createUiElement) method, int
- data - new data for the DataComponent, dict

#### Example:
    uiElementID = ui.createUiElement()
    ui.updateUiElementData(elementID, {'newValue': 1000.0})

#### Note:
*From client version 13.5 it will be used mods_DataComponent instead dataComponent !*

---

### deleteComponent(uiID, componentId)
The method deletes required component from the ui element.

#### Input parameters
- uiID - ID of the ui element, returned by [createUiElement()](#createUiElement) method, int
- componentId - ID of the deleting component, [constants](./constants.md).UiComponents

#### Example:
    uiElementID = ui.createUiElement()
    ui.deleteComponent(uiElementID, constants.UiComponents.screenPosition)

---

### getUiElementByComponentId(componentId)
The method returns ID of the ui element, which contains required component.

#### Input parameters
- componentId - ID of the required  component, [constants](./constants.md).UiComponents

#### Example:
    cameraUiElementId = ui.getUiElementByComponentId(([constants](./constants.md).UiComponents.camera)

---

### getLengthOnMiniMap(length)
The method recalculates length from battle world to battle mini map.

#### Input parameters
- length - length in battle world, float

#### Example:
    radiusOnMiniMap = ui.getLengthOnMiniMap(100.0)

---

### setUiPreference(hideInBattleStatus=None)
The method setup required ui settings parameter.
Can be extended by request in future.

#### Input parameters
- hideInBattleStatus - required parameter name with bool value

#### Example:
    ui.setUiPreference(hideInBattleStatus=True)

---

### getUserPrefs(sectionName, parameterName, defaultValue)
The method returns required ui settings parameter.

#### Input parameters
- sectionName - required section name, str
- parameterName - required parameter name,str
- defaultValue - default return value, some of python's types

#### Example:
    userPref = ui.getUserPrefs('chatBoxWidth', 'requiredParameterName', 0.7)

---

### clearData()
The method deletes all mods_DataComponent components from data hub.

#### Example:
    events.onBattleQuit(ui.clearData())

---

### mods_DataComponent

This is a special data component for using in IU in mods instead of using **data** or **dataComponent**.

Еhe fundamental difference of this component is the update of its data - when the [updateUiElementData(uiID, data)](#updateUiElementDatauiID-data) method is called, the data is not replaced with new ones, but merged, creating a multi-level dictionary.
Thus, this component can be safely added to the same UI element at the same time in different mods, without fear that data from different mods of mods will overlap.

This element also has an **ID** field that can be used to search for the component in the UI code.
To add this component with specified ID use method [addDataComponentWithId(uiID, componentId, initData)](#addDataComponentWithIduiID-componentId-initData)

#### Example
If two mods adding a new UI element tied to the player's ship, then the Python code will look like this:


    *In mod One*
    ship = battle.getSelfPlayerShip()
    ui.updateUiElementData(ship.uiId, {'modOneData': 'mod one data fo player's ship'})


    *In mod Two*
    ship = battle.getSelfPlayerShip()
    ui.updateUiElementData(ship.uiId, {'modTwoData': 'mod two data fo player's ship'})


Then UI unbound2 code will look like this:

    *In mod One*
    (macro GET_MARKER_ENTITY_COMPONENT 'mods_DataComponent')
    (var modData:str = "mods_DataComponentComponent ? mods_DataComponentComponent.data['modOneData']: []" (event "mods_DataComponentComponent.evDataChanged"))

    *In mod Two*
    (macro GET_MARKER_ENTITY_COMPONENT 'mods_DataComponent')
    (var modData:str = "mods_DataComponentComponent ? mods_DataComponentComponent.data['modTwoData']: []" (event "mods_DataComponentComponent.evDataChanged"))

So, you can show different UI information on the ship in two different mods using one UI component.

If you want to find your component by ID in the UI part, the Python code will look like this:

	uiElementID = ui.createUiElement()
	ui.addDataComponentWithId(uiElementID, 'my_component_ID', {'myModData': 'my mod data'})

Then UI unbound2 code will look like this:

	(var collection:gfx = "$datahub.getCollection(CC.mods_DataComponent)")
	(var myModData:str = "$datahub.getPrimaryCompositeEntity(CC.mods_DataComponent, 0, 'my_component_ID')" (event "collection.evAdded") (event "collection.evRemoved"))


#### Note
*Will be able from client version 13.5 !* 

---

