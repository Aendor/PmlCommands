# File Handling in AVEVA PML2

File handling in PML2 allows you to read from and write to files, which is useful for data export, logging, and configuration management. This guide covers opening files, reading and writing data, and handling errors.

## Table of Contents

1. [Opening Files](#opening-files)
2. [Writing to Files](#writing-to-files)
3. [Reading from Files](#reading-from-files)
4. [Closing Files](#closing-files)
5. [Error Handling](#error-handling)
6. [Examples](#examples)

---

## Opening Files

To work with files in PML2, use the `OPENFILE` command to open a file in `READ` or `WRITE` mode.

- **WRITE Mode**: Creates a new file or overwrites an existing file.
- **READ Mode**: Opens an existing file to read its content.

```pml
VAR !file OPENFILE 'output.txt' WRITE   -- Opens the file for writing
VAR !file OPENFILE 'input.txt' READ     -- Opens the file for reading
```

## Writing to Files

After opening a file in `WRITE` mode, you can use the `WriteLine` method to add text to the file.

```pml
VAR !file OPENFILE 'output.txt' WRITE
IF (!file.Error() EQ FALSE) THEN
  !file.WriteLine('This is the first line.')
  !file.WriteLine('This is the second line.')
  !file.Close()
ELSE
  $P 'Error opening file for writing.'
ENDIF
```

## Reading from Files

To read from a file, open it in `READ` mode and use `ReadLine` to read each line. You can use a `WHILE` loop to read until the end of the file.

```pml
VAR !file OPENFILE 'input.txt' READ
IF (!file.Error() EQ FALSE) THEN
  WHILE (!file.EOF() EQ FALSE) DO
    VAR !line = !file.ReadLine()
    $P $!line
  ENDDO
  !file.Close()
ELSE
  $P 'Error opening file for reading.'
ENDIF
```

## Closing Files

Always close a file after you finish reading or writing to ensure data is saved and resources are freed.

```pml
!file.Close()
```

## Error Handling

The `Error()` method checks if an error occurred when opening a file. This is useful for confirming that a file was opened successfully before attempting to read or write.

```pml
VAR !file OPENFILE 'data.txt' WRITE
IF (!file.Error() EQ TRUE) THEN
  $P 'Failed to open file.'
ENDIF
```

---

## Examples

Here are examples of common file-handling tasks in PML2.

### Example 1: Writing Data to a CSV File

This example collects data and writes it to a CSV file with headers.

```pml
define function !!ExportDataToCSV()
  VAR !file OPENFILE 'data.csv' WRITE
  IF (!file.Error() EQ FALSE) THEN
    !file.WriteLine('ID,Name,Value')    -- Write header
    VAR !data ARRAY()
    !data[1] = '1,ItemA,100'
    !data[2] = '2,ItemB,200'
    DO !row VALUES !data
      !file.WriteLine($!row)
    ENDDO
    !file.Close()
  ELSE
    $P 'Error: Could not open file for writing.'
  ENDIF
endfunction

!!ExportDataToCSV()
```

### Example 2: Reading and Displaying File Content

This example reads each line from a text file and displays it.

```pml
VAR !file OPENFILE 'log.txt' READ
IF (!file.Error() EQ FALSE) THEN
  WHILE (!file.EOF() EQ FALSE) DO
    VAR !line = !file.ReadLine()
    $P $!line
  ENDDO
  !file.Close()
ELSE
  $P 'Error: Could not open file for reading.'
ENDIF
```

### Example 3: Appending Data to a File

To append data to a file without overwriting, you can use a custom method that opens the file, writes data, and then closes it.

```pml
define function !!AppendToFile(!filename is STRING, !data is STRING)
  VAR !file OPENFILE !filename WRITE
  IF (!file.Error() EQ FALSE) THEN
    !file.WriteLine(!data)
    !file.Close()
  ELSE
    $P 'Error: Could not open file for writing.'
  ENDIF
endfunction

!!AppendToFile('output.txt', 'New entry added.')
```

---
