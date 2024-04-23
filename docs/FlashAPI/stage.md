This module methods allow you to work with **Stage**.

## Available methods:

- [gameAPI.stage.addChild(child:displayObject)](#gameAPIstageaddChildchilddisplayObject)
- [gameAPI.stage.addChildAt(child:displayObject, index:int)](#gameAPIstageaddChildAtchilddisplayObject-indexint)
- [gameAPI.stage.removeChild(child:displayObject)](#gameAPIstageremoveChildchilddisplayObject)
- [gameAPI.stage.removeChildAt(index:int)](#gameAPIstageremoveChildAtindexint)
- [gameAPI.stage.width()](#gameAPIstagewidth)
- [gameAPI.stage.height()](#gameAPIstageheight)

---

### gameAPI.stage.addChild(child:displayObject)
It works in a way similar to the **addChild** method, it adds a **displayObject** to the Stage to visualize the object.
The input argument **child** is a Flash object that is being created.

#### Input parameters
- child - is a Flash object that is being created

---

### gameAPI.stage.addChildAt(child:displayObject, index:int)
Like the **addChildAt** method, it adds a **DispalyObject** to a certain layer of the Stage.

#### Input parameters
- child - a Flash object that is being created
- index - an indexing number of the layer where a DisplayObject should be added

---

### gameAPI.stage.removeChild(child:displayObject)
The method removes a DispalyObject from the Stage.

#### Input parameters
- child - is a DisplayObject that should be removed from the Stage

---

### gameAPI.stage.removeChildAt(index:int)
The method removes the top layer from the Stage.

#### Input parameters
- index - is an indexing number of the layer where a DisplayObject should be removed

---

### gameAPI.stage.width()
The method returns the Stage width.

#### Returns
- **Number** type of data.

---

### gameAPI.stage.height()
The method returns the Stage height.

#### Returns
- **Number** type of data.

---
