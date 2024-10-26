# Advanced Examples and Patterns in AVEVA PML2

This section provides advanced PML2 examples and patterns for handling complex tasks. These examples demonstrate database management, custom reporting, and working with environment variables, allowing you to extend the capabilities of your PML2 scripts.

## Table of Contents

1. [Exporting Data to CSV](#exporting-data-to-csv)
2. [Database Management](#database-management)
   - [Moving Items Across Databases](#moving-items-across-databases)
   - [Backtracking Sessions](#backtracking-sessions)
   - [Reconfiguring Databases](#reconfiguring-databases)
3. [Environment Variables](#environment-variables)
4. [Automated Reports](#automated-reports)
5. [Excel Data Import](#excel-data-import)

---

## Exporting Data to CSV

This example collects specific items (e.g., pipes) and exports their names and attributes to a CSV file.

```pml
define function !!ExportPipeDataToCSV()
  VAR !pipes COLLECT ALL WITH TYPE :Pipe
  VAR !file OPENFILE 'PipeData.csv' WRITE
  IF (!file.Error() EQ FALSE) THEN
    !file.WriteLine('PipeName,Diameter,Length')    -- CSV Header
    DO !pipe VALUES !pipes
      VAR !line = $!pipe.NAME & ',' & !pipe.DIAMETER.String() & ',' & !pipe.LENGTH.String()
      !file.WriteLine(!line)
    ENDDO
    !file.Close()
  ELSE
    $P 'Error: Could not open file for writing.'
  ENDIF
endfunction

!!ExportPipeDataToCSV()
```

---

## Database Management

### Moving Items Across Databases

You can use the `INCLUDE ACROSSDB` command to move items from one database to another. This example demonstrates how to move an item across databases within AVEVA.

```pml
INCLUDE ACROSSDB /ITEM_NAME
```

### Backtracking Sessions

The `BACKTRACK` command allows you to roll back to a specific session, which is helpful for restoring a previous state of the database.

```pml
BACKTRACK TEAM_NAME/DB_NAME TO SESSION 2
```

### Reconfiguring Databases

Reconfiguring a database can help apply new configurations across items. This example shows how to use `RECONFIGURE` on a copied item.

```pml
FROM DB SOURCE_DB TO DB TARGET_DB
RCFCOPY /ITEM_NAME
RECONFIGURE
```

---

## Environment Variables

Environment variables can be queried and set within AVEVA PML2. Use `evar` to retrieve information and `q evar` to display specific environment variables.

```pml
-- Query an environment variable
q evar 'AVEVA_DESIGN_WORK'

-- Set and retrieve a custom environment variable
var !userEnv evar pdmsuser
q !userEnv
```

---

## Automated Reports

Automating reports with PML2 allows you to generate consistent output based on specific filters or criteria. This example demonstrates how to generate a standard report and modify it.

```pml
CALLIBR XREPSEL MODIFY     -- Modify an existing report
CALLIBR XREPDEF            -- Define a new report
```

---

## Excel Data Import

Importing data from Excel can be done with the `spreadSheetImport` object. This example demonstrates reading data from an Excel file and processing it row by row.

```pml
-- Define the path to the Excel file
!!spreadSheetImport.filename.val = 'C:\data\PipeData.xls'

-- Load data from the file
!!spreadSheetImport.loadData()

-- Process the data from the first row
VAR !dataArray = ARRAY()
DO !row VALUES !!spreadSheetImport.dataGrid.getRows()
  VAR !dataLine = ''
  DO !cell INDICE !row
    VAR !separator = (IF !cell EQ 1 THEN '' ELSE ' ' ENDIF)
    !dataLine = !dataLine & !separator & !row[!cell]
  ENDDO
  !dataArray.Append(!dataLine)
ENDDO

-- Output results
DO !line VALUES !dataArray
  $P $!line
ENDDO
```

---
