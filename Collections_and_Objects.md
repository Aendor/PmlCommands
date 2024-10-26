# Collections and Objects in AVEVA PML2

Collections and custom objects are essential for handling multiple items and creating structured data in PML2. Collections allow you to work with groups of elements, while objects let you define custom data structures with attributes and methods.

## Table of Contents

1. [Collections](#collections)
   - [COLLECT Command](#collect-command)
   - [Filtered Collect](#filtered-collect)
   - [DO VALUES Loop with Collections](#do-values-loop-with-collections)
2. [Creating Custom Objects](#creating-custom-objects)
   - [Defining an Object](#defining-an-object)
   - [Creating Object Instances](#creating-object-instances)
   - [Defining Methods for Objects](#defining-methods-for-objects)
3. [Examples](#examples)

---

## Collections

A collection in PML2 is a set of objects of the same type that you can iterate over and manipulate. Collections are helpful for tasks like gathering all items of a particular type or filtering based on certain conditions.

### COLLECT Command

The `COLLECT` command gathers all items of a specified type into an array, allowing you to work with them as a collection.

```pml
VAR !pipes COLLECT ALL WITH TYPE :Pipe
DO !pipe VALUES !pipes
  $P 'Pipe Name: ' & $!pipe.NAME
ENDDO
```

### Filtered Collect

You can use conditions with `COLLECT` to filter items based on specific attributes, such as name patterns.

```pml
VAR !pumps COLLECT ALL WITH TYPE :Equipment WHERE NAME MATCHES '*Pump*'
DO !pump VALUES !pumps
  $P 'Pump Name: ' & $!pump.NAME
ENDDO
```

### DO VALUES Loop with Collections

The `DO VALUES` loop is used to iterate through each item in a collection, performing an action for each one.

```pml
VAR !valves COLLECT ALL WITH TYPE :Valve
DO !valve VALUES !valves
  $P 'Valve: ' & $!valve.NAME
ENDDO
```

---

## Creating Custom Objects

In PML2, you can define custom objects to store data with specific attributes and methods. This is helpful for organizing related data and functions in a single structure.

### Defining an Object

To define an object, use the `define object` statement and specify its attributes with the `member` keyword.

```pml
define object Component
  member .Name is STRING
  member .Length is REAL
endobject
```

### Creating Object Instances

Once you define an object type, you can create instances of it and set their attributes.

```pml
VAR !comp = object Component()
!comp.Name = 'PipeSegment'
!comp.Length = 15.5
$P 'Component Name: ' & !comp.Name & ', Length: ' & !comp.Length.String()
```

### Defining Methods for Objects

You can add methods to an object, which are functions that operate on that specific object’s data. Methods are defined using `define method`.

```pml
define method Component.DisplayInfo()
  $P 'Name: ' & !this.Name & ', Length: ' & !this.Length
endmethod
```

Once defined, you can call the method on an instance of the object.

```pml
VAR !comp = object Component()
!comp.Name = 'Valve'
!comp.Length = 20.0
!comp.DisplayInfo()   -- Output: Name: Valve, Length: 20.0
```

---

## Examples

Here are additional examples demonstrating collections and custom objects in PML2.

### Example 1: Collect and Filter Items

This example collects all `:Pipe` objects and filters them by name.

```pml
VAR !pipes COLLECT ALL WITH TYPE :Pipe WHERE NAME MATCHES '*Main*'
DO !pipe VALUES !pipes
  $P 'Main Pipe Name: ' & $!pipe.NAME
ENDDO
```

### Example 2: Using Custom Objects and Methods

This example shows how to create and use a custom object with a method.

```pml
define object Equipment
  member .Name is STRING
  member .Weight is REAL
endobject

define method Equipment.DisplayWeight()
  $P 'Equipment: ' & !this.Name & ', Weight: ' & !this.Weight & ' kg'
endmethod

VAR !equip = object Equipment()
!equip.Name = 'Generator'
!equip.Weight = 500.0
!equip.DisplayWeight()   -- Output: Equipment: Generator, Weight: 500.0 kg
```

### Example 3: Nested Loops with Collections

This example collects two types of items and uses nested loops to compare them.

```pml
VAR !pipes COLLECT ALL WITH TYPE :Pipe
VAR !valves COLLECT ALL WITH TYPE :Valve

DO !pipe VALUES !pipes
  DO !valve VALUES !valves
    $P 'Pipe: ' & $!pipe.NAME & ', Valve: ' & $!valve.NAME
  ENDDO
ENDDO
```

---
