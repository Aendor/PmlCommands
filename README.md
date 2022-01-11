# PML Function Examples

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

This repository shows examples of PML Functions

  - Sample PML1 functions
  - Sample PML2 functions

**Startup:**
```sh
[path]\diagrams.bat XXX SYSTEM/[password] /[MDB] DIAGRAMS
[path]\engineering.bat XXX SYSTEM/[password] /[MDB] TAGS
[path]\diagrams.bat TTY XXX SYSTEM/XXXXXX /ALL %1%

[path]\Diagrams14.1.1\mon.exe" tty -macro="[path]\publishAllDiagramsToAVEVANET.pmlmac" PROD DIAGRAMS init "[path]\Diagrams14.1.1\diagrams.init"
"[path]\Engineering15.3.0\mon.exe" tty -macro="[path]\extractDBViewsToAVEVANET.pmlmac" PROD ENGINEERING init "[path]\Engineering15.3.0\engineering.init"

```

**Database modification information:**
```sh
LASTMOD
USERMOD
```

**List user directory:**
```sh
evar pdmsuser
```

**To see all commands on the commandline when you running a process:**
```sh
$R6
```

**Query Enviroment Variables:**
```sh
q evar 'AVEVA_DESIGN_WORK'
var !a evar pdmsuser
q !a
```

**Modify a standard report:**
```sh
CALLIBR XREPSEL MODIFY
```

**Create a standard report:**
```sh
CALLIBR XREPDEF
```

**Set Decimals:**
```sh
preci 2 deci
```

**Clock:**
```sh
CLOCK DATE
CLOCK TIME
```

**Change the database primary location:**
```sh
CHANGE TEST/TESTDESI PRIMARY AT HUB
```

**Change the team name:**
```sh
CN DB TEAMNAME/TESTDESI NEWNAME/TESTDESI
```

**Create an ENGWLD:**
```sh
NEW ENGWLD /ENGI_DATA_PROC DB ENGIPROC/ENGI_DATA_PROC
NEW XPIWLD /PROC_XPI DB ENGIPROC/ENGI_DATA_PROC
```

**Show the Include form:**
```sh
SHOW _CDCINCLUDE
```

**Write to text file:**
```sh
var variable COLLECT ALL element FOR array

!file = object File('filename')
!result = ARRAY()

do element values variable
    !ref = element.DBREF()
    !name = !ref.NAME
    
    !output = !name
    !result.Append(!output)
enddo

!file.WriteFile('WRITE', !result)
```

**Using Specon Mode in Paragon:**
```sh
SPECONMODE

ALPHA LOG /C:\temp\spec.txt
  OUT NEW /AAAA
ALPHA LOG END

EXIT
```
**Change Specification Name:**
```sh
CHANGE 'NEW SPECIFICATION' TO 'OLD SPECIFICATION'
```

**Create a DB LISTING:**
```sh
call !!displayOutput('Datal')
```

**Move item across databases:**
```sh
INCLUDE ACROSSDB /ITEM
```

**Backtrack with removing previous sessions:**
```sh
BACKTRACK [Team name]/[DB name] TO SESSION 2
```

**Delete all members:**
```sh
DELETE SCGROU MEM
```

**Message Box:**
```sh
!!Alert.Message('HELLO')
```

**PML Definition:**
```sh
!!PMLDefinition('SBMCloneObjects')
```

**UNDO TRANSACTION:**
```sh
PREVOWNER [Team Name]/[Database Name]
```

**Empty USER directory:**
```sh
C:\Users\Public\DOCUME~1\AVEVA\USERDATA
C:\Users\[User Name]\AppData\Local\AVEVA
```

**Show old members menu:**
```sh
SHOW _CDCMEMBER FREE
```

**Show all LINK database references:**
```sh
GOTO CMPLNK
```

**Change DB location:**
```sh
CHANGE [Team name]/[DB name] PRIMARY AT HUB
```

**Turn PML events off:**
```sh
!!PMLEVENTS = 'OFF'
```

**Read data from .xls file:**
```sh
–Open Forms\Hide
show !!spreadsheetimport
hide !!spreadsheetimport
!!spreadsheetImport.setDataHandler(object EQUILOADER())
!!spreadSheetImport.filename.val = 'c:\PipeImport.xls' $* Excel PATH
!!spreadSheetImport.loadData()
–Find first column names
!array = ARRAY()
do !rowVals values !!spreadSheetImport.dataGrid.getrows()
!row =''
do !rowVal indice !rowVals
!sep = ''
if(!rowVal.eq(1).not())then
!sep = ' '
endif
!row = !row + !sep + !rowVals[!rowVal]
enddo
!array.append(!row)
enddo
q var !array

Output:
[1] '100-B-1 PIPE 1'
[2] '100-B-2 PIPE 2'
```

**Show naming rules in Engineering:**
```sh
show !!namoptedit
```

**Autoname CE:**
```sh
!!autoNameCe(true)
```

**AutoRename:**
```sh
UNNAME
!!autoNameCe(true)
```

**Get autoname result:**
```sh
!dbref = REF
!name = !!namOpt.nameString(!dbref, '', true, true)
$P $!name
```
**Using the KEYCOPY command:**
```sh
KEYCOPY [uda name]
```

**Using the "OF" keyword:**
```sh
Q DESC OF [TYPE] /ITEM
Q [attribute name]\[Distributed attribute name][1] OF ENGITE /118-LPAI-2132 
```

**Show all pml files in use on a project:**
```sh
show !!pmlbrowser
```

**Set DB file name to be the same as the db number:**
```sh
Fino 0
```

**Convert to units and nearest bore:**
```sh
!!CE.:SPECOREF.CATREF.PARAM[1].ConvertUnits('INCH').NearestBore()
```

**Find all distributed attributes:**
```sh
XRLIST
```

### Additional Info
*Import AutoCad file in Visio; only for AutoCAD version 2007*
