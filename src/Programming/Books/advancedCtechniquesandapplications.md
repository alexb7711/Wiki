---
title: Advanced C Techniques & Applications
header-includes:
	- \usepackage[a4paper, margin=0.5in]{geometry}
	- \fontfamily{qag} 
	- \renewcommand{\familydefault}{\sfdefault}
---

# Programming Style
This chapter presents several methods for solving complex programming in the C language. In particular, the text introduces techniques for dividing large tasks into sets of functions and smaller files so that the programs run efficiently and are easily portable among different C environments.

## Separate Compilation and Information Hiding
The careful use of separate files can be used to hide implementation details. This practice not only simplifies and modularizes the total program, but also prevents the unintended overlap of variable or function names that may occur in a large program, especially if more than one person is involved in program design.

An external element can be defined only once. In addition to specifying type information, the definition allocates storage and may also set initial values. An external name is only visible in the file in which the variable is defined until the end of the file. If the variable or function name is needed at an earlier position in that file or in another file, the name can be declared with the `extern` keyword. 

Information hiding is accomplished through the use of the external static storage class. If an external variable or function is defined with the `static` prefix, the variable can be accessed only within that file. Thus, functions and external variables can be shared throughout a file and yet be totally unknowable in any other file. 

As an example of using `static` to hide methods:

``` C
static int p, g;
static double r, s;

static int f1(a, b);
int a, b;
{
	...
}

static int f2(a, b, c)
char a, b, c
{
	...
}

char utility (x, y, z)
int x, y, z
{
	...
}
```

The function `utility` can make calls to functions `f1` and `f2`, and all three can read and write to the external variables `p`, `g`, `r`, and `s` However, only the `utility` function can be seen from another file. Therefore, if another file contains `extern char utility` at the beginning of the file, functions within that file can gain access to `utility` through a call like `letter = utility(x, y, z)`.

## Header Files
Logically connected groups of constants and data types that are used in different parts of a large program should be collected in a single file (known as a header file) and simply copied (by means of the `#include` facility) into the files that require the use of those elements. Another good general practice is to avoid *hard coding* any numerical constant. Instead, define a suitable name for the constant and refer to that name when the value is needed. 

C provides a technique that easily implements this type of program organization. The `#define` facility replaces a name with a character string throughout a file from the line of the name's definition until the end of the file. The replacement is done by a pre pass by the compiler before any syntactic or semantic analysis is performed. 

### External Variables
Header files are also convenient for declaring external variables and defining structures types. If a set of variables are to be shared by different files, the variables are defined only once, typically in the file containing the main routine. Then, a set of corresponding `extern` declarations can be assembled in separate file called `globals.h`. 

### Structure Types
Similarly, if a group of data types are needed in several files, an entire set of structure type definitions should be put into a single file. 

### Macros with Arguments
Another powerful feature of C is the capability of defining macros with arguments. This facility permits simple functions to be expressed as macros, thereby eliminating the overhead (parameter passing) associated with making function calls. *A single macro can be used with arguments of different data types and so be-have as a generic procedure.* This convenient feature improves the program readability and execution time. 

As an example, the following macro computes the sum of its squares of its arguments:

``` C
// Sum of Squares
#define  SOS(x, y) ((x) * (x) + (y) * (y))
```

A function call and subsequent returns involve a certain amount of overhead; but with the macro, the compiler performs a direct in-line substitution of code. Specifically, on the compiler pre-pass, the compiler replaces the statement 

``` C
e = SOS(a + b, c + d);

// with

e = ((a + b) * (a + b) + (c + d) * (c + d));
```

It is important to note from this example that parenthesis are important to ensure proper mathematical ordering. As a matter of safety, also enclose the entire macro definition in parenthesis. These parenthesis guarantee the correct precedence of operation even when the macro is used as an element in a complex expression. 

## Portability and Hardware Independence
When programming, it is always important to consider potability. Even though you may think that a particular program will always be compiled with a certain compiler and be run only on a given machine, circumstances may change. When new compilers and faster machines appear, a "dedicated application program" is suddenly a candidate for transfer to a new environment. 

The consideration of portability also applies to any piece of code that is specific to a piece of hardware. This limitation typically occurs in input or output routines and may involve such details as the choice of color or monochrome for the display type, the number of horizontal pixels available, the use of specialty defined keys, or the properties of a positioning device like a mouse. 

```
Application Routine -> Generic Interface Routine -> Device Dependent Routine
```

*Any routine of the kind should be written using a layered approach, with the application routine calling the generic routine that make calls to other hardware specific functions*. The application makes calls to a set of interface functions that are to perform the hardware specific tasks. Each of these  interface functions would be implemented using the primitives of the target machine. In this way, the code contained in the application routine will be fixed; only the set of interface routines needs to be changed for a new environment.
