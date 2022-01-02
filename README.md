C# Style Guide

Note: this guide is adapted from The Official raywenderlich.com C# Style Guide and the SS3D C# Style Guide.


Our overarching goals are **clarity**, **readability** and **simplicity**. Also, this guide is written to keep **Unity** in mind.

## Inspiration

This style guide is based on C# and Unity conventions

## Table of Contents

- [Nomenclature](#nomenclature)
  + [Namespaces](#namespaces)
  + [Classes & Interfaces](#classes--interfaces)
  + [Methods](#methods)
  + [Fields](#fields)
  + [Parameters](#parameters--parameters)
  + [Events](#events--events)
  + [Misc](#misc)
- [Declarations](#declarations)
  + [Access Level Modifiers](#access-level-modifiers)
  + [Fields & Variables](#fields--variables)
  + [Properties](#properties)
  + [Classes](#classes)
  + [Interfaces](#interfaces)
- [Spacing](#spacing)
  + [Indentation](#indentation)
  + [Line Length](#line-length)
  + [Vertical Spacing](#vertical-spacing)
- [Brace Style](#brace-style)
- [Switch Statements](#switch-statements)
- [Language](#language)
- [Common Patterns and Structure](#common-patterns-and-structure)


## Nomenclature

On the whole, naming should follow C# standards.

### Namespaces

Namespaces are all **PascalCase**, multiple words concatenated together, without hypens ( - ) or underscores ( \_ ):

Namespaces should be used for major systems, such as Slimes, or Building. Everything else should be without namespace.

**BAD**:

```csharp
com.ress3dclient.scripts.structures
```

**GOOD**:

```csharp
Structures.Door
```

### Classes & Interfaces

Written in **PascalCase**. For example `RadialSlider`.

### Methods

Methods are written in **PascalCase**. For example `DoSomething()`.

### Fields

All non-static fields are written **camelCase**. Per Unity convention, this includes **public fields** as well.

### Properties

Properties are written PascalCase.

For example:

```csharp
public class MyClass
{
    public int publicField;
    private int packagePrivate;
    private int myPrivate;
    protected int myProtected;
    public int MyProperty { get; private set; }
}
```

**BAD:**

```csharp
private int _myPrivateVariable
```

**GOOD:**

```csharp
private int myPrivateVariable
```

Static fields are the exception and should be written in **PascalCase**:

```csharp
public static int TheAnswer = 42;
```

### Parameters

Parameters are written in **camelCase**.

**BAD:**

```csharp
void DoSomething(Vector3 Location)
```
**GOOD:**

```csharp
void DoSomething(Vector3 location)
```

Single character values are to be avoided except for temporary looping variables.


### Events

Use event Action<T> rather than delegates
 
Prefix event methods with the prefix **On**.

**BAD:**

```csharp
public static event Action CloseCallback Close;
```  

**GOOD:**

```csharp
public static event CloseCallback OnClose;
```

### Misc

In code, acronyms should be treated as words. For example:

**BAD:**

```csharp
XMLHTTPRequest
String URL
findPostByID
```  

**GOOD:**

```csharp
XmlHttpRequest
String url
findPostById
```

## Declarations

### Access Level Modifiers

Access level modifiers should be explicitly defined for classes, methods and member variables.
This includes defining private even though C# will implicitly add it.

Use the least accessible access modifier, except for public member that is expected to be used by other classes in the future.

Use [SerializeField] rather than public to make fields visible in the inspector, unless the field truly needs to be public.

### Fields & Variables

Prefer single declaration per line.

**BAD:**

```csharp
string username, twitterHandle;
```

**GOOD:**

```csharp
string username;
string twitterHandle;
```

  ### Properties

Where possible, if read only access is required to a field from outside its containing class, use a property with a public get and private set:

```csharp
public GameObject SomeMember { get; private set; };
```

Keep in mind that this won’t be accessible in the inspector, however. If that is the desired behavior, the following can be used:


```csharp
[SerializeField] private GameObject someMember;
public GameObject SomeMember => someMember;
```
  
### Classes

Exactly one class, struct, or interface per source file, although inner classes are encouraged where scoping appropriate.

### Interfaces

All interfaces should be prefaced with the letter **I**.

**BAD:**

```csharp
RadialSlider
```

**GOOD:**

```csharp
IRadialSlider
```

## Spacing

Spacing is especially important to make code more readable.

### Indentation

Indentation should be done using **spaces** — never tabs.  

#### Blocks

Indentation for blocks uses **4 spaces** for optimal readability:

**BAD:**

```csharp
for (int i = 0; i < 10; i++)
{
  Debug.Log("index=" + i);
}
```

**GOOD:**

```csharp
for (int i = 0; i < 10; i++)
{
    Debug.Log("index=" + i);
}
```

#### Line Wraps

Indentation for line wraps should use **4 spaces** (not the default 8):

**BAD:**

```csharp
CoolUiWidget widget =
        someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line);
```

**GOOD:**

```csharp
CoolUiWidget widget =
    someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line);
```

### Line Length

Lines should be no longer than **100** characters long.

### Vertical Spacing

There should be just one blank line between methods to aid in visual clarity
and organization. Whitespace within methods should separate functionality, but
having too many sections in a method often means you should refactor into
several methods.

Similarly, fields can be arranged into logical groupings using single spaces.


## Brace Style

All braces get their own line as it is a C# convention:

**BAD:**

```csharp
class MyClass {
    void DoSomething() {
        if (someTest) {
          // ...
        } else {
          // ...
        }
    }
}
```

**GOOD:**

```csharp
class MyClass
{
    void DoSomething()
    {
        if (someTest)
        {
          // ...
        }
        else
        {
          // ...
        }
    }
}
```

Conditional statements are always required to be enclosed with braces,
irrespective of the number of lines required.

**BAD:**

```csharp
if (someTest)
    doSomething();  

if (someTest) doSomethingElse();
```

**GOOD:**

```csharp
if (someTest)
{
    DoSomething();
}  

if (someTest)
{
    DoSomethingElse();
}
```
## Switch Statements

Switch-statements come with `default` case by default (heh). If the `default` case is never reached, be sure to remove it.

If the `default` case is an unexpected value, it is encouraged to log and return an error

**BAD**  
 
```csharp
switch (variable)
{
    case 1:
        break;
    case 2:
        break;
    default:
        break;
}
```

**GOOD**  
 
```csharp
switch (variable)
{
    case 1:
        break;
    case 2:
        break;
}
```

**BETTER**  
 
```csharp
switch (variable)
{
    case 1:
        break;
    case 2:
        break;
    default:
        Debug.LogError("Unexpected value when...");
        return;
}
```

## Language

Use US English spelling.

**BAD:**

```csharp
string colour = "red";
```

**GOOD:**

```csharp
string color = "red";
```

The exception here is `MonoBehaviour` as that's what the class is actually called.

## Common Patterns and Structure

This section includes some rules of thumb for design patterns and code structure

### Error handling

Avoid throwing exceptions. Instead log and error. Methods returning values should return null in addition to logging an error

**BAD:**
```csharp
public List<Transform> FindAThing(int arg){
    ...
    if (notFound) {
        throw new NotFoundException();
    }
}
```

**GOOD:**
```csharp
public List<Transform> FindAThing(int arg){
    ...
    if (notFound) {
        Debug.LogError("Thing not found");
        return null;
    }
}
```

### Default Script Comments

We know what Start and Update does. Please remove their comments when you create them through the editor.

***NO:***
```csharp
// Use this for initialization
void Start() {
    ...
}
```

**YES:**
```csharp
private void Start() {
    ...
}
```

### Finding references
Try to avoid hard references between game objects that don’t belong to the same parent object. Find other ways to communicate (singletons or events). 

Don't use Find or in other ways refer to game objects by name or child index *when possible*. Reference by inspector reference is less error prone and more flexible.
Expect people to set the fields in the inspector and log warnings if they don't.

**BAD:**
```csharp
private GameObject someMember;

private void Start() {
    someMember = GameObject.Find("ObjectName");
}
```

**GOOD:**
```csharp
[SerializeField] GameObject someMember;
```

### RequireComponent

Unless absolutely required, all needed components should be added to the GameObject in the inspector. 

Otherwise, prefer RequireComponent and GetComponent over AddComponent. Having the components in the inspector let's us edit them. AddComponent limits us. 

**BAD:**
```csharp
public class : MonoBehaviour
{
    private AudioSource audioSource;

    private void Start() {
        audioSource = gameObject.AddCompenent<AudioSource>();
    }
}
```

**BETTER:**
```csharp
[RequireComponent(typeof(AudioSource))]
public class : MonoBehaviour
{
    private AudioSource audioSource;

    private void Start() {
        audioSource = GetCompenent<AudioSource>();
    }
}

**BEST**
Add the AudioSource to the GameObject in the inspector.
```







