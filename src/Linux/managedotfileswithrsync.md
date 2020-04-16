---
layout: post
title: How to Quickly Manage Dot Files and packages In Linux 
categories: Linux dotfiles
---

If you have used Linux for any period of time (and especially for extended periods of time) you know dot files are a hell of a beast. From ricing you desktop, configuring your shell configuration, to configuring your vimrc. It takes a long time to get things how you want. Considering how quickly you can destroy your install, it is probably a good idea to keep everything backed up. I'm going to talk about a quick way to do that using a simple script, rsync, and GitHub (or another equivalent).

# Introduction to rsync
Rsync (Remote Sync) is a command for copying/synchronizing files and directories locally as well as remotely. In a typically transfer, rsync compares filenames and file timestamps on the source and destination directory trees to assess which files should be transferred. Also, rsync can effectively resume transfers that have been halted or interrupted. Another benefit of using rsync over something like the cp command is that it only syncs the files that have been updated rather than blindly coping everything over every time the command is ran.

The basic syntax of rsync is as follows: 

```
rsync -[flags] [source] [destination]
```

With some common flags being
* -v : verbose
* -a : archive mode
* -z : compress file data
* -h : human-readable
* -r : copies data reccursively
* -P : same as --partial --progress where --partial keeps partially transfered files and --progress shows the progress of each file being transfered
* -t : preserves the time stamps

# Backup Installed Packages
I am using Manjaro, so the following `pacman` commands will work with Arch and its distributions. 

Keeping track of the packages you have installed is extremely easy. To print the list to console all you have to type is:

```
pacman -Qe
```

and you have list of all the packages you manually installed. Now, to make this readable by pacman later (such as if you are doing a re-install) you have to add the flag `-q` to remove all the extra stuff that is included in the output. All that there is left to do is export it to a file. 

# Putting It All Together
To do this part you are going to need to create a simple shell script to grab the files that you want and to export the programs you have installed on your system. The following is the shells script that I am currently using:

```
#!/bin/sh

rsync -atP ~/.bashrc .
rsync -atP ~/.zshrc .
rsync -atP ~/.vim/vimrc .
rsync -atP ~/.Xresources .
rsync -atP ~/.Xdefaults .
rsync -atP ~/.Xmodmap .
rsync -atP /etc/lightdm .
rsync -atP ~/.config/i3 .
rsync -atP ~/.config/polybar .
rsync -atP ~/.config/dunst .
rsync -atP ~/.config/rofi .
rsync -atP ~/.config/mutt .
pacman -Qqe > PackageList.txt
```

If you would like to backup your entire `.config` directory that would simplify the script greatly. Also you can see at the end I have the command `pacman -Qqe > PackageList.txt`. The `>` part exports the output into `Packagelist.txt`. As described above, the command outputs the list of programs you have installed and formats it in a way pacman can read it in later with the command `sudo pacman -Syu < PackageList.txt`.  
