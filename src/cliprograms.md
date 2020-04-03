# Command Line Interface Programs

## Debugging
### General Steps to Start Debugging
* Compile the program using the `-g` flag to signify debugging. `gcc -g program.c -o program`
* Run `gdb ./program`

### Visualizing Code
* Type `layout next` or `Ctrl-X A` to show code visually, the box that shows up should be empty because the program has not started yet.
* Type `Ctrl-X 2` will bring up 2 windows. If you type `Ctrl-X 2` again, it will cycle through the windows.

# Running and Navigating Code
* You can type `start` which will start the program at line 1, but wont run anything yet. It allows you to step from the beginning of the program.
* If you wish to start the program now, type `run` or `r`.
* If you type `Ctrl-C` that will pause the program 
* Typing `next` or `n` will step over the next line
* Typing `step` will step into the next line
* Continue: `continue`
* If your program takes inline commands, you can either set them while you run gdb or you can run gdb normally and type `set args ARGS`

### Debugging Commands
* Set a break point: `break POINT` or `b POINT`, can be a line number, function, file name, etc.
	* `break function`
	* `break filename:line#`
	* `break filename:function`
* Print a variable's value: `print VARIABLE`
* Print an array: `print *arr@len`
	* The `*` is used to de-reference the array just like you would in C
* Watch a variable for changes: `watch VARIABLE`
* You can clear breakpoints at a point, function, or file by specifying `clear LINE`, `clear FUNCTION`, or `clear FILE`.
* If you have a program that crashes you can run `backgrace full` to see the line that it crashes.
* You can run commands at breakpoints by typing `command BREAKPOINT#`

### Debugging a Process
* Get the process ID of the program you are looking for. While you have gdb open you can run `shell ps -C program -o pid h`
* Then you can attach the program by running: `attach pid`

### Useful GDB Commands
* Refresh Display: `refresh` (or control-L)
* Up and down arrows scrolls through the code in the `layout next` display
* `Ctrl-p` and `Ctrl-n` cycles up and down through command line history
* `set print pretty on` makes gdb print structures and classes more neatly
* You can run shell commands by typing `shell` then the command you wish to run

## Diff & Patch
### diff-ing and patching
Diff is a usefull command to determine the difference between files and directories. It comes in handy when you are trying to figure out edits that someone has done on a file or if you are trying to create a patch to merge the files or directories (like a git merge). 

#### Introduction to diff-ing lingo
Diff-ing two files is pretty easy to do, the only thing to have to do is
``` shell
diff [file1] [file2]
```
which will output to the console the differences in the file. Below is a sample output:
``` shell
1c1
< These are a few words.
 No newline at end of file
---
> These still are just a few words.
 No newline at end of file
```

The `1c1` is a way of indicating line numbers and the task to be done on the differences. In this instance it is saying "change the lines from row 1 to row 1". If it were something like `12c15` it would mean "changes the lines from row 12 to row 15". The other characters you may see are "a" (append or add) or "d" (delete). 

The "<" indicates that the patch should remove the characters after the sign, and ">" means that the characters after this sign should be added. Extrapolating on this, when you see a "c" between the line numbers in the output, you will always see both < and > (adding and removing). When you see an "a", you will only see the > sign (because we are only adding to a line). Lastly, if you see a "d" you will only see the < sign (because we are deleting lines).

#### Creating A Simple Patch
Creating a patch is pretty simple. To do so, we use the same syntax as creating a diff but instead output it to a directory. As and example: 
``` shell
diff [file1] [file2] > patchFile.patch
```

#### Applying A Simple Patch
Rather than patching two files together, we can use the patch file and the original document to create a new document that has all the edits specified by the patch file. This can be done by running:

``` shell
patch [file1] -i patchFile.patch -o [file2]
```

#### Contextual Patching
To save ourselves some time and effort we can use contextual patching. What this does is includes more metadata about the files that are being diff-ed. For example running:
``` shell
diff -c [file1] [file2]
```
will output something like

``` shell
*** originalfile        2007-02-03 22:15:48.000000000  0100
--- updatedfile 2007-02-03 22:15:56.000000000  0100
***************
*** 1 ****
! These are a few words.
--- 1 ----
! These still are just a few words.
```

Because there is more information about the files being diff-ed, patching becomes a little more simple: 

``` shell
patch -i patchFile.pactch -o [file2]
```

### Diff-ing Directories
The easiest way to do this is by running:

``` shell
diff [directory1]/ [directory2]/ > patchFile.patch
```

or for contextual diff-ing

``` shell
diff -c [directory1]/ [directory2]/ > patchFile.patch
```

To patch these without contextual diff-ing:

```shell
patch -c [directory1]/ [directory2]/ -i patchFile.patch -o [directory2]/
```

or with using contextual diff-ing

``` shell
patch -p0 -i patchFile.patch -o [directory2]/
```

The `-p0` flag indicates to not remove the directory paths so patch has context.

### Reversing A Patch
``` shell
patch -p0 -R -i patchFile.patch
```
## Grep
### Searching a project
`grep -H -r 'what_you_search' *.c | less`

Where: 
* -H prints out the filename
* -r recurssive search
