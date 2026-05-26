# Unbound 2.0 Framework Documentation

---

## Table of Contents

1. [System Level](#system-level)
   - [Calculated Expressions](#calculated-expressions)
   - [Grammar](#grammar)
2. [Basic Functionality](#basic-functionality)
   - [Build Stage](#build-stage)
   - [Display Objects Without Layout System](#display-objects-without-layout-system)
   - [Define Element](#define-element)
   - [Scope](#scope)
   - [Bindings](#bindings)
   - [Customizing Display Object's Style](#customizing-display-objects-style)
3. [Declarative Markup Language and S-expressions](#declarative-markup-language-and-s-expressions)
   - [Macros](#macros)
   - [Markup Execution](#markup-execution)
   - [Data Types](#data-types)
   - [Enums](#enums)
4. [Base Blocks of Markup Language](#base-blocks-of-markup-language)
   - [Constants](#constants)
5. [Controllers](#controllers)
   - [`$Instance`](#instance)
   - [`$FxInstance`](#fxinstance)
   - [`$Repeat`](#repeat)
   - [`$Animation`](#animation)
   - [`$Sector`](#sector)
6. [Element](#element)
7. [Event](#event)
8. [Functions for Calculated Expressions](#functions-for-calculated-expressions)
9. [Layout](#layout)
10. [Macro](#macro)
11. [Scope (Detailed)](#scope-detailed)
12. [Top-Level `def`](#top-level-def)
13. [UI Widgets](#ui-widgets)
14. [Styles and CSS](#styles-and-css)
15. [CSS Tips and Tricks](#css-tips-and-tricks)

---

## System Level

### Calculated Expressions

Unbound allows working with so-called "calculated expressions" (not to be confused with S-expressions). These expressions are calculated on the execution stage. The content of the expression is inside quotation marks (`""`). For the purpose of convenience, we'll call them simply "expressions," and if an S-expression is meant, we'll specify this explicitly.

Expressions are designed for doing unsophisticated data processing and forming values of properties or method call parameters. In the expressions, you can use the variables and events (which were declared in the scope), numeric, string, and boolean literals, as well as operators.

```lisp
(tf
    (text = "' ' + tankmanName + ' — '")
)

(mc forsage_progress_bar
    (style (position = "absolute"))
    ...
)
```

Such expressions will be calculated while executing the markup, namely when methods are called. But they can also be used for defining a parameter in the S-expression method and for setting the value in the S-expression setter.

```lisp
(def element AircraftForsage(activeSquadron:number) layout=true
    (scope
        (event evForsageFinishedAnimate)
        ...
    )
)
```

> **Note:** these expressions will be calculated only once, and it won't be tracked whether the data is updated or not. To track that the data is updated, use the binding mechanism.

ActionScript syntax is used as the basis. The following operators can be used in expressions:

```lisp
(text = "2 + 4")
(text = "name + 'HorScrlBar'")        # similarly: -, /, *, %
(text = "keyCode == 13")              # similarly: >, <, >=, <=, !=
(text = "isFocused && keyCode == 13") # similarly: !, ||, &, ~, |
(width = "400 >> 1")                  # similarly: <<

(scope
    (var testDict:dict = "{
        'up'    : 'bitmap:button_black_bg',
        'hover' : 'bitmap:button_black_bg_hover',
        'down'  : 'bitmap:button_black_press'
    }")
)
(text = "testDict['up']")

(text = "(count1 + count2) + '/' + (total1 + total2)")

(bind class "currStateClass ? currStateClass.style ? currStateClass.style : [] : []")

(text = "(str)count + '/' + (str)total")
```

Expressions can also call functions:

```lisp
(bind text "toUpper('Skorpion G')")
```

### Grammar

| Rule | Definition |
|---|---|
| `root` | `ternary_expr` |
| `ternary_expr` | `logical_or ('?' expression ':' ternary_expr)?` |
| `logical_or` | `logical_and ('\|\|' logical_and)*` |
| `logical_and` | `inclusive_or ('&&' inclusive_or)*` |
| `inclusive_or` | `exclusive_or ('\|' exclusive_or)*` |
| `exclusive_or` | `and ('^' and)*` |
| `and` | `equality ('&' equality)*` |
| `equality` | `relational ([== !=] relational)?` |
| `shift` | `additive ([<< >>] additive)?` |
| `additive` | `multiplicative ([+ -] multiplicative)*` |
| `multiplicative` | `cast ([* / %] cast)*` |
| `cast` | `'(' TYPE_NAME ')' cast \| unary` |
| `unary` | `postfix \| [- !] cast` |
| `postfix` | `primary ('[' ternary_expr ']' \| '(' ')' \| '(' argument_list ')' \| '.' IDENTIFIER)*` |
| `argument_list` | `assignment (',' assignment)*` |
| `assignment` | `IDENTIFIER '=' ternary_expr \| ternary_expr` |
| `primary` | `IDENTIFIER \| constant \| '(' expression ')'` |
| `constant` | `IDENTIFIER \| TYPE_NAME \| STR \| NUMBER \| HEX \| BOOLEAN \| LIST \| MAP` |
| `LIST` | `'[' ']' \| '[' ternary_expr (',' ternary_expr)* ']'` |
| `MAP` | `'{' '}' \| '{' IDENTIFIER ':' ternary_expr (',' IDENTIFIER ':' ternary_expr)* '}'` |
| `IDENTIFIER` | `$?[a-zA-Z]+[a-zA-Z0-9]*` |
| `NUMBER` | `[0-9]+ (.[0-9]+)?` |
| `PERCENT` | `[0-9]+ (.[0-9]+)? '%'` |
| `STRING` | `'\'' .* '\''` |
| `BOOL` | `true \| false` |

---

## Basic Functionality

Basic functionality determines the framework's basic capabilities:

- Forming a scene (creating and adding sprites, textfields, symbols, and blocks)
- Scope, bindings system
- Building definitions (element, css, animation, macro, constant)
- Holders of global data (enums, global constants, global pointers to objects, global methods)

### Build Stage

The key feature of Unbound markup is the ability to create, configure, and add instances of display objects (DOs) to the corresponding target object in a display list. The target object is the parent DO for the current markup fragment. All DOs can be divided into two groups, based on whether they have or don't have the layout system. The layout system serves to position the DO on the stage.

```lisp
(block
    (tf
    )
)
```

where the `block` node is the target object for the `tf` display object.

### Display Objects Without Layout System

| Top-level methods | Description |
|---|---|
| `sprite` | Create empty instance of Sprite |
| `symbol` | Create instance of Symbol (MovieClip or Sprite) from library by linkage |
| `bitmap` | Create instance of Bitmap from library by linkage |
| `tf` | Create instance of TextField |
| `element` | Creating an instance of the element described in the layout |
| `bitmapImage` | Create instance of Bitmap with argument BitmapData |

### Define Element

A high-level DO of a markup is an **element**. An element is a named and parametrized sprite-based markup fragment. An element can have a Scope, which contains the data that are available in the element's body. Work with an element consists of two stages: **"definition"** and **"create instance"**. Elements are defined using the `def` method.

Example definition:

```lisp
(def element CommanderPersonalInfo() layout=true
)
```

Example create instance:

```lisp
(element CommanderPersonalInfo)
```

### Scope

A scope is a storage of data and events, available in the body of the element's description. Only an element can have a scope; the remaining DOs can work only with the scope of the parent element.

All the variables and events used in the element's body must be defined in the scope. If you try to call a property or event that doesn't exist, you'll get the following error: `access of undefined scope event 'nameEvent'`.

| Top-level methods | Description |
|---|---|
| `scope` | This method returns the element's scope, so that you can work with it. |

```lisp
(scope
    (var lvlVal:str = '')
    (var title:str = '')
    (var cost:str = '')
    (var text:str = '')
    (var lvlTextColor:number = 0xffcac8c1)
    (var imageUrl:str = '')
)
```

### Bindings

Bindings are responsible for simple synchronization of data (property, method call, event dispatch). Three elements are synchronized:

- Property
- Method call
- Event

Bindings take a snapshot of the execution data and use it when calculating expressions. This is done for the expressions to contain all the data which were available at the moment when the binding was initialized.

| Top-level methods | Description |
|---|---|
| **scope → object** | |
| `bind` | Adding a value to the object's property. |
| `bindcall` | Calling a method from the object. |
| **object → scope** | |
| `sync` | The value of the parameter in the scope is synced with the value of the object's parameter. |
| `dispatch` | The event in the scope is synced with the event generated by the object (the event is dispatched into the scope based on the object's event). |

All bindings have four common properties:

- **watch** — whether to follow changes in the values of properties in the scope which are used in expressions.
- **init** — whether to execute the relevant action when the binding is initialized.
- **on** — the target object's event which will trigger the binding.
- **enabled** — a boolean value used to enable and disable the binding's execution.

And one common method:

- **event** — adds any event as a trigger for the binding.

#### Bind

Syntax:

```lisp
(bind scopeVar|property "scopeVar|$target|$event.field" [init=false|true] [watch=false|true] [on='scopeEventName|flashEventName|cppEventName'])
```

You can sync both the variable from the scope and the property of the target object.

To sync the variable from the scope, you should place `bind` inside `scope`:

```lisp
(scope
    (var count:number = 30)
    (var total:number = 100)
    (var percent:number = 0)
    (bind percent "count / total")
)
```

To sync the property of the target object, `bind` must be called in the target object whose property is being synced:

```lisp
(scope
    (var vehicleType:str = 'vehicleHeavy')
)
(tf
    (bind text "vehicleType")
)
```

In both cases, if any variable from the expression changes, the expression is calculated and the result is added to the synced variable or property. You can manage this behavior through the `watch=true|false` property.

Another way to sync an expression is to subscribe to an event. There are two methods of subscribing to an event:

**1. Set the event name as the `on` argument.** This method is used for subscribing to flash events or events generated from core C++. If the event has arguments, you can access them via the `$event` object. All the variables must be known by the time the expression is executed in `bind`. But the arguments will be added to the `$event` only if the event has been generated. As no event has happened so far, the `$event` is empty at the start. Therefore, all binding types have the `init=true|false` property, which regulates the binding's behavior during initialization.

```lisp
(tf
    (class GrandTitleTextStyle)
    (text = 'default text')
    (bind text "$event.localX" init=false on='click')
)
```

**2. Dispatch the event into the scope, based on the object's event.**

```lisp
(scope
    (event onCustomEvent)
)
(tf
    (bind text "$event.localY" (event "onCustomEvent"))
    (dispatch onCustomEvent on='click')
)
```

> **Note:** You can subscribe to an event of a specific instance of an element in the scope. In this case, you must set this event name as the `on` argument.

```lisp
(element ButtonPrimary
    (scope
        (bind label "$event.localX+ $event.localY" init=false on='evBtnLeftClickEvent')
    )
)
```

You can manage how the synchronization is executed using a nested structure called `enabled`. In this structure, you can set any logical expression so its result will be a boolean value. If you want to subscribe to changes in `enabled`, use the `bind` structure.

```lisp
(scope
    # Declare the event's definition
    (event changedToogle)

    # Declare the boolean variable — the condition for the execution of the bind
    (var toogleFlag:bool = true)
    (bind toogleFlag "!toogleFlag" watch=false init=false (event "changedToogle"))
)

# Create a button. When clicked, this button must show mouse coordinates in the "label" field
(element ButtonPrimary
    (scope
        # Set the variable in the label so that it synchronizes with the button clicks.
        (bind label "'localX: ' + $event.localX" init=false on='evBtnLeftClickEvent' (bind enabled "toogleFlag"))
    )
)

# Create a button, by clicking which you will dispatch the event that switches the toogleFlag flag.
(element ButtonPrimary
    (scope
        (bind label "'toogleFlag: ' + toogleFlag")
        (dispatch changedToogle on='evBtnLeftClickEvent')
    )
)
```

#### Bindcall

Syntax:

```lisp
(bindcall functionName "scopeVar|$target"* [init=false|true] [watch=false|true] [on='scopeEventName|flashEventName|cppEventName'])
```

`Bindcall` is used to call a method of the target object if an event occurs or any argument changes.

Below is an example of calling the `gotoAndPlay` method of the `mc` display object:

```lisp
(mc 'CloseBtnCrossAnim'
    (bindcall gotoAndPlay "stateFrame")
)
```

Thus, the `gotoAndPlay` method will be called when the `stateFrame` variable is changed.

Here's another example. This time, the `play` method of the `$Animation` controller is called:

```lisp
(controller $Animation
    (bindcall play duration=0.2 from={alpha:0} to={alpha:0.5} (event "evBtnOverEvent") (bind enabled "_isEnabled"))
)
```

The `event` and `enabled` parameters behave just like the `bind` structure.

#### Dispatch

Syntax:

```lisp
(dispatch scopeEventName on='flashEventName|scopeEventName|cppEventName'|[(event "scopeEventName")] [args="{...}"])
```

Dispatch of an event, based on another event generated in Scaleform or Core C++ Unbound. Before dispatching the event, you must declare it in the scope.

```lisp
(scope
    (event onClick)
)
(dispatch onClick on='click')
```

##### Passing Arguments

When dispatching events, you can pass arguments in the form of a dict. By default, if the `args` parameter hasn't been set, all the properties of the original event (the one that serves as a trigger) are passed to the dispatched event.

```lisp
(scope
    (event onClick)
)
(element ButtonPrimary
    (dispatch onClick on='click')
)
(bind text "$event" init=false (event "onClick"))
```

Output in `unbound.log`:
```
UBTRACE: {altKey:false,bubbles:true,buttonDown:false,buttonIdx:0,cancelable:false,clickCount:0,commandKey:false,...}
```

If you specify at least one argument, the properties of the source event will not be passed:

```lisp
(scope
    (event onClick)
    (var argument:number = 100)
)
(element ButtonPrimary
    (dispatch onClick args="{param: argument}" on='click')
)
(bind text "$event" init=false (event "onClick"))
```

Output in `unbound.log`:
```
UBTRACE: {param:100}
```

##### Event Dispatch Direction

You can manage the event's dispatch direction via the `dir` parameter. This parameter can have one of three values:

- **`0`** — the event is dispatched inside the element. By default, `dir=0`.
- **`1`** — the event is dispatched from the child object to the parent object.
- **`2`** — the event is dispatched from the parent object to the child object.

Example with `dir=1`:

```lisp
(def element TestView() layout = true
    (scope
        (event onClick)
    )

    (element ChildElement)

    (tf
        (class HeroTitleYellowTextStyle)
        (text = 'default text')
        (bind text "$event.key" init=false (event "onClick"))
    )
)

(def element ChildElement() layout=true
    (scope
        (event onClick)
    )
    (element ButtonPrimary
        (dispatch onClick args={key: 100} dir=1 on='click')
    )
)
```

> **Note:** Don't forget to declare the event in the scope before using it. Though the event has been declared in the scope of the `ChildElement` definition element, you must also declare it in the scope of `TestView`.

Example with `dir=2`:

```lisp
(def element TestView() layout = true
    (scope
        (event onClick)
    )

    (element ChildElement)

    (element ButtonPrimary
        (dispatch onClick args={key: 100} dir=2 on='click')
    )
)

(def element ChildElement() layout=true
    (scope
        (event onClick)
    )

    (tf
        (class HeroTitleYellowTextStyle)
        (text = 'default text')
        (bind text "$event.key" init=false (event "onClick"))
    )
)
```

##### Identification of Events

When there are several instances on the same level, it's hard to identify which of them generated the event. You can redispatch events from a specific child's scope into the parent object's unique event:

```lisp
(def element TestView() layout = true
    (scope
        (event onClickChild1)
    )

    (element ChildElement id=0
        (scope
            (dispatch onClickChild1 on='onClick')
        )
    )
    (element ChildElement id=1)
    (element ChildElement id=2)
    (element ChildElement id=3)

    (tf
        (class HeroTitleYellowTextStyle)
        (text = 'default text')
        (bind text "'click button id=' + $event.buttonId" init=false (event "onClickChild1"))
    )
)

(def element ChildElement(id:number) layout=true
    (scope
        (event onClick)
    )
    (element ButtonPrimary
        (scope
            (label = "'button_' + id")
        )
        (dispatch onClick args="{buttonId: id}" dir=1 on='click')
    )
)
```

Consequently, the `onClickChild1` event is synced with the `onClick` event only for the button whose `id=0`. As a result, the `text` property of the `tf` block will change only if you click on this button.

##### Dispatch with enabled=true

The event does not respond when switching `enabled` to `true`, but continues to respond when switching `trigger` to `true`.

```lisp
(def element MainTestElement() layout=true
    (scope
        (event evMouseClick)
        (event evTestEvent)
        (event evTestTriggerEvent)

        (var count:number = "0")
        (bind count "count+1" watch=false init=false (event "evMouseClick"))

        (var testCount:number = "count" watch=false init=false (event "evTestEvent"))
        (var testTriggerCount:number = "count" watch=false init=false (event "evTestTriggerEvent"))
    )
    (style
        (width = 500px)
        (height = 300px)
        (backgroundColor = 0x88FF00FF)
    )
    (dispatch evMouseClick on='click')
    (dispatch evTestEvent (bind enabled "count%2 == 0" ))        # will not fire
    (dispatch evTestTriggerEvent (bind trigger "count" ))        # will fire

    (macro trace "'count: ' + count")
    (macro trace "'must always be zero:' + testCount")
    (macro trace "'must be triggered:' + testTriggerCount")
)
```

### Customizing Display Object's Style

Elements and blocks have a **style**. It allows you to configure their visual presentation, for example, change size, apply filters, etc.

| Top-level methods | Description |
|---|---|
| `style` | This method returns the current DO's style, so that you can work with it. |

Each block has its own set of style properties. For example, for the `tf` block, you can customize font, size, and color:

```lisp
(tf
    (style
        (fontFamily = $TitleFont)
        (fontSize = 36)
        (textColor = 0xf5eed5)
    )
)
```

By changing a style's layout properties (paddings, margins, position, flow, etc.) you can adjust the block's position:

```lisp
(block
    (style
        (position = "absolute")
        (bottom = 18px)
        (paddingLeft = 24px)
        (paddingRight = 24px)
    )
)
```

> Style is available only for objects with the layout system, namely elements whose `layout=true` and all kinds of blocks inherited from the `BaseBlock` in C++. If you try to call a style property of DOs without the layout system, you'll get the following error: `access of undefined method 'style' through a reference with type element`.

---

## Declarative Markup Language and S-expressions

A markup consists of **S-expressions**. There are four types of S-expressions, each intended for a specific action:

**1. Call method**

```
(<method name> <positional argument value>* <named argument>*
    <nested s-expression>+
)
<named argument> := <argument name> = <argument value>
```

```lisp
(bind isEnabled "$event.enabled" init=false
    (event "isEnableChanged")
)
```

- `bind` → `<method name>`
- `isEnabled, "$event.enabled"` → `<positional argument value>*`
- `init=false` → `<named argument>*`
- `(event "isEnableChanged")` → `<nested s-expression>+`

**2. Add definition**

```
(def <definition type> <difinition name> (<declaration argument>*) <named argument>*
    <nested s-expression>+
)
<declaration argument> := <argument name> : <argument type> [ = <default value> ]
<named argument>       := <argument name> = <argument value>
```

This definition is essentially a specific instance of an S-expression method. It was introduced only for the special syntax used for declaring parameters.

```lisp
(def element TestView(name:str = '', count:number) layout=true
    (block
    )
)
```

**3. Set a property value**

```
(<property name> = <property value>)
```

```lisp
(style
    (width = 100px)
)

(tf
    (text = 'Hello world!')
)
```

**4. Get a property value**

```
(.<property name>
    <nested s-expression>+
)
```

```lisp
(.graphics
    (lineStyle 1 0xffffdc84 1)
    (beginFill "0xff414141" "0")
    (drawRect 0 0 450 64)
    (endFill)
)
```

The entire markup is based on these four types of expressions.

Full example:

```lisp
# definition
(def element CommanderPersonalInfo(name:str = '') layout=true
    (mc 'ResearchPageBGFlags'
        # set property
        (name = 'flags')

        # call method with argument
        (gotoAndStop "nation")
    )

    (block
        # get property
        (.graphics
            # nested s-expressions
            (beginFill "0xFF0000" "1")
            (drawCircle 40 40 10)
            (endFill)
        )
    )
)
```

### Macros

A macro is a named and parametrized markup fragment which is added to the place where it's called on the parsing stage. Macros are implemented on the AST (Abstract Syntax Tree) level.

Definition of a macro:

```
(def macro <macro name> (<declaration argument>*)
    <nested s-expression>+
)
<declaration argument> := <argument name> : <argument type> [ = <default value> ]
```

```lisp
(def macro StatusesVehicleTypes(width:number=100%, height:number=100%, renderer:str='VehicleTypeItem', name:str)
    (element List "name" "renderer" "width" "height"
        (scope
            (containerFlow = "Flow.HORIZONTAL")
            (listVscrollPolicy = 'off')
            (listHscrollPolicy = 'off')
        )
    )
)
```

You can run a macro with the help of the keyword `macro`:

```
(macro <macro name> <positional argument value>* <named argument>*)
```

```lisp
(macro StatusesVehicleTypes 160 height=32)
```

Though it looks like an ordinary method call, it's not. **The macro's content is added on the parsing stage.**

In the definition of the macro, you can use the macros that were defined before. The resolve operation is done recursively.

```lisp
(def macro ComponentStateBase (statesDict:expression)
    (macro ComponentStateBaseScope "statesDict")
    (macro ComponentStateBaseContent)
)
```

### Markup Execution

The engine that executes the markup isn't tied to any specific features. It doesn't keep any knowledge base on sprites, scopes, etc. A "target object" is the current object subjected to the operations described in the S-expressions. S-expressions are divided into types: method, setter, and getter. On this level, even a definition is simply a method.

The first execution of a markup happens after the file's text has been uploaded to the framework. After the file is parsed, we get a list of S-expressions contained by the file (as a rule, these are definitions and setups of global constants). A fake object is created to execute this list of S-expressions (though, in fact, these methods don't need it).

Once a definition has been declared, the engine starts executing the list of S-expressions. The engine creates the corresponding object and S-expressions, which are contained in the definition's body and applied to it.

As the S-expressions are being executed, the target object changes. This happens along with the execution of nested S-expressions. For them, the target object will be the object returned by the parent S-expression. If the S-expression didn't return anything or returned something other than an object, the nested S-expressions won't be executed. Values (including objects) can be returned by methods and getters.

```lisp
# the def method doesn't return anything, therefore its nested S-expressions won't be executed
# the def method will save them in order to use them later for building a definition
# S-expressions in the body of the CommanderPersonalInfo definition will be applied to the sprite object
# When building the CommanderPersonalInfo element,
(def element CommanderPersonalInfo (command:str, toggle:bool = false) layout=true
    # target-object — Sprite
    # the tf method will create TextField, add it to the target object in the display list,
    # and return it
    (tf
        # target-object — TextField, which was returned by the tf method
        # style returns StylePreset for the target-object
        # in style, the width parameter will be set as 100
        (style
            (width = 100px)
        )
    )

    # the mc method will create an object of the ResearchPageBGFlags class from the library, using linkage
    # the mc method will add it to the Sprite target-object in the display list
    # and return the created object
    (mc 'ResearchPageBGFlags'
        # target-object — ResearchPageBGFlags (inherited from MovieClip)
        # the gotoAndStop method has been called using the 'ussr' string argument
        (gotoAndStop 'ussr')
    )
)
```

### Data Types

In markup, variables must be strictly divided into types (arguments of definitions, variables of scope). Types are verified on the execution stage (except for macros — they are verified on the parsing phase). This helps you identify errors much faster.

| Type | Description | Syntax | Comments |
|---|---|---|---|
| `number` | number | `12.34` | For numbers, you can specify the unit of measure. |
| | percent | `12.34%` | |
| | pixels | `12px` | |
| `bool` | boolean expression | `true` / `false` | |
| `str` | string | `'text123'` | single quotes |
| `dict` | dictionary | `{a : 1, b: 2}` | |
| `array` | array | `[1, 2, 3]` | |
| `expression` | calculated expression | `"a ? 1 : 2"` | inside double quotation marks. A constant can't be defined inside this expression. |
| `gfx` | pointer to any `GFx::Value` | — | A constant cannot be defined in the layout and in expressions. |
| `object` | pointer to operated object | — | A constant cannot be defined in the layout and in expressions. |

> **Note:** An important peculiarity of working with string literals and variables is that you don't need to use single quotation marks, because the parser interprets any value as a string. Consequently, there are two ways of declaring strings.

```lisp
# Initializing a string
(var vehicleName:str = Skorpion)

# Declaring a key in dict
(var testDict:dict = "{
    up    : 'bitmap:button_black_bg',
    hover : 'bitmap:button_black_bg_hover',
    down  : 'bitmap:button_black_press'
}")
(bind text "toUpper(testDict['up'])")
```

This peculiarity reveals itself when you use binding structures (`bind`, `bindcall`, `sync`, `dispatch`). Example:

```lisp
# Dispatch of the evBtnUpEvent event
(dispatch evBtnUpEvent on=mouseUp)
```

The first argument of the `dispatch` function is a string-type variable, but you don't need to use single quotes.

### Enums

In expressions, you can use the enumerations that were set in the core C++ part of Unbound.

**Flow** — determines how nested display objects are positioned:

- `HORIZONTAL`
- `VERTICAL` (default)
- `TILE_HORIZONTAL`
- `TILE_VERTICAL`
- `REVERSE_HORIZONTAL`
- `REVERSE_VERTICAL`

```lisp
(block
    (style
        (flow = "Flow.HORISONTAL")
    )
)

# This is the equivalent to what's written above:
(hblock
)
```

Aliases for blocks with specific flow values: `vblock`, `vtile`, `htile`, `vreverse`, `hreverse`.

**Easing** — types of easing for animation:

- `line`
- `elastic_in`, `elastic_out`
- `bounce_in`, `bounce_out`
- `back_in`, `back_out`
- `cubic_in`, `cubic_out`
- `quint_in`, `quint_out`
- `expo_in`, `expo_out`, `expo_in_out`
- `sine_in`, `sine_out`, `sine_in_out`

```lisp
(controller $Animation
    (play duration=0.3 to={alpha:0} easing="Easing.cubic_out")
)
```

---

## Base Blocks of Markup Language

### Constants

Unbound constants have the same purpose as those in other languages: they serve to store fixed values. Two types of constants can be used in Unbound:

#### Global Constants

The `(def` function is used to declare a global constant. The value of the constant is added after its name. In the example below, `C_ALLY` is the constant's name and `0xFF80c0ff` is the constant's value.

```lisp
(def constant C_ALLY 0xFF80c0ff)

# The declared constant can then be used in any calculated expression
(style
    (width = "32px")
    (height = "32px")
    (backgroundColor = "C_ALLY")
)
```

```lisp
(def constant ModuleNames [
    'engine',
    'maingun',
    'atba',
    'aviation',
    'airdefence',
    'none',
    'torpedoes',
    'wheel',
    'none',
    'none',
    'fire',
    'flood'
])

(var damagedModuleName:str = "(moduleState == 3 ? 'module_dead_' : 'module_crit_') + ModuleNames[moduleType]")
```

```lisp
(def constant BTN_PRIMARY {
    up              : {font: ButtonTextStyle,         image: {source: 'bitmap:button_normal_bg',          scale9: "Rect(15, 7, 135, 35)"}},
    hover           : {font: ButtonTextStyle,         image: {source: 'bitmap:button_normal_bg_hover',    scale9: "Rect(15, 7, 135, 35)"}},
    down            : {font: ButtonTextStyle,         image: {source: 'bitmap:button_normal_bg_press',    scale9: "Rect(15, 7, 135, 35)"}},
    disabled        : {font: ButtonTextDisabledStyle, image: {source: 'bitmap:button_normal_bg_disabled', scale9: "Rect(15, 7, 135, 35)"}},
    disabledOverlay : {style: 'BtnNormalDisabledOverlayStyle'},
    focusOverlay    : {image: {source: 'bitmap:button_normal_focus', scale9: "Rect(15, 7, 135, 35)"}},
    upSelected      : {font: ButtonTextStyle,         image: {source: 'bitmap:button_normal_bg_press',    scale9: "Rect(15, 7, 135, 35)"}},
    hoverSelected   : {font: ButtonTextStyle,         image: {source: 'bitmap:button_normal_bg_press',    scale9: "Rect(15, 7, 135, 35)"}},
    downSelected    : {font: ButtonTextStyle,         image: {source: 'bitmap:button_normal_bg_press',    scale9: "Rect(15, 7, 135, 35)"}}
})
(macro ComponentStateBase "BTN_PRIMARY")
```

#### Local Constants

These constants are declared in the element's scope and can be used only inside this element.

```lisp
(def element TestView() layout = true
    (scope
        (const STATE_AVAILABLE:number = 0)
        (const STATE_UNAVAILABLE:number = 1)
        (const STATE_LOCKED:number = 2)

        (var currentState:number = 1)
    )

    (tf
        (bind class "currentState == STATE_AVAILABLE ? 'EpicTitleYellowTextStyle' : 'GrandTitleTextStyle'")
        (text = 'Hello Unbound!!!')
    )
)
```

---

## Controllers

A controller is an entity that applies one type of action to the assigned object. For the `$Instance`, `$FxInstance`, and `$Repeat` controllers, specify the object in the `renderer` field. The `$Animation` controller targets the parent object. The `$Sector` controller is an object itself.

Controllers are written in C++.

| Top-level methods | Description |
|---|---|
| `controller` | Creates a controller and applies it to the target object. |

### `$Instance`

This controller adds an instance of the element to the stage.

```lisp
(controller $Instance renderer='PlayerListTextLine' layout=false
    (args entityId="13123")
    (exprs
        (scope
            (bind width "290")
            (bind isAlive "isAlive")
            (bind isSelf "isSelf")
        )
    )
    (bind enabled "isBoolTrue")
)
```

- **`renderer`** — sets the element with which the controller will perform its operations. Available for binding.
- **`layout`** — determines whether the layout system is enabled or not. By default, the value is `false`.
- **`args`** — a controller method. It passes the value from the parent scope to the renderer.
- **`exprs`** — is carried out inside the renderer, but this method has access to the parent scope. `exprs` can contain expressions and bindings. With the help of this method, the controller allows you to subscribe to changes in variables from the parent scope.
- **`enabled`** — assigns the expression which runs the controller. The controller is triggered if the expression is `true`.
- **`trigger`** — sets the expression to trigger the controller. The controller will fire if the expression changes value.
- **`event`** — analogue of `enabled`, but responds to Events.

In some cases, you don't need to create a separate element — you can add all the blocks to `exprs` and set the controller's `layout` parameter as `true`:

```lisp
(controller $Instance layout=true
    (exprs
        (tf
            (name = 'level')
            (class HeroTitleTextStyle)
            (selectable = false)
            (bind text "parentLevel")
        )
    )
)
```

```lisp
(controller $Instance renderer='OwnHealthBar'
    (args _entityId="entityId")
    (bindcall recreate (bind trigger "entityId"))
)
```

### `$FxInstance`

This controller temporarily adds an instance of the element to the stage. The instance is removed from the stage when its **lifetime** expires. The lifetime is measured in seconds.

```lisp
(controller $FxInstance renderer='DamageDangerFX' lifetime=5
    (args data="$event")
    (bindcall create (event "$datahub.getEntity(entityId).damageDanger.evDamage"))
)
```

- **`renderer`, `args`, `exprs`, `enabled`, `layout`** — the same as in the `$Instance` controller.
- **`create`** — this controller method creates an instance of the element. Calls of this method can be subscribed to an event in the scope.
- **`lifetime`** — determines how long the element will exist on the stage. If not set, the default lifetime is **15 seconds**.

```lisp
(controller $FxInstance renderer='LevelView' lifetime=2
    (args textStyle='HeroTitleTextStyle')
    (exprs
        (scope
            (level = "parentLevel")
            (radius = 40)
        )
    )
    (bindcall create (event "onClick"))
)

(def element LevelView(textStyle:str = 'MainTextStyle') layout=true
    (scope
        (event __onParamChange)
        (var radius:number = 13
            (dispatch __onParamChange on='evChanged')
        )
        (var color:number = 0xfff2ad
            (dispatch __onParamChange on='evChanged')
        )

        (var index:number = "$index")
    )

    (style
        (bind width "radius * 2")
        (bind height "radius * 2")
        (align = "center|middle")
    )
    (.graphics
        (bindcall clear init=true (event "__onParamChange"))
        (bindcall lineStyle 1 "color" 0.3 init=true watch=false (event "__onParamChange"))
        (bindcall drawCircle "radius" "radius" "radius" init=true watch=false (event "__onParamChange"))
        (bindcall endFill init=true (event "__onParamChange"))
    )
    (scope
        (var level:number = 0)
    )
    (tf
        (name = 'level')
        (bind class "textStyle")
        (bind text "level" init=false)
        (selectable = false)
    )
)
```

### `$Repeat`

This controller creates the specified number of renderer copies.

```lisp
(controller $Repeat renderer='MapMarkerItem'
    (bind count "collection.items.length" (event "collection.evAdded"))
    (args size="size" mapScale="mapScale" scaleRatio="scaleRatio")
)
```

- **`renderer`, `args`, `exprs`, `enabled`, `layout`** — the same as in the `$Instance` controller.
- **`count`** — sets the number of renderers. In `count`, you can specify any number or an expression which will return a number.
- **`removeChildAt(index)`** — removes from the stage a renderer whose id is `index`.
- **`$index`** — an integer which shows the child's ordinal number from `0` to the last element. The first created element will have `$index=0`, etc. By default, this variable is in the child's scope since the child's creation.

```lisp
(scope
    (event onClick)
    (var countRenderers:number = 5)
)

(controller $Repeat layout=true
    (bind count "countRenderers")
    (exprs
        (element ButtonPrimary
            (scope
                (label = "'button_' + $index")
            )
            (dispatch onClick args="{index : $index}" on='click')
        )
    )

    (bindcall removeChildAt "$event.index" init=false (event "onClick"))
)
```

### `$Animation`

This controller animates values of:

- Properties of the target display object
- Variables from scope
- Variables from styles

Available controller methods:

#### `play` — launch one animation

```lisp
(play
    duration=1.0       # Animation's lifetime in seconds. Obligatory.
    to={ alpha:1, y:0, visible:true }
    from={ alpha:0, y:50, visible:false }
    name='AnimX'       # Name of predefined animation. Example: (def animation AnimX() from=... to=...)
    delay=2.0          # Delay before the animation begins. Default 0.0.
    easing="Easing.quint_out"
    repeatCount=1      # How many times the animation is repeated.
    reverse=false      # Play reversely (to → from). Both 'from' and 'to' must be defined.
    callbacks="{
        onComplete: onCompleteEvent,
        onStart:    onStartEvent,
        onRepeat:   onRepeatEvent,
        onUpdate:   onUpdateEvent
    }"
    id='anmId'         # Animation's id, used to stop the animation via 'stop'.
)
```

#### `playSeq` — launch a sequence of animations

```lisp
(playSeq
    "[
        {duration:1.0, to:{scale:2.0, alpha: 0.5}, delay: 0.4},
        {duration:2.0, to:{scale:1.0, alpha: 1.0}, callbacks: \"{onStart: onAnmStart}\"}
    ]"
    delay=2.0
    repeatCount=1
    callbacks="{
        onComplete:  onCompleteEvent,
        onStart:     onStartEvent,
        onStartItem: onStartItem,
        onRepeat:    onRepeatEvent
    }"
    id='anmId'
)
```

#### `stop` — stop an animation

```lisp
(stop
    id="anmId"   # If id is not set, all animations of the controller are stopped.
)
```

#### `stopSeq` — stop an animation sequence

```lisp
(stopSeq
    id="anmId"
)
```

#### Available Easings

```
Easing.line
Easing.elastic_in
Easing.elastic_out
Easing.bounce_in
Easing.bounce_out
Easing.back_in
Easing.back_out
Easing.quad_in
Easing.quad_out
Easing.cubic_in
Easing.cubic_out
Easing.quint_in
Easing.quint_out
```

#### Examples

**1. Animation triggered when you click the button:**

```lisp
(scope
    (var animationVariable:number = 0)
    (event playAnimationEvent)

    (controller $Animation
        (bindcall play
            duration = 10
            from     = "{animationVariable:0}"
            to       = "{animationVariable:360}"
            easing   = "Easing.cubic_out"
            (event "playAnimationEvent")
        )
    )
)

(tf
    (class HeroTitleYellowTextStyle)
    (bind text "animationVariable")
)

(element ButtonPrimary
    (scope
        (label = 'Play')
        (dispatch playAnimationEvent on='evBtnLeftClickEvent')
    )
)
```

**2. Block animation:**

```lisp
(scope
    (event playAnimationEvent)
    (var triggerAnimation:bool = false)
    (bind triggerAnimation "!triggerAnimation" init=false watch=false (event "playAnimationEvent"))
)

(block
    (style
        (position = "absolute")
        (width = 50)
        (height = 30)
        (top = 100)
        (left = 100)
        (backgroundColor = 0xFFFF0000)
        (alpha = 0)
    )

    (controller $Animation
        (bindcall play
            duration=2
            easing="Easing.cubic_out"
            from="{alpha:0, top:100, width: 50, height: 30}"
            to="{ alpha:1, top:200, width: 100, height: 50 }"
            reverse="!triggerAnimation"
            (bind trigger "triggerAnimation")
        )
    )
)

(element ButtonPrimary
    (scope
        (label = 'Play')
        (dispatch playAnimationEvent on='evBtnLeftClickEvent')
    )
)
```

**3. Trigger vs Enabled:**

```lisp
(controller $Animation
    (bindcall play duration = "HEALTH_ANI_MIN"
        enabled="isEnabled"
        ...
    )
)
(controller $Animation
    (bindcall play duration = "HEALTH_ANI_MIN"
        trigger="isTarget == 'ally'"
        ...
    )
)
```

- **`trigger`** — the condition that triggers the animation. This animation is triggered when the value in the condition changes to the opposite value. Its difference from `enabled` is that `enabled` is triggered only when the condition is `true`.

#### Other animation properties

- **`bindcall`** — indicates that the animation should be started according to the conditions specified in `bind enabled`, `bind trigger`, or `event`.
- **`duration`** — duration of the animation in seconds.
- **`delay`** — delay before playing the animation.
- **`from`** — starting values. If not specified, the animation starts with the current scope values.
- **`to`** — final animation values. Obligatory.
- **`reverse`** — condition for playing the animation in the opposite direction (`to → from`).
- **`trigger`** — triggers when the condition value changes.
- **`killAll`** — when the animation starts, destroys all active animations of the object.

> **Warning:** The peculiarity of this controller is that it memorizes the animated values in the `to` parameter without taking into account the `delay`. Therefore, if the animated values change during the delay, the controller will keep operating old values.

### `$Sector`

This controller allows to draw a sector using `flash.display.Graphics` of that controller's target.

```lisp
(def element SectorControllerSample() layout=true
    (x = 10)
    (y = 10)
    (scope
        (var _circOffset:number     = 30)
        (var _circArc:number        = 60)
        (var _circRad:number        = 200)
        (var _circInRad:number      = 50)
        (var _circColor:number      = 0xffff0000)
        (var _circGradient:array    = [0xffff0000, 0xffff00ff, 0xffffff00])
        (var _circAlphas:array      = [1, 0.5, 0.5])
        (var _circRatios:array      = [0, 127, 255])
        (var _lineThickness:number  = 10)
        (var _lineColor:number      = 0xffffffff)
        (var _lineAlpha:number      = 0.5)
    )

    (block
        (mc 'flash.display.Sprite'
            (controller $Sector
                (offset="_circOffset")
                (color="_circColor" )
                (arc="_circArc" )
                (radius="_circRad" )
                (colors="_circGradient" )
                (alphas="_circAlphas")
                (ratios="_circRatios")
                (lineThickness="_lineThickness")
                (lineColor="_lineColor")
                (lineAlpha="_lineAlpha")
                (innerRadius="_circInRad")
            )
        )
    )
)
```

---

## Element

An element is a top-level object. An element has its own name, so it can be called (inter alia, from outside the document that contains it) or reused. There are two ways to reuse an element: create its instance by calling a Controller, or create its instance by calling the `element` method with the element's name as the argument. An element has its individual scope, but variables of the parent scope can be set to it.

Element parameters:

- **`layout`** (boolean) — enables and disables the layout system. Possible values: `layout=true|false`.
- **`isReadyTracked`** (boolean) — turns on (when `true`) tracking of dependency resolving for each child of element. Also tracks that additional conditions are ok for some specific blocks. For example, image block has an additional condition — image is loaded. Element is hidden while tracking works. Event `$evReadyChanged` is triggered when dependencies are resolved and additional conditions are ok. If `isReadyTracked` equals `false`, then `$evReadyChanged` is triggered when nodes tree is built.
- **`entrance`** (boolean) — determines root element for View. Possible values: `entrance=true|false`.

> **Note:** Element with `entrance=true` obtains size from its parent AS3 container if no size properties were specified in the `style` block.

- **`initType`** (dict/map) — used to specify that the run-time unbound object will not be the container block (for element definition by default) but it will be the block associated with `initType`. When you define the type different from `CONTAINER`, you have to use only the syntax of that block. For example, `BUTTON` is inherited from `CONTAINER`, you can define all kinds of standard blocks inside, but at the same time you can use `(label =)` setter which is part of `(button)` block syntax.

Usage example:

```lisp
(def element PlaneMarker() layout=true
    (element PlaneIcon)
)

# or

# (def layout PlaneMarker()
#     (element PlaneIcon)
# )

(def element PlaneIcon()
    (symbol "(isConsumable ? 'catapult': 'fighter') + '_c'"
        (scaleX = 1)
        (scaleY = 1)
    )
)

# The flag isReadyTracked is used to avoid performance dropping, this behaviour is not default.
# We use this flag for elements where we have to hide element while dependencies are not resolved
# and images are loading.
(def element StandardWindow() layout=true isReadyTracked=true entrance=true
    ...
    (controller $Fade
        (duration = 0.01)
        # starts to play animation when event $evReadyChanged is triggered.
        # It means that all dependencies are resolved and all images are loaded.
        (bindcall play
            (event "$evReadyChanged")
        )
    )
)
```

---

## Event

An event is an object generated and dispatched upon any action of the user (a mouse click, a button pressed, etc.). To distribute the event, the `dispatch` method is used.

Events are defined in the scope:

```lisp
(event valChanged)
(event evKilled)
...
(dispatch evKilled args={} dir="EventDirection.DOWN" (event $datahub.getEntity(entityId).health.evKilled))
```

`dir` sets the direction of the event in a hierarchy. By default, `dispatch` dispatches an event only within the element itself. To send an event to the parent, you need to specify `EventDirection.UP` in `dir`. In the child — `EventDirection.DOWN`. In siblings — just declare the event in the desired siblings, and `dir` can be omitted. For `dir`, a dict with values is entered. By default, `dir = 0`.

```lisp
(def constant EventDirection {
    NONE: 0,
    UP:   1,
    DOWN: 2
})
```

In Unbound, events can be generated from:

**The core C++ part.** For example, the `valueChanged` event is generated in the `slider` block when its value changes.

```lisp
(dispatch valChanged on='valueChanged' dir=1)
```

**The Scaleform part.** For example, the event of clicking on the display object.

```lisp
(block
    (style
        (width = 100)
        (height = 100)
        (backgroundColor = 0xff00ff00)
    )
    (bind alpha "0.5" init=false on='click')
)
```

### Difference Between Subscription to Events with `on` and `event`

Subscription of binding structures can be implemented in two ways:

**1. By passing the event's name to the `on` argument:**

```lisp
(bind eventArgs "$event" init=false on='eventScope')
```

**2. By passing the nested `event` object:**

```lisp
(bind text "$event" init=false (event "eventScope"))
```

The event can be generated in:

- **Scaleform** — e.g., the `click` event of the mouse, or the `keyDown` event of the keyboard.
- **The Core C++ part of Unbound** — e.g., the `slider` block generates the `sliderPositionChanged` event when the slider thumb's position changes.
- **Markup** — i.e., the event has been defined in the element's scope and is generated in its definition.

```lisp
(def element TestView() layout = true entrance=true
    (scope
        (event eventScope)
    )

    (element Button
        (dispatch eventScope on='click')
    )
)
```

Essentially, it isn't generation of an event; it is transformation from a Scaleform/Core C++ event (in this example, it is `'click'`) into the event of the scope (in this example, it is `eventScope`).

If the event is generated in Scaleform or Core C++ Unbound, you can create subscription only by using the `on` argument:

```lisp
(def element TestView() layout = true entrance=true
    (scope
        (event eventScope)
    )

    (block
        (style
            (width = 100px)
            (height = 100px)
            (backgroundColor = 0xffff0000)
        )
        (bind alpha "0.5" init=false on='click')
    )

    (video original_widht=1920 original_height=1080
        (style
            (width = 320px)
            (height = 180px)
        )

        (source = "R.videos.Logo_All" )
        (bind text "$event" init=false on='metaDataChanged')
    )
)
```

If the event is defined in the element's scope, there are two subscription cases depending on where the subscription is located.

**Subscription inside the scope can be done both via `on` and `event`:**

```lisp
(def element TestView() layout = true entrance=true
    (scope
        (event eventScope)

        (var eventArgs:dict = null)
        (bind eventArgs "$event" init=false (event "eventScope"))
        # (bind eventArgs "$event" init=false on='eventScope')
    )

    (element Button
        (scope
            (label = 'dispatch scope event')
        )
        (dispatch eventScope on='click')
    )

    (bind text "eventArgs" init=false)
)
```

**Subscription outside of the scope can be done only via `event`:**

```lisp
(def element TestView() layout = true entrance=true
    (scope
        (event eventScope)
    )

    (element Button
        (scope
            (label = 'dispatch scope event')
        )
        (dispatch eventScope on='click')
    )

    (bind text "$event" init=false (event "eventScope"))
)
```

Consequently, you can use the `on` argument to subscribe only to the events generated by the **target object**.

Let's consider separately subscription to events inside the scope when an element is created:

```lisp
(element Button
    (scope
        (label = 'default text')
        (bind label 'leftClick'  init=false on='evBtnLeftClickEvent')
        (bind label 'rightClick' init=false on='evBtnRightClickEvent')
    )
)
```

The `'evBtnLeftClickEvent'` and `'evBtnRightClickEvent'` events are generated in the definition of the `Button` element.

If you use the `event` structure, the events must be defined in the parent scope:

```lisp
(def element TestView() layout = true entrance=true
    (scope
        (event eventScope)
    )

    (element Button
        (scope
            (label = 'default text')
            (bind label "'keyCode: ' + $event.keyCode" init=false (event "eventScope"))
        )
    )

    (dispatch eventScope on='stageKeyUp')
)
```

---

## Functions for Calculated Expressions

| Function name in markup | Description | Example |
|---|---|---|
| `round(number)` | Mathematical rounding to an integer | `"round(0.423456)"` # 0 |
| `toUpper(str)` | Converts lower case symbols to upper case symbols | |
| `toLower(str)` | Converts upper case symbols to lower case symbols | |
| `clamp(value, min, max)` | Clamps a value between min and max | `(var test:number = "clamp(smth, 0, 10)")` |
| `tr` | IDS string localization | |
| `abs(number)` | Mathematical module | |
| `radToGrad(radNumber)` | Conversion from radians to degrees | |
| `tan(radNumber)` | Tangent of an angle in radians | |
| `floor(number)` | The closest integer less than or equal to the specified number | |
| `ceil(number)` | The closest integer greater than or equal to the number | |
| `pow(basis, exponent)` | The `basis` number raised to the power of `exponent` | |
| `formatSeparator(number)` | Grouping the integer part into 3-digit segments separated by a space. Rounding the fractional part to the second decimal place. | `"formatSeparator(1103569353.789254232)"` → `110 123 123 123.79` |
| `formatFloatingPoint(number, numberOfDigits=1)` | Rounds the fractional part to `numberOfDigits` decimal place. Default = 1. | `"formatFloatingPoint(1.193454334123)"` → `1.2` ; `"formatFloatingPoint(0.423456, 3)"` → `0.423` |
| `subst(str, array_values, dict_values)` | Substitution of the arguments into the placeholders. | `"subst('first number is %d, second is %d', [50, 51])"` ; `subst('%(min)d - %(max)d', [], {min:1, max:2})` |
| `countdownFormat(numberSeconds, numberOfDigits, isShowMinutes)` | Formats the number of seconds into the `min:seconds` format. If the number of minutes is 0, it displays `00`. | `"countdownFormat(125, 0, true)"` |
| `min(x, y)` | Minimum number of the two. `return x < y ? x : y` | `(var test:number = "min(smth, smth2)")` |
| `max(x, y)` | Maximum number of the two. `return x > y ? x : y` | `(var test:number = "max(smth, smth2)")` |

---

## Layout

Unbound has a layout system which serves to position the blocks located in one container based on certain parameters. To turn on the layout system, set `layout=true|false` in the element's definition. The description of the element with `layout=true` is equivalent to `def layout`.

Layout's parameters are described in `style`.

```lisp
(def element TestView() layout = true
    (block
        (style
            (width = 1024px)
            (height = 768px)
            (backgroundColor = 0xff191711)
            (marginLeft = 200px)
        )
        (tf
            (style
                (textColor = 0xffffffff)
            )
            (text = 'SandBox')
        )
    )
)

# or

(def layout TestView()
    (block
        (style
            (width = 1024px)
            (height = 768px)
            (backgroundColor = 0xff191711)
            (marginLeft = 200px)
        )
        (tf
            (style
                (textColor = 0xffffffff)
            )
            (text = 'SandBox')
        )
    )
)
```

### Positioning of Blocks

The layout system positions the blocks based on the values of the `position` property. `position` can have the following values:

- **`flow`** — the layout system positions nested blocks one by one (a block's position depends on the position of the previous block); default is `position="flow"`
- **`absolute`** — the layout system excludes the block from the flow (positioning list)

To position blocks relative to each other with `position="flow"`, you can use the following style properties:

#### `paddingLeft` / `paddingRight` / `paddingTop` / `paddingBottom`

Left/right/top/bottom padding for nested blocks.

```lisp
(def element TestView() layout = true
    (style
        (width = 1024px)
        (height = 768px)
        (backgroundColor = 0xff191711)
        (paddingLeft = 20px)     # left padding in pixels for the nested block
        (paddingTop = 10%)       # top padding, measured in percentage from the current height
    )

    # Coordinates: x:20px (paddingLeft of parent), y: 76.8 (10% of 768px)
    (block
        (style
            (width = 100px)
            (height = 100px)
            (backgroundColor = 0xff0000ff)
        )
    )

    # Coordinates: x:20px (paddingLeft of parent), y: 176.8 (previous block's height + paddingTop)
    (block
        (style
            (width = 100px)
            (height = 100px)
            (backgroundColor = 0xffff0000)
        )
    )
)
```

If you need to set all four parameters at once, you can use the following structure:

```lisp
(style
    (padding = [5, 10, 15, 20])   # [paddingLeft, paddingTop, paddingRight, paddingBottom]
)
```

#### `marginLeft` / `marginRight` / `marginTop` / `marginBottom`

Left/right/top/bottom margin from the current block.

```lisp
(def element TestView() layout = true
    (style
        (width = 1024px)
        (height = 768px)
        (backgroundColor = 0xff191711)
    )

    # Coordinates: x:10px, y:20px (from margins of current block)
    (block
        (style
            (width = 100px)
            (height = 100px)
            (backgroundColor = 0xff0000ff)
            (marginLeft = 10px)
            (marginTop = 20px)
        )
    )

    # Coordinates: x:20px (marginLeft), y:125px (previous y + previous height + current marginTop)
    (block
        (style
            (width = 50px)
            (height = 50px)
            (backgroundColor = 0xffff0000)
            (marginLeft = 20px)
            (marginTop = 5px)
        )
    )
)
```

If you need to set all four parameters at once:

```lisp
(style
    (margin = [5, 10, 15, 20])   # [marginLeft, marginTop, marginRight, marginBottom]
)
```

> **Note:** The principal difference between margins and paddings is that the **paddings** parameters are set in the parent block and determine the positioning of nested blocks, while **margins** determine the position of the current block.

#### `gap`, `hgap`, `vgap`

The distance between each of the nested blocks horizontally/vertically.

```lisp
(def element TestView() layout = true
    (style
        (width = 1024px)
        (height = 768px)
        (backgroundColor = 0xff191711)
        (vgap = 20px)
        (paddingTop = 40px)
        (paddingLeft = 40px)
    )

    (block
        (style
            (width = 20px)
            (height = 20px)
            (backgroundColor = 0xffff0000)
        )
    )

    (block
        (style
            (width = 30px)
            (height = 30px)
            (backgroundColor = 0xff00ff00)
        )
    )

    (block
        (style
            (width = 40px)
            (height = 40px)
            (backgroundColor = 0xff0000ff)
        )
    )
)
```

If the distance between blocks is the same horizontally and vertically, use `gap`:

```lisp
(def element TestView() layout = true
    (style
        (width = 1024px)
        (height = 768px)
        (backgroundColor = 0xff191711)
        (paddingLeft = 100px)
        (paddingTop = 100px)
    )

    # htile positions blocks horizontally, wrapping when width is reached.
    (htile
        (style
            (width = 80px)
            (gap = 10px)
            (backgroundColor = 0x44ffffff)
        )
        (block (style (width = 20px) (height = 20px) (backgroundColor = 0xffff0000)))
        (block (style (width = 30px) (height = 30px) (backgroundColor = 0xff00ff00)))
        (block (style (width = 40px) (height = 40px) (backgroundColor = 0xff0000ff)))
    )
)
```

#### `align`

Positioning of all nested blocks as a single block. Possible values:

- `left` — alignment with the left margin
- `right` — alignment with the right margin
- `top` — alignment with the top margin
- `bottom` — alignment with the bottom margin
- `center` — alignment with the central horizontal line
- `middle` — alignment with the central vertical line

You can use several values at a time, divided by `|`:

```lisp
(align = "center | middle")
```

#### Absolute Positioning

To position the blocks with `position="absolute"` the above properties aren't applied. Use these instead:

- **`left` / `right` / `top` / `bottom`** — padding from the corresponding edge of the container.
- **`hcenter` / `vcenter`** — padding from the center horizontally/vertically.

```lisp
(def element TestView() layout = true
    (style
        (width = 1024px)
        (height = 768px)
        (backgroundColor = 0xff191711)
    )

    (block
        (style
            (width = 20px)
            (height = 20px)
            (backgroundColor = 0xffff0000)
        )
    )

    # Excluded from layout flow positioning
    (block
        (style
            (position = "absolute")
            (width = 30px)
            (height = 30px)
            (left = 40px)
            (top = 50px)
            (backgroundColor = 0xff00ff00)
        )
    )

    (block
        (style
            (width = 40px)
            (height = 40px)
            (backgroundColor = 0xff0000ff)
        )
    )
)
```

> **Note:**
> - The size of the block whose `position="flow"` equals the sizes of the blocks nested in it.
> - The size of the block whose `position="absolute"` equals 0 by default.

---

## Macro

A macro is a named and parametrized markup fragment which is added to the place where it's called on the parsing stage. This allows using a markup fragment several times.

Usage example:

```lisp
# Macro's definition
(def macro trace(expr:expression)
    (block
        (style
            (backgroundColor = "0x50000000")
        )
        (tf
            (class $TextHUD16Bold)
            (style (textColor = "0xFFFF00FF"))
            (autoSize='left')
            (bind text "expr")
        )
    )
)
```

Once defined, the macro can be called at any place:

```lisp
# A structure that calls a macro
(macro trace expr="variable")
```

This mechanism is used for autogeneration of the scope which will be bound with a Python model:

```lisp
(def macro ButtonModel()
    (scope
        (event onClicked)

        (var rawLabel:str       = '')
        (var label:str          = '')
        (var isEnabled:bool     = true)
        (var icon:gfx           = null)
        (var iconAfterText:bool = true)
    )
)
```

---

## Scope (Detailed)

A scope is a storage of data available in the body of the element's description. **It is not inherited from parent elements.** The markup features strong typing — all the used variables and their types, as well as events, must be defined before they are used in the calculated expression. Otherwise, they must be passed from an external scope when calling the element.

A scope can contain:

- Variables (`var`)
- Constants (`const`)
- Definition of an event
- Call of the `bind` method
- Dispatch of an event
- The `$Animation` controller for animating variables in the scope

```lisp
# Definition of an element with the "level" argument
(def element LevelView(textStyle:str = 'MainTextStyle') layout=true
    (scope
        # Definition of an event
        (event __onParamChange)

        # Definition of variables with a default value and dispatch of the '__onParamChange' event when changed.
        # The 'evChanged' event is an internal event in Unbound's core.
        (var radius:number = 13
            (dispatch __onParamChange on='evChanged')
        )
        (var color:number = 0xfff2ad
            (dispatch __onParamChange on='evChanged')
        )
    )

    (style
        (bind width "radius * 2")
        (bind height "radius * 2")
        (align = "center|middle")
    )
    (.graphics
        (bindcall clear init=true (event "__onParamChange"))
        (bindcall lineStyle 1 "color" 0.3 init=true watch=false (event "__onParamChange"))
        (bindcall drawCircle "radius" "radius" "radius" init=true watch=false (event "__onParamChange"))
        (bindcall endFill init=true (event "__onParamChange"))
    )
    (scope
        # Definition of a variable with a default value
        (var level:number = 0)
    )
    (tf
        (name = 'level')
        (class "textStyle")
        (bind text "level" init=false)
        (selectable = false)
    )
)
```

The scope can be described in different parts of the element. On the execution stage, all the parts will be integrated into one scope.

Display of the scope's content:

```lisp
(trace "$scope")
```

Result:

```
UBTRACE: Scope:
    Events: __onParamChange
    Vars:
        color  : 1.67738e+07
        level  : 0
        radius : 13
```

> **Note:** The variables passed to the element as arguments of a definition are **NOT** added to the scope. In the example above, the `textStyle` variable is not in the scope.

When creating an instance of an element, you can change the variables in its scope:

```lisp
(element LevelView 'PromoTitleTextStyle'
    (scope
        (level = 10)
        (radius = 40)
    )
)
```

When an element is called, variables in its scope can be synced with the parent scope's variables:

```lisp
(scope
    (var parentLevel:number = 15)
)

(element LevelView 'PromoTitleTextStyle'
    (scope
        (bind level "parentLevel")
    )
)
```

When scope is updated, `evScopeUpdated` event is dispatched.

> **Note:** At this moment `evScopeUpdated` event is dispatched only if the model was changed.

`evScopeUpdated` event has the parameter `type`. By default it equals `"default"`. It is `"model"` in case of model updating.

```lisp
(bind enableTutorialHint "!showUnavailableConfirm" init=false watch=false
    (event "evScopeUpdated")
    (enabled="$event.type == 'model'")
)
```

---

## Top-Level `def`

### `(def)` or Definition

Construction `(def object Name)` allows defining a global object that can be invoked from any file in working directories.

> **Warning!** Name of the object has to be unique. No matter if in the same or separate files this definition is placed. Otherwise you'll get an error and only first object will be created.

```lisp
(def element TestView())

(def element TestView())


ERROR: Duplicate element definition: 'TestView'
```

---

## UI Widgets

### Symbol

Adding a MovieClip to the stage by linkage. Symbols are used inside definitions of elements whose `layout` parameter is set as `false`. Layout system is disabled.

```lisp
(style
    (backgroundImage = "'symbol:minimap_aim_position'")
)
```

```lisp
'symbol:' + toLower('minimap_' + markerIcon)
```

### Sprite

Adding a Sprite instance to the stage. Sprites are used inside definitions of elements whose `layout` parameter is set as `false`.

```lisp
(def element TestView() layout=false
    (sprite
        (y = 140)
        (tf
            (text = 'hello unbound')
        )
    )
)
```

### MC

Adding a MovieClip instance to the stage by linkage. MovieClips are used inside definitions of elements whose `layout` parameter is set as `true`. Layout system is enabled.

```lisp
(def element TestView() layout=true
    (mc 'FWCloseButtonSlimMC'
        (name = 'closeBtnCrossAnim')
        (bindcall gotoAndPlay "stateFrame")
    )
)
```

### TextField

Adding a TextField instance to the stage. This is supported for all elements whose `layout=true|false`. To display a text, use the `text` or `htmlText` property. When `text` and `htmlText` are set at the same time, only the last action will be applied.

```lisp
(tf
    (text = 'Hello world!')
)
```

```lisp
(tf
    (style
        (width = 400)
        (height = 100)
        (textColor = 0xff0000)
        (fontFamily = $TitleFont)
        (fontSize = 56)
        (textAlign = "right")
        (leading = 10)
        (letterSpacing = 10)
    )
    (multiline = true)
    (autoSize = 'left')
    (selectable = false)
    (text = 'Hello unbound!!!')
)
```

When the text is too large and doesn't fit into the text field, you can use the `elideMode` property. If `elideMode=true`, the text that doesn't fit into the block is cut off, and the last three symbols of the text inside the block are replaced with dots. Every time a text is entered, the block generates the `textElideStatus` event with the `value` argument, which indicates whether the text has been cut or not.

```lisp
(tf
    (class HeroTitleTextStyle)
    (style
        (width = 200)
        (elideMode = true)
    )
    (text = 'Any long text')
    (trace "$event.value" init=false on='textElideStatus')
)
```

### `substitute`

`substitute` — a textblock method that allows replacing substrings with pictures.

`init=true` — required argument.

```lisp
(tf
    (class $TextDefault19NM)
    (bindcall substitute imageOffset="_frameTextCount"
        substitutionMap={'[test_icon]' : 'icon_ground_radar_ally' }
        sourceText='radar: [test_icon] mouse: [KEY_LEFTMOUSE]'
        postfix='_bg'
        init=true
    )
)
```

### Block

It adds a Sprite container-instance to the stage. All nested blocks will be added to this container and positioned one after another, based on the value of the `flow` property in the block's style.

A block has the following aliases:

- `block` — vertical block
- `hblock` — horizontal block
- `vtile` — vertical tile block
- `htile` — horizontal tile block
- `reverse` — vertical block with reverse order of elements
- `hreverse` — horizontal block with reverse order of elements

```lisp
(hblock
    (block
        (style
            (height = 100px)
            (width = 100px)
            (backgroundColor = "0xFF00FF00")
        )
    )

    (block
        (style
            (height = 100px)
            (width = 100px)
            (marginLeft = 10px)
            (backgroundColor = "0xFFFFFFFF")
        )
    )
)
```

### `backgroundImage`

It adds a Bitmap instance to the stage. In the `source` property, specify:

- The path to the file (specify the relevant object of the `R`-class global object)
- The texture name from the atlas
- URL of the image

If the block's size hasn't been set in `style`, the block will become of the same size as the image once the image is loaded.

```lisp
(bind backgroundImage "markerIcon")

(style
    (bind backgroundImage "'bitmap:' + toLower(markerIcon)")
)

(block
    (style
        (backgroundImage = 'url:../aircraft/icon_lock.png')
    )
)
```

### Slider

This component is just a regular Slider. It can be implemented in two different variants: `SliderNormalH` (horizontal) and `SliderNormalV` (vertical).

Scope variables:

- **`value`** (number) — current value of the slider between the minimum and maximum values.
- **`minimum`** (number) — minimum value.
- **`maximum`** (number) — maximum value.
- **`enabled`** (true/false) — whether the slider is available.

Events:

- **`evValueChanged`** — the slider value has changed.

```lisp
(def element Slider (_value:number, _min:number, _max:number, _enabled:bool=true) layout=true
    (scope
        (var enabled:bool = "_enabled")
        (event evValueChanged)
        (var value:number = "$event.value" init=false watch=false (event "evValueChanged"))
    )
    (mc slider_default
        (bind minimum "_min")
        (bind maximum "_max")
        (bind value "_value")
        (bind enabled "enabled")
        (dispatch evValueChanged args="{value: $event.value}" dir=1 on='valueChange')
    )
)
```

---

## Styles and CSS

### General Description

A block's layout parameters can be customized via its style. Each block has its own set of style parameters.

**Customizing style for the `tf` block:**

```lisp
(tf
    (style
        (fontSize = 32)
        (textColor = 0xFFFFFFFF)
    )
    (text = 'Hello world!!!')
)
```

**Customizing style for the `block`-type block:**

```lisp
(block
    (style
        (backgroundColor = 0xffff0000)
        (width = 100px)
        (height = 100px)
    )
)
```

**Customizing style for the `mc` block:**

```lisp
(mc 'Window_BG'
    (style
        (width=100)
        (height=50)
        ...
    )
)
```

Styles can be described in a separate definition and transferred to the block's `class` property:

```lisp
(def element TestView() layout = true
    (block
        (class BlockStyle)
    )
)

(def css BlockStyle()
    (backgroundColor = 0xffff0000)
    (width = 100px)
    (height = 100px)
)
```

The value of the `class` property can be calculated in an expression. This allows you to adjust the blocks' styles depending on the conditions:

```lisp
(def element TestView() layout = true
    (scope
        (event onClick)
        (var switcher:bool = false)
        (bind switcher "!switcher" init=false watch=false (event "onClick"))
    )

    (block
        (bind class "switcher ? 'BlockStyle_1' : 'BlockStyle_2'")
    )

    (element ButtonPrimary
        (scope
            (label = 'change style')
        )
        (dispatch onClick on='click')
    )
)

(def css BlockStyle_1()
    (backgroundColor = 0xffff0000)
    (width = 100px)
    (height = 100px)
)

(def css BlockStyle_2()
    (backgroundColor = 0xff00ff00)
    (width = 120px)
    (height = 130px)
    (alpha = 0.5)
)
```

If several styles with the same properties are applied to a block, the subsequent ones will overwrite the values of the previous ones. **The application sequence is important.**

```lisp
(block
    (class BlockStyle_1)
    (class BlockStyle_2)
)
```

> **Note:** But if you change the style's property directly in the `style` and transfer CSS as a parameter with the same property, the sequence of style application does not matter. The `style` block will be the last one applied.

```lisp
(def element TestView() layout = true
    (block
        (style
            (backgroundColor = 0xffff0000)
            (width = 100px)
            (height = 100px)
        )
        (class BlockStyle_2)
    )
)

(def css BlockStyle_2()
    (backgroundColor = 0xff00ff00)
    (width = 120px)
    (height = 130px)
    (alpha = 0.5)
)
```

### Table of Styles

**Block types:**

- **Basic blocks:** `tf`, `mc`, `image`, and `text_input`.
- **Container blocks:** `block` (and all its aliases — `hblock`, `vtile`, `gtile`, `reverse`, and `hreverse`), `list`, `view_holder`, `slider`, `scroll_bar`, `progress`, and `scrollArea`. Container blocks inherit the properties and methods of their base block.

| Property | CSS analog | Supported by | Value types | Example |
|---|---|---|---|---|
| `width` | width | all blocks | number, %, px | `10px`; `10%` |
| `minWidth` | min-width | all blocks | number, %, px | `100px`; `50%` |
| `maxWidth` | max-width | all blocks | number, %, px | `100px`; `50%` |
| `height` | height | all blocks | number, %, px | `10px`; `10%` |
| `minHeight` | min-height | all blocks | number, %, px | `100px`; `50%` |
| `maxHeight` | max-height | all blocks | number, %, px | `100px`; `50%` |
| `position` | position | all blocks | `absolute`, `flow` | `absolute` |
| `left` | left | all blocks | number, %, px | `10px`; `10%` |
| `right` | right | all blocks | number, %, px | `10px`; `10%` |
| `top` | top | all blocks | number, %, px | `10px`; `10%` |
| `bottom` | bottom | all blocks | number, %, px | `10px`; `10%` |
| `center` | offset from the center | all blocks | number, %, px | `-170` |
| `hcenter` | offset from center horizontally | all blocks | number, %, px | `10px`; `10%` |
| `vcenter` | offset from center vertically | all blocks | number, %, px | `10px`; `10%` |
| `marginLeft` | margin-left | all blocks | number, %, px | `10px` |
| `marginRight` | margin-right | all blocks | number, %, px | `10px` |
| `marginTop` | margin-top | all blocks | number, %, px | `10px` |
| `marginBottom` | margin-bottom | all blocks | number, %, px | `10px` |
| `paddingLeft` | padding-left | container blocks | number, %, px | `10px` |
| `paddingRight` | padding-right | container blocks | number, %, px | `10px` |
| `paddingTop` | padding-top | container blocks | number, %, px | `10px` |
| `paddingBottom` | padding-bottom | container blocks | number, %, px | `10px` |
| `padding` | padding | container blocks | number, %, px | `10px` |
| `backgroundColor` | background-color | container blocks | 0xARGB | `0x1000ff00` |
| `backgroundImage` | background-image | container blocks | str, `'url: {url}'`, `'bitmap: {linkage}'`, `'symbol: {linkage}'` | `backgroundImage = 'url:..\icons\ico.png'` |
| `backgroundSize` | background-size, background-repeat | container blocks | `fill`; `crop`; `cover`; `repeat`; `autosize` | `backgroundSize = "crop"` |
| `flow` | flex-direction | container blocks | `Flow.HORISONTAL`, `Flow.VERTICAL`, `Flow.TILE_HORIZONTAL`, `Flow.TILE_VERTICAL` | `flow = "Flow.HORISONTAL"` |
| `align` | justify-content, align-items | container blocks | `left`, `right`, `bottom`, `top`, `center`, `middle` | `align = "middle\|right"` |
| `alpha` | opacity | all blocks | number from 0 to 1 | `1`; `0`; `0.4` |
| `fontSize` | font-size | `tf` | number | `36` |
| `leading` | inter-string interval | `tf` | number | |
| `letterSpacing` | letter-spacing | `tf` | number | `2` |
| `fontFamily` | font-family | `tf` | str | |
| `textColor` | color | `tf` | 0xRGB | `0xCFC7A8` |
| `textAlign` | text-align | `tf` | `left`; `right`; `center` | `textAlign = "center"` |
| `multiline` | white-space | `tf` | bool | `true`; `false` |
| `ubScaleX` | transform: scaleX() | all blocks | number | `1.25` |
| `ubScaleY` | transform: scaleY() | all blocks | number | `1.25` |
| `rotation` | block rotation (for blocks in absolute position) | all blocks in absolute position | number (degrees) | `(rotation = 30)` |
| `pivotX` | zero-point position by X (used for rotation, scale, absolute position) | all blocks in absolute position | number, %, px | `(pivotX = 50%)` or `(pivotX = 100px)` |
| `pivotY` | zero-point position by Y (used for rotation, scale, absolute position) | all blocks in absolute position | number, %, px | `(pivotY = 10%)` or `(pivotY = 20px)` |
| `scaleX` | scale by X (can be < 0, applied to block and its children) | all blocks | double | `(scaleX = 1.2)` |
| `scaleY` | scale by Y (can be < 0, applied to block and its children) | all blocks | double | `(scaleY = -1.0)` |

### BackgroundSize

```lisp
(def element NationFlagsSmall () layout=true
    (style
        (bind backgroundImage "'url:../nation_flags/small/flag_USA.png'" init=false)
        (backgroundSize = "fill")
        (width = 117)
        (height = 72)
    )
)
```

- **`cover`** — stretch the texture to the container's size while maintaining proportions; the texture fills the entire area, with cropping outside the container.
- **`crop`** — crop the image to the container's size.
- **`fill`** — stretch the image to the container's size without maintaining proportions.
- **`align`** — position the image at the center of the container with cropping outside the container.

---

## CSS Tips and Tricks

### Usage of Style Objects (Similar to CSS Classes)

**Create style objects:**

```lisp
(def css SomeStyleObject()
    (position = "absolute")
    (width = 100%)
    (height = 100%)
)
```

**Invoke:**

```lisp
(block
    (class SomeStyleObject)
)
```

### Example of Implementing the Hover Pseudo-Class

```lisp
(def element SomeElement() layout=true
    (scope
        # Defining the events:
        (event evBtnOverEvent)
        (event evBtnOutEvent)
        ...
    )
    ...
    # Binding the events:
    (dispatch evBtnOverEvent args="{}" on=rollOver)
    (dispatch evBtnOutEvent  args="{}" on=rollOut)
    ...
    (block
        (style
            # Binding style changes to the events:
            (bind alpha 1   (event "evBtnOverEvent"))
            (bind alpha 0.7 (event "evBtnOutEvent"))
        )
    )
)
```

### Hover Triggered on a Specific Area (not the entire block)

If you need to set a certain area as `hitArea`, add a block whose `name='hoverArea'` and pass the block's name to the `hitArea` property of the parent element with the help of the `$target` object.

```lisp
(def element parentElement() layout=true
    (style
        (width = 100px)
        (height = 100px)
        ...
    )

    (block
        (name = 'hoverArea')
        (style
            (width = 50px)
            (height = 50px)
            ...
        )
    )

    (hitArea = "$target.hoverArea")
    # The Hover on the parent block will be triggered only if you point the cursor to the 'hoverArea' block.
)
```

### Styles Change Depending on the Screen's Width/Height (similar to media queries)

```lisp
(def element SomeElement() layout=true
    (scope
        # Add the screen's height to the variable
        (var viewSizeHeight:number = "viewSize.height")
        (bind viewSizeHeight "viewSize.height" (event "viewResized"))
    )
    (style
        ...
        # Verify and set the required value for the property
        (bind bottom 0    (bind enabled "viewSizeHeight < 800"))
        (bind bottom 27px (bind enabled "viewSizeHeight > 800"))
    )
)
```
