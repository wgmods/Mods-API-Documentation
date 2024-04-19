Module **devmenu** makes it possible to use the developer menu.

This menu has two buttons:

- **Constants** - opens / hides a list of some game constants: types of lootboxes, rewards, ribbons and damage
- **Reload Mod** - reloads the mod

### Available methods:

devmenu.enable() - after entering the port allows you to call the developer menu
the menu is accessed by a shortcut "Ctrl" + "F1"
the button "Reload Mod" reloads the mod that calls the menu
when calling a menu of several mods, the "Reload Mod" button will reload the last loaded mod that brings up this menu
constants:
gives access to the constant value
the value of a specific constant (for example, credits) is obtained in the following way: constants.LootboxType.CREDITS
returns int() value
