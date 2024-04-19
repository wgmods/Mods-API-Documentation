## This module is deprecated, using [ui](./ui.md) module recommended instead this

Module **dataHub** gives the access to the game data if access to it was not restricted.

The full list of all components and their fields can be found in the **Components.xml** file in the game resources.

## Available methods:

- [getFirstEntity(componentName)](#getFirstEntitycomponentName)


---

### getFirstEntity(componentName)
The method returns the first entity object from the **componentName** collection (ex. dataHub.getFirstEntity ('playerAvatar')).

#### Input parameters
- componentName - the name of the component, begins with a small letter, str

#### Returns
- object

#### Example

    playerAvatar = dataHub.getFirstEntity ('playerAvatar')

---
