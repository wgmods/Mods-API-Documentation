**utils** methods allow you to work with various additional functions.

## Available methods:

- [getGameVersion()](#getGameVersion)
- [getModDir()](#getModDir)
- [stat(path)](#statpath)
- [walk(top, topdown=True, followlinks=False)](#walktop-topdownTrue-followlinksFalse)
- [isFile(path)](#isFilepath)
- [isDir(path)](#isDirpath)
- [isPathExists(path)](#isPathExistspath)
- [timeNowUTC()](#timeNowUTC)
- [timeNow()](#timeNow)
- [getTimeFromGameStart()](#getTimeFromGameStart)
- [jsonEncode(obj)](#jsonEncodeobj)
- [jsonDncode(s)](#jsonDncodes)
- [logInfo(message='', *args, **kwargs)](#logInfomessage-args-kwargs)

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

The method returns an object with attributes corresponding to attributes **os.stat(path)**.

You can see full documentation on this function on the official Python website here:  https://docs.python.org/2/library/os.html#os.stat

#### Input parameters
- path - path to the file, str

#### Returns
- object

---

### walk(top, topdown=True, followlinks=False)

The method generates file names in the directory tree moving along the tree down from the top or vice versa; for every  directory in the tree it is fixed in the top part of the directory switching on the top.

The method is similar to **os.walk(top, topdown=True, onerror=None, followlinks=False)**.

You can see full documentation on this function on the official Python website here:  https://docs.python.org/2/library/os.html#os.walk

#### Input parameters
- top - is a directory in the mod folder (if it exists) where the method will pass, str
- topdown - is a way of passing: **True** is top down (a base value), **False** is bottom up

#### Returns
- dirpath - a path to the directory, str
- dirnames - a list of sub-directory names in the directory "dirpath"
- filenames - a list of file names in this directory

---

### isFile(path)

The method is similar to **os.path.isfile(path)**.

It returns **true** if the file exists on the given path.

You can see full documentation on this function on the official Python website here: https://docs.python.org/2/library/os.path.html#os.path.isfile

#### Input parameters
- path - a path to the file, str

#### Returns
- bool

---

### isDir(path)

The method is similar to **os.path.isDir(path)**.

It returns **true**, if the directory exists on the given path.

You can see full documentation on this function on the official Python website here: https://docs.python.org/2/library/os.path.html#os.path.isdir

#### Input parameters
- path - a path to the file, str

#### Returns
- bool

---

### isPathExists(path)

The method is similar to **os.path.exists(path)**. 

It returns **true**, if the given path exists.

You can see full documentation on this function on the official Python website here: https://docs.python.org/2/library/os.path.html#os.path.exists

#### Input parameters
- path - a path to the file/directory, str

#### Returns
- bool

---

### timeNowUTC()

The method is similar to **datetime.datetime.utcnow()**. 

It returns the current UTC and date.

You can see full documentation on this function on the official Python website here: https://docs.python.org/2/library/datetime.html#datetime.datetime.utcnow

#### Returns
- object

---

### timeNow()

The method is similar to **datetime.datetime.now()**.

It returns the current time and date.

You can see full documentation on this function on the official Python website here: https://docs.python.org/2/library/datetime.html#datetime.datetime.now

#### Returns
- object

---

### getTimeFromGameStart()

The method returns the time passed from game start in seconds.

#### Returns
- float

---

### jsonEncode(obj)

The method is similar to *json.dumps(obj, skipkeys=False, ensure_ascii=True, check_circular=True, allow_nan=True, cls=None, indent=None, separators=None, encoding="utf-8", default=None, sort_keys=False)* with corresponding base values.

The method serializes the object **obj** to a **JSON** line.

You can see full documentation on this function on the official Python website here: https://docs.python.org/2/library/json.html#json.dumps

#### Input parameters
- obj - ogject

#### Returns
- JSON string

---

### jsonDncode(s)

The method is similar to **json.loads(s)**.

It deserializes a **JSON** string to a Python object.

You can see full documentation on this function on the official Python website here: https://docs.python.org/2/library/json.html#json.loads

#### Input parameters
- s - JSON string

#### Returns
- object

---

### logInfo(message='', *args, **kwargs)

The method displays information in the file *python.log*.

#### Input parameters
- message - message to the log file, str
- * args - positional arguments
- ** kwargs - named arguments

---

