If you want to modify ships geometry, there are few options to do it for now.

### .primitives modifying

.primitives is an old format for geometry, which is not used in client now.

For the old ships (before 0.9.7 client version) you can find this files here.
https://github.com/sea-group/?q=Primitives-Backup&sort=name

For each .model or .geometry  file, find the .primitives file that has exactly the same filename, and put it beside the .model file.

Models in .primitives format are modifiable through ShadowyBandit's Blender Plug-in:

https://github.com/ShadowyBandit/.primitives-converter

Blender versions 2.8 or  3.X are recommended.

After modifying the .primitives must be converted into .geometry format. 

Use official wows_geometrypack tool from ModSDK for converting:

https://github.com/wgmods/ModSDK/tree/main/wows_geometrypack

### .geometry modifying

You can try to use some of follow tools for modifying .geometry files directly:

- https://github.com/ShadowyBandit/.geometry-converter
- https://github.com/wows-tools/wows-geometry

Whatever the method you use, you shall always make sure that your modified model:

- is triangularized
- has valid normals
- has a valid uv map (and it must be named uv1)
- by default, for each model part, the number of vertex combinations and the number of triangles shall be less than 65535. (Some index blocks which have "list32" type can support up to 65536^2-1 indices, but since you can not distinguish them from the tool's interface, I still suggest not to put large model into one part)

