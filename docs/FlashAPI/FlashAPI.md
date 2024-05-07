To create the Flash part of the mod, you need an ActionScript 3 IDE, you can use **FlashDevelop**, **Adobe Flash Professional**, **Adobe Flash Builder** and other editors.

Let’s create a new AS3 project. We call the main file **Main**, it will have an extension "*.as” and we add an external SWC library (you can find an updated version in our ModsSDK - [ModsSDK](https://github.com/wgmods/ModSDK) https://github.com/wgmods/ModSDK - as3_library/wows_library.swc) depending on the selected IDE.

An example of adding it to Flash Builder:

![image](https://github.com/wgmods/Mods-API-Documentation/assets/167185926/b1156d3f-5307-4eaf-8bec-4be0dd69791a)

Then we rework the script in the "Main.as" file of the project for our mod template.

![image](https://github.com/wgmods/Mods-API-Documentation/assets/167185926/04f0ff2e-0425-45c7-a545-d39ee45cd458)

We can create the Flash part of our mod now. As you see, our main class has the basic class "ModBase" contained in the added library, the Flash file of the mod will not work without it.

## Available modules:

- [data](./data.md)
- [stage](./stage.md)
