**utils** methods allow you to work with various additional functions.

## Available methods:

- [getGameVersion()](#getGameVersion)
- [getModDir()](#getModDir)
- [stat(path)](#statpath)

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

