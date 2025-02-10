There is one known issue now with some .dds files, which are extracted from game client by Python script contentSdk.extractSources('...').

Some .dds files can't be loaded by client.

In this case you need to replace them by the the .dds files from client with other resolution:

- .dd0
- .dd1
- .dd2

First, you need to unpack client resources by on of the extracting tools:

- wowsunpack.exe from the ModSDK

https://github.com/wgmods/ModSDK/tree/main

- WoWs Unpack Tool:

https://gitlab.com/AutoSpy/wowsut/raw/master/WOWSUnpackTool.exe

https://dl-wows-gc.wargaming.net/projects/mods/WOWSUnpackTool.exe?_gl=1*m9n0bd*_gcl_au*MTc1MTE3NTQwNi4xNjg4MTM3MDY3

Unpack tool should be put directly into the root game folder. i.e. C:\Games\World_of_Warships.


Notice, that in the files address no other letter symbols that Latin alphabet is allowed.
Grab the .dd0 files when these are available. Copy them to your mod, inside the proper folder and rename to .dds.

#### Editing

Files with extension .dds are direct draw surface files that serve as textures of the 3D models.

Use Paint.NET\GIMP\or Photoshop to edit them.

Filenames ending:
- _a.dds - this file is the base texture. Edits made here directly affect the skin.
- _ao.dds - ambient occlusion, these help the game by loading a pre-rendered shadow.
- _mg.dds - specular, determines the "shininess" and color of reflected environment light.
- _n.dds - normal map, this adds "normals" (inexpensive topology), allowng you to create dents and grooves on the surface of a model without adding them to the 3D model itself.

Files with extension .mfm control which texture files the Game Client needs look up. Editing them will allow you to set customized file names and paths to your textures.
