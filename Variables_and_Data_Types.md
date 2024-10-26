# Variables and Data Types in AVEVA PML2

This section explains how to declare variables, use data types, and work with various PML2 data structures. Variables are fundamental in programming and allow you to store and manipulate data in your PML2 scripts.

## Table of Contents

1. [Variable Declaration](#variable-declaration)
2. [Data Types](#data-types)
   - [STRING](#string)
   - [REAL](#real)
   - [BOOLEAN](#boolean)
   - [ARRAY](#array)
   - [OBJECT](#object)
3. [Examples](#examples)

---

## Variable Declaration

Variables in PML2 are declared with the `VAR` keyword. Local variables use the `!` prefix, while global variables use the `!!` prefix.

- **Local Variable**: Accessible only within the current function or procedure.
  ```pml
  VAR !count = 10

  ```
- **Global Variable**: Accessible across functions and procedures.
  ```pml
  VAR !!globalName = 'Project1'
  ```

### Naming Conventions

- Variables should start with either `!` for local or `!!` for global.
- Use descriptive names to improve readability (e.g., `!totalLength` instead of `!t`).

---

## Data Types

PML2 supports several primary data types, each with its own purpose. Below are the main data types used in AVEVA PML2 scripts.

### STRING

A `STRING` is used to store text data. Strings are defined with quotes, and you can concatenate strings using the `&` symbol.

```pml
VAR !greeting = 'Hello, '
VAR !name = 'World'
VAR !message = !greeting & !name   -- Result: "Hello, World"
```

### REAL

A `REAL` is a numeric data type used for mathematical operations. Use `REAL` for numbers with or without decimals.

```pml
VAR !length = 25.75   -- Declares a REAL variable with a decimal
VAR !width = 10       -- Declares a REAL variable as an integer
VAR !area = !length * !width
```

### BOOLEAN

A `BOOLEAN` stores logical values, either `TRUE` or `FALSE`. Boolean values are often used in conditions and loops.

```pml
VAR !isConnected = TRUE
IF (!isConnected) THEN
  $P 'Connection is active'
ENDIF
```

### ARRAY

An `ARRAY` is used to store a list of values, which can be accessed by index. Arrays are useful for managing collections of data.

```pml
VAR !values = ARRAY()
!values[1] = 'Item1'
!values[2] = 'Item2'
$P $!values[1]    -- Output: "Item1"
```

### OBJECT

An `OBJECT` in PML2 is a custom data type that you can define to hold attributes and methods.

```pml
define object Component
  member .Name is STRING
  member .Length is REAL
endobject

VAR !comp = object Component()
!comp.Name = 'Valve'
!comp.Length = 123.45
```

---

## Examples

Here are a few examples demonstrating how to use variables and data types effectively in PML2.

### Example 1: Concatenating Strings

```pml
VAR !firstName = 'John'
VAR !lastName = 'Doe'
VAR !fullName = !firstName & ' ' & !lastName
$P 'Full Name: ' & !fullName
```

### Example 2: Basic Math Operations with REAL Numbers

```pml
VAR !length = 10.5
VAR !width = 5.0
VAR !area = !length * !width
$P 'Area: ' & !area.String()
```

### Example 3: Working with Arrays

```pml
VAR !colors = ARRAY()
!colors[1] = 'Red'
!colors[2] = 'Green'
!colors[3] = 'Blue'

DO !color VALUES !colors
  $P $!color
ENDDO
```

### Example 4: Creating and Using a Custom Object

```pml
define object Pipe
  member .Name is STRING
  member .Diameter is REAL
endobject

VAR !pipe = object Pipe()
!pipe.Name = 'MainPipeline'
!pipe.Diameter = 24.0
$P 'Pipe Name: ' & !pipe.Name & ', Diameter: ' & !pipe.Diameter.String()
```

---
