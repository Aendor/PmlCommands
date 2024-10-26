# Functions and Procedures in AVEVA PML2

In PML2, functions and procedures are blocks of code that you can reuse throughout your scripts. Functions allow you to pass parameters and optionally return a value, while procedures perform an action without returning a value.

## Table of Contents

1. [Defining Functions](#defining-functions)
2. [Calling Functions](#calling-functions)
3. [Defining Procedures](#defining-procedures)
4. [Calling Procedures](#calling-procedures)
5. [Examples](#examples)

---

## Defining Functions

A function in PML2 is defined using the `define function` statement. Functions can accept parameters and return a value using the `RETURN` keyword.

### Syntax

```pml
define function !!FunctionName(!param1 is DataType, !param2 is DataType) is ReturnType
  -- Function code here
  RETURN value
endfunction
```

- **Parameters**: Defined with `!` prefix, followed by the type (e.g., `REAL`, `STRING`).
- **Return Type**: Specifies the type of value the function will return (e.g., `REAL`, `STRING`).

### Example

This example function calculates the area of a rectangle.

```pml
define function !!CalculateArea(!length is REAL, !width is REAL) is REAL
  VAR !area = !length * !width
  RETURN !area
endfunction
```

---

## Calling Functions

Once a function is defined, you can call it by passing arguments that match the parameter types. The return value can be assigned to a variable.

```pml
VAR !length = 10.0
VAR !width = 5.0
VAR !area = !!CalculateArea(!length, !width)
$P 'Area: ' & !area.String()
```

---

## Defining Procedures

A procedure is similar to a function but does not return a value. Procedures perform specific actions, such as displaying messages or updating values.

### Syntax

```pml
define function !!ProcedureName(!param1 is DataType, !param2 is DataType)
  -- Procedure code here
endfunction
```

### Example

This example procedure displays a greeting message.

```pml
define function !!DisplayGreeting(!name is STRING)
  $P 'Hello, ' & !name
endfunction
```

---

## Calling Procedures

To call a procedure, pass arguments that match the parameter types. Since procedures do not return a value, you simply invoke them without assigning the result.

```pml
!!DisplayGreeting('John')
```

---

## Examples

Here are additional examples to help you work with functions and procedures in PML2.

### Example 1: Function with Multiple Parameters and Return Value

```pml
define function !!CalculateVolume(!length is REAL, !width is REAL, !height is REAL) is REAL
  VAR !volume = !length * !width * !height
  RETURN !volume
endfunction

VAR !length = 10.0
VAR !width = 5.0
VAR !height = 2.0
VAR !volume = !!CalculateVolume(!length, !width, !height)
$P 'Volume: ' & !volume.String()
```

### Example 2: Procedure to Format and Print Text

```pml
define function !!PrintFormattedMessage(!message is STRING, !value is REAL)
  $P !message & ': ' & !value.String()
endfunction

!!PrintFormattedMessage('Total Cost', 250.75)
```

### Example 3: Nested Function Calls

You can call one function within another function for more complex calculations.

```pml
define function !!CalculatePerimeter(!length is REAL, !width is REAL) is REAL
  RETURN 2 * (!length + !width)
endfunction

define function !!CalculateRectangleProperties(!length is REAL, !width is REAL)
  VAR !area = !!CalculateArea(!length, !width)
  VAR !perimeter = !!CalculatePerimeter(!length, !width)
  $P 'Area: ' & !area.String() & ', Perimeter: ' & !perimeter.String()
endfunction

!!CalculateRectangleProperties(10.0, 5.0)
```

---
