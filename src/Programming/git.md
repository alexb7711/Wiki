# Git Configuration

```
[user]
	email = alex.brown7711@gmail.com	// Set user email 
	name = Alex Brown			// Set user name

[merge]
	tool = vimdiff

[mergetool]
	prompt = true

[mergetool "vimdiff"]
	cmd = nvim -d $LOCAL $REMOTE

[core]
	editor = nvim
	autocrlf = input

[help]
	autocorrect = 1 			// Enable fuzzy search on misspelled words

[color]
	ui = auto				// Enables colors when commands are ran in the console
```

# Working Locally With Git
## Viewing History and Diffs
`git log` show the commits made to the repository in reverse chronological order. If you want to see the differences between the commits, you can run

```
git diff #######...#######
```

However, if you don't want to work with the hashes, you can count back from head using `Head~#`, where `#` is a number that represents the commit that many numbers back. For example, 

```
git diff Head~5...Head
```

compares the 5th commit back to the head. You can also shorten the syntax by using

```
git diff Head~5...
```

Git will assume you meant to compare with `HEAD`.

## Undoing Changes In The Working Directory
If you want to undo changes made to a single file, you can run

```
git checkout [file]
```

and by default, it will grab the version from `HEAD` and replace your copy.

## Undoing/Redoing Changes In The Working Directory
```
git reset --hard
```
Resets back to `HEAD`, but doesn't keeps all the changes that you made staged.


```
git reset --soft
```

Resets back to `HEAD`, but keeps all the changes that you made staged.

## Cleaning The Working Copy
If you would like to clear out certain files that you don't need, such as log files or build artifacts. 

```
git clean -n	// Displays what you would do (much like make -n)
git clean -f	// Cleans all shown in git clean -n
```

## Ignoring files With .gitignore
If you don't want to include files, you can use a `.gitignore` to not commit/push those file types or directories. 

```
// .gitignore

[dir]/		// ignores everything in this directory
*.txt		// Ignores all of this filetype
[file].txt	// Ignores this file
