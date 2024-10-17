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
