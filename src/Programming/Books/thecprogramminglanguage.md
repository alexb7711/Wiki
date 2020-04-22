---
title: The C Programming Language
header-includes:
	- \usepackage[a4paper, margin=0.5in]{geometry}
	- \fontfamily{qag} 
	- \renewcommand{\familydefault}{\sfdefault}
---

# Types, Operators, and Expressions
## Constants
A character constant is an integer, written as one character within single quotes such as 'x'. The value of a character constant is the numeric value of the character in the machine's character set. For example, '0' has the value 48 in ASCII.

Certain characters can be expressed in character and string constants by escape sequences like `\n`. In addition, an arbitrary byte-sized bit pattern can be specified by `\ooo`, where `ooo` is one to three octal digits (0...7) or by `\xhh` where `hh` is one or more hexadecimal digits (0..9, a...f, A...F). So as an example, you can write:

``` C
#define VTAB '\013'	// ASCII vertical tab
#define BELL '\007'	// ASCII bell character
```

or in hexadecimal,

``` C
#define VTAB '\xb'	// ASCII vertical tab
#define BELL '\x7'	// ASCII bell character
```

The complete set of escape sequences is:

```
\a       alert (bell) character
\b       backspace
\f       formfeed
\n       newline
\r       carriage return
\t       horizontal tab
\v       vertical tab
\\       backslash
\?       question mark
\′       single quote
\"       double quote
\0	 null character
\ooo	 octal number
\xhh	 hexadecimal number
```

## Increment and Decrement Operators
An example of when to use `++i` rather than `i++`:

``` C
/* squeeze:  delete all c from s */

void squeeze(char s[], int c)

{

    int i, j;



    for (i = j = 0; s[i] != ′\0′; i++)

        if (s[i] != c)

            s[j++] = s[i];

    s[j] = ′\0′;

}
```

This is the same code as:

``` C
if (s[i] != c)
{

    s[j] = s[i];

    j++;

}
```

## Bitwise Operators
C provides six operators for bit manipulation; these may only be applied to integral operands, that is, `char`, `short`, `int`, and `long`, whether signed or unsigned.

```
&    bitwise AND
|    bitwise inclusive OR
^    bitwise exclusive OR
<<   left shift
>>   right shift
~    one’s complement (unary)
```

`~` yield's one's compliment of an integer; that is, it converts each 1-bit into a 0-bit and vice versa.

# Control Flow
## Break and Continue
The `break` statement provides an early exit from `for`, `while`, and `do`, just as it does from `switch`. **A `break` causes the innermost enclosing loop or switch to be exited immediately.**

The `continue` statement is related to `break`, but less often used; **it causes the next iteration of the enclosing `for`, `while`, or `do` loop to begin.** In the `while` and `do`, this means that the test part is executed immediately; in the `for`, control passes to the increment step. This statement only applies to loops, not to a `switch`.

## GoTo and Labels
`goto` is almost never needed, but it can be useful in situations such as abandoning a process in some deeply nested structure, such as breaking out of two or more loops at once as shown below:

``` C
for ( ... )

    for ( ... ) {

        ...

        if (disaster)

            goto error;

    }

...

error:
	// Clean up the mess
```

# Functions and Program Structure
## Static Variables
The `static` declaration, applied to an external variable or function, limits the scope of that object to the rest of the source file being compiled

# Types, Operators, and Expressions
## Constants
A character constant is an integer, written as one character within single quotes such as 'x'. The value of a character constant is the numeric value of the character in the machine's character set. For example, '0' has the value 48 in ASCII.

Certain characters can be expressed in character and string constants by escape sequences like `\n`. In addition, an arbitrary byte-sized bit pattern can be specified by `\ooo`, where `ooo` is one to three octal digits (0...7) or by `\xhh` where `hh` is one or more hexadecimal digits (0..9, a...f, A...F). So as an example, you can write:

``` C
#define VTAB '\013'	// ASCII vertical tab
#define BELL '\007'	// ASCII bell character
```

or in hexadecimal,

``` C
#define VTAB '\xb'	// ASCII vertical tab
#define BELL '\x7'	// ASCII bell character
```

The complete set of escape sequences is:

```
\a       alert (bell) character
\b       backspace
\f       formfeed
\n       newline
\r       carriage return
\t       horizontal tab
\v       vertical tab
\\       backslash
\?       question mark
\′       single quote
\"       double quote
\0	 null character
\ooo	 octal number
\xhh	 hexadecimal number
```

## Increment and Decrement Operators
An example of when to use `++i` rather than `i++`:

``` C
/* squeeze:  delete all c from s */

void squeeze(char s[], int c)

{

    int i, j;



    for (i = j = 0; s[i] != ′\0′; i++)

        if (s[i] != c)

            s[j++] = s[i];

    s[j] = ′\0′;

}
```

This is the same code as:

``` C
if (s[i] != c)
{

    s[j] = s[i];

    j++;

}
```

## Bitwise Operators
C provides six operators for bit manipulation; these may only be applied to integral operands, that is, `char`, `short`, `int`, and `long`, whether signed or unsigned.

```
&    bitwise AND
|    bitwise inclusive OR
^    bitwise exclusive OR
<<   left shift
>>   right shift
~    one’s complement (unary)
```

`~` yield's one's compliment of an integer; that is, it converts each 1-bit into a 0-bit and vice versa.

# Control Flow
## Break and Continue
The `break` statement provides an early exit from `for`, `while`, and `do`, just as it does from `switch`. **A `break` causes the innermost enclosing loop or switch to be exited immediately.**

The `continue` statement is related to `break`, but less often used; **it causes the next iteration of the enclosing `for`, `while`, or `do` loop to begin.** In the `while` and `do`, this means that the test part is executed immediately; in the `for`, control passes to the increment step. This statement only applies to loops, not to a `switch`.

## GoTo and Labels
`goto` is almost never needed, but it can be useful in situations such as abandoning a process in some deeply nested structure, such as breaking out of two or more loops at once as shown below:

``` C
for ( ... )

    for ( ... ) {

        ...

        if (disaster)

            goto error;

    }

...

error:
	// Clean up the mess
```

# Functions and Program Structure
## Static Variables
<<<<<<< Updated upstream
The `static` declaration, applied to an external variable or function, limits the scope of that object to the rest of the source file being compiled.
=======
The `static` declaration, applied to an external variable or function, limits the scope of that object to the rest of the source file being compiled

# Pointers and Arrays
In C, there is a strong relationship between pointers and arrays. Any operation that can be achieved by array subscripting can also be done with pointers. The pointer version will generally be faster, but at least to the uninitiated, somewhat harder to understand. 

If you look at an array, indexing it via `array[i]`, is the same way as indexing it via `&array[0] + i`. `&array[0]`, is the pointer to the first item in the array, if we have a value I added on to it, that will move down the array as shown in Figure \ref{fig:arraypointerexample}

![Using pointers to index an array \label{fig:arraypointerexample}](https://learning.oreilly.com/library/view/the-c-programming/9780133086249/graphics/98med03.jpg)

Using this line of thinking, it is possible to then pass part of an array to a function:

``` C
foo(&a[2]);
// or
foo(a+2);
```

Where the function `foo`'s arguments have the form of:

``` C
foo(int arr[]) {...}
// or
fo(int* arr) {...}
```

As far as `foo` is concerned, the fact that the parameter refers to part of a larger array is of no consequence. 

## Address Arithmetic 
Because memory is allocated sequentially, we can use mathematical comparisons to see if we have enough memory allocated in a buffer, to see a position of a value in an array, etc. For example:

``` C
if (allocbuf + ALLOCSIZE - allocp >= n)		// Checks if the buffer is large enough
// or
if (p >= allocbuf && p < allocbuf + ALLOCSIZE)	// Checks if the pointer is within the buffer range
```

## Character Pointers and Functions
A string constant is written as `"I am a string"`. It is represented as an array of characters and is terminated with a `\0`. 

When a character string appears, it is accessed through a character pointer. For example

``` C
printf("Hello, World!\n");
```

takes the pointer of the start of the character string.

If you declare a character pointer as follows:

``` C
char* pmessage;
```

then the statement

``` C
pmessage = "Hello, World!";
```

Assigns `pmessage` to the "Hello, World!". This is *not* a copy; only pointers are involved. C does not provide any operators for processing an entire string of characters as a unit.

## Pointer Arrays; Pointers to Pointers
To create an array of pointers, we can say:

```
char* lineptr[10];	// Array of character pointers
```

## Multi-Dimensional Arrays
C provides rectangular multi-dimensional arrays, although in practice they are much less used than arrays of pointers.

**If a two-dimensional array is to be passed to a function, the parameter declaration in the function must include the number of columns; the number of rows is irrelevant, since what is passed is, as before, a pointer to an array of rows.

``` C
foo (int daytab[2][13] {...}
// or
foo (int daytab[][13] {...}
// or
foo (int (*daytab)[13] {...}
```
It is necessary to have the parenthesis in the last version since brackets `[]` have higher precedence than *. Without the parenthesis 

``` C
int* daytab[13]
```

is an array of 13 pointers to integers. More generally, only the first dimension of an array is free; all others have to be specified.

## Initialization of Pointer Arrays
``` C
char* array_of_pointers[] = 
{
	"Item 1",
	"Item 2",
	...
}
```

## Pointers vs. Multi-Dimensional Array
The big difference between

``` C
int a[10][20];
// and
int* b[10];
```

Is that the first one allocates all 10x20 array, the second only allocates 10 integer pointers. Initialization must be done explicitly either statically or with code. The important advantage of the pointer array is that the rows of the array may be of different lengths.

## Command Line Arguments
When `main` is called, it is called with two arguments. The first (conventionally called `argc` for argument count) is the number of command-line arguments. The second (`argv`, for argument vector), is a pointer to an array of character strings that contain the arguments, one per string. We customarily use multiple levels of pointers to manipulate these character strings. 

### Accepting Command Line Flags
``` C
#include <stdio.h>

#include <string.h>

#define MAXLINE 1000



int getline(char *line, int max);



/* find:  print lines that match pattern from 1st arg */

main(int argc, char *argv[])

{

    char line[MAXLINE];

    long lineno = 0;

    int c, except = 0, number = 0, found = 0;



    while (--argc > 0 && (*++argv)[0] == ′-′)

        while (c = *++argv[0])

            switch (c) {

            case ′x′:

                except = 1;

                break;

            case ′n′:

                number = 1;

                break;

            default:

                printf("find: illegal option %c\n", c);

                argc = 0;

                found = −1;

                break;

            }

    if (argc != 1)

        printf("Usage: find -x -n pattern\n");

    else

        while (getline(line, MAXLINE) > 0) {

            lineno++;

            if ((strstr(line, *argv) != NULL) != except) {

                if (number)

                    printf("%ld:", lineno);

                printf("%s", line);

                found++;

            }

        }

    return found;

}
```

## Pointers To Functions
In C, it is possible to define pointers to functions which can be assigned, placed in arrays, passed to functions, returned by functions, and so on. 

The generic `void*` is used for pointer arguments. Any pointer can be cast to `void*` and back again without loss of information. 

When creating a function that accepts function pointers:

``` C
void qsort (void* v[], int left, int right, int (*comp)(void*, void*))
```

Says that `comp` is a pointer to a function that has two `void*` as arguments.

## Complicated Declarations
``` C
char **argv

    argv:  pointer to pointer to char

int (*daytab)[13]

    daytab:  pointer to array[13] of int

int *daytab[13]

    daytab:  array[13] of pointer to int

void *comp()

    comp:  function returning pointer to void

void (*comp)()

    comp:  pointer to function returning void

char (*(*x())[])()

    x: function returning pointer to array[] of

    pointer to function returning char

char (*(*x[3])())[5]

    x: array[3] of pointer to function returning

    pointer to array[5] of char
```
