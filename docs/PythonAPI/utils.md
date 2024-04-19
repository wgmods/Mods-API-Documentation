**utils** methods allow you to work with various additional functions.

## Available methods:

- [getGameVersion()](#getGameVersion)
- [getModDir()](#getModDir)
- [stat(path)](#statpath)
- [walk(top, topdown=True, followlinks=False)](#walktop-topdownTrue-followlinksFalse)

---

### getGameVersion()

This function returns the game version.

#### Returns
- game version, int (0, 5, 15, 123456)

---

### getModDir()

This function returns an absolute path to the folder with the current mod.

#### Returns
- str

---

### stat(path)

The method returns an object with attributes corresponding to attributes "os.stat(path)".
You can see full documentation on this function on the official Python website here: https://docs.python.org/2/library/os.html#os.stat

#### Input parameters
- path - path to the file, str

#### Returns
- object

---

### walk(top, topdown=True, followlinks=False)

The method is similar to "os.walk(top, topdown=True, onerror=None, followlinks=False)" where:
  - "top" is a directory in the mod folder (if it exists) where the method will pass (see "C:\Games\World_of_Warships\res_mods\0.7.9.1\PnFMods\TestMod\testDir"),
  - "topdown" is a way of passing: "True" is top down (a base value), "False" is bottom up, generates file names in the directory tree moving along the tree down from the top or vice versa; for every  directory in the tree it is fixed in the top part of the directory switching on the top, and returns the following parameters:
  - "dirpath" is a string, a path to the directory
  - "dirnames" is a list, a list of sub-directory names in the directory "dirpath"
  - "filenames" is a list, a list of file names in this directory

You can see full documentation on this function on the official Python website here: https://docs.python.org/2/library/os.html#os.walk

#### Input parameters
- "top" is a directory in the mod folder (if it exists) where the method will pass (see "C:\Games\World_of_Warships\res_mods\0.7.9.1\PnFMods\TestMod\testDir"),
- "topdown" is a way of passing: "True" is top down (a base value), "False" is bottom up, generates file names in the directory tree moving along the tree down from the top or vice versa; for every  directory in the tree it is fixed in 

#### Returns
- object
