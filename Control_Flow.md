# Control Flow in AVEVA PML2

Control flow allows you to manage the execution order of commands in your PML2 scripts. In this section, you’ll learn about conditional statements and loops to control your program’s logic.

## Table of Contents

1. [Conditional Statements](#conditional-statements)
   - [IF Statements](#if-statements)
   - [IF-ELSE Statements](#if-else-statements)
2. [Loops](#loops)
   - [DO Loop (Fixed Count)](#do-loop-fixed-count)
   - [DO VALUES Loop (Array/Collection)](#do-values-loop-arraycollection)
   - [Loop with Step](#loop-with-step)
3. [Examples](#examples)

---

## Conditional Statements

Conditional statements allow you to execute code based on specific conditions.

### IF Statements

An `IF` statement checks a condition and executes code only if the condition is true. Use `IF` to perform actions based on the current state of variables.

```pml
VAR !count = 10
IF (!count GT 5) THEN
  $P 'Count is greater than 5'
ENDIF
```

### IF-ELSE Statements

An `IF-ELSE` statement provides an alternative block of code to execute if the condition is false.

```pml
VAR !count = 3
IF (!count EQ 5) THEN
  $P 'Count is equal to 5'
ELSE
  $P 'Count is not equal to 5'
ENDIF
```

### Nested IF Statements

You can nest `IF` statements within other `IF` statements to check multiple conditions in sequence.

```pml
VAR !score = 85
IF (!score GT 90) THEN
  $P 'Grade: A'
ELSE
  IF (!score GT 70) THEN
    $P 'Grade: B'
  ELSE
    $P 'Grade: C'
  ENDIF
ENDIF
```

---

## Loops

Loops allow you to repeat a block of code multiple times, which is useful for iterating through arrays or performing repeated actions.

### DO Loop (Fixed Count)

The `DO` loop repeats a block of code a specific number of times. Set the start, end, and optional step value.

```pml
DO !i = 1 TO 5
  $P 'Iteration: ' & !i
ENDDO
```

### DO VALUES Loop (Array/Collection)

The `DO VALUES` loop iterates through each element in an array or collection, executing the loop for each item.

```pml
VAR !colors = ARRAY()
!colors[1] = 'Red'
!colors[2] = 'Green'
!colors[3] = 'Blue'

DO !color VALUES !colors
  $P $!color
ENDDO
```

### Loop with Step

You can specify a step value in a `DO` loop to control the increment between iterations.

```pml
DO !i = 1 TO 10 STEP 2
  $P 'Step Iteration: ' & !i
ENDDO
```

---

## Examples

Here are a few examples that combine control flow elements.

### Example 1: Checking Conditions with IF-ELSE

```pml
VAR !temperature = 75
IF (!temperature GT 85) THEN
  $P 'It’s hot outside'
ELSE
  IF (!temperature GT 60) THEN
    $P 'It’s warm outside'
  ELSE
    $P 'It’s cold outside'
  ENDIF
ENDIF
```

### Example 2: Looping through an Array with DO VALUES

```pml
VAR !fruits = ARRAY()
!fruits[1] = 'Apple'
!fruits[2] = 'Banana'
!fruits[3] = 'Cherry'

DO !fruit VALUES !fruits
  $P 'Fruit: ' & $!fruit
ENDDO
```

### Example 3: Using a DO Loop with Step

```pml
DO !i = 10 TO 0 STEP -2
  $P 'Countdown: ' & !i
ENDDO
```

---
