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
