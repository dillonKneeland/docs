# jBASE BASIC (jBC)

<PageHeader />

## Creating a Program

### Create the program file

This file is created as 2 folders (directories) as illustrated below. The first directory is where you place your source code. When a program is compiled, the object code is placed in the second directory, which is simply a data section.

1. Create the program file using the **CREATE-FILE** command with **TYPE** of **JBC**.

```
C:\home>CREATE-FILE TEST.BP TYPE=JBC
[ 417 ] File TEST.BP created , type = UD
[ 417 ] File TEST.BP]MOBJECT created , type = UD
```

2. Edit a program using the JED editor and add the data below.

```
JED TEST.BP PROG1
0001 CRT "Hello World!"
0002 CRT "jBASE is Great!"
```

3. Compile the program.

```
BASIC TEST.BP PROG1
PROG1
BASIC_3.c
Source file PROG1 compiled successfully
```

4. Catalog the program.

```
CATALOG TEST.BP PROG1
PROG1
Object PROG1 cataloged successfully
```

5. Run the program.

```
PROG1
Hello World!
jBASE is Great!
```

Note that steps 2 through 5 can be conveniently achieved with a few key strokes in the jED editor by pressing the **Esc**ape key and entering **FIBCR** (**FI**le, **B**asic, **C**atalog, **R**un) at the **Command-&gt;** prompt.

## Compiling a Program

The **BASIC** command is provided as a front end program to the jBASE jBC compiler. The **jBC** compiler converts the BASIC code into "C" and invokes the native "C" compiler to convert the "C" source code into a machine native object file.

The **BASIC** command creates the object record as $PROGRAM1 in file BP. The BP file can be any file type supported by jBASE, whether it is a hashed file, directory and so on.

The steps used by **BASIC** command are as follows:

- Any supplied record keys with a dollar/pound prefix or a .o or .obj suffix are ignored.
- The source is moved to the current working directory as a temporary file called **BASIC\_nn.c**, where **nn** is the users port number.
- The source is compiled using the **jcompile** command.
- The **.** **o** or **.obj** file is then moved back to the original source file with a dollar/pound prefix and the **.o** or **.obj** suffix removed.
- The command then cleans up any scratch files it created.

## BASIC Command Syntax

```
BASIC {-Options} <filename> <programname> {(Option}
```

| Option | Description |
| --- | --- |
| v           | verbose mode     |
| -wn         | set the warning level to 0, 1, 2 or 3. See later |
| -Ipath       | path for include files |
| (On         | optimize the code, see below |
| (En         | optimize the code. As the (O) option |
| (Wn         | set warning level to 0, 1, 2 or 3, see below |
| (Ipath       | path for include files |
| (V           | allow persistent variables in subroutines |
| (Qq         | specifies that the source code contains embedded SQL statements |

In order to compile and catalog programs and subroutines in jBASE, a 'C' compiler must be installed on the system under the same folder where jBASE is installed. After completing the jBASE installation, one of the optional tasks you can select is to install and configure the compiler. Please refer to the jBASE Installation Guide and rerun the jBASE installer for the option to install the compiler.

## Cataloging a Program

The **CATALOG** command is provided as a front end program to convert object files generated by the BASIC command into main program executables and shared libraries/DLLs of subroutines.

Main program executables by default are copied in the home directory "bin" directory.

Subroutine object files are collated into evenly sized shared libraries and then by default placed in the home directory "lib" directory.

In order to be able to rebuild a shared library, the object file is retained in the "objdir" subdirectory of the "lib" directory. These object files are no longer required once all the shared libraries have been debugged and ready to release.

The **CATALOG** command invokes the jBASE jBuildSLib command with the subroutine object file to construct the shared libraries. The jBuildSLib command then links several object files together with relevant references to other required libraries and creates a shared library/DD.

It should be noted that every time a subroutine is cataloged, jBuildSLib is invoked to rebuild the shared library/DLL. However, when the **CATALOG** command is issued with an active select list of program names, the rebuilding is deferred until the list has been fully processed. This means that each shared object/DLL is only rebuilt once, as opposed to once for each subroutine. So when cataloging subroutines, it is much faster to work from an active select list. The same is true when decataloging subroutines.

## CATALOG Command Syntax

```
CATALOG {-Options} <filename> <programname>
```

| Option | Description |
| --- | --- |
| v           | verbose mode     |
| Llib         | alternative lib directory to use for shared libraries |
| obin         | alternative bin directory to use for executables |
| cExternalLibs | external C library functions |

Back to [Getting Started](./../../README.md)

<PageFooter />