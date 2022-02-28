---
layout: post
title: Must know CLI-commands for Data Scientists
---

## File system

### pwd - print working directory

```pwd``` prints the absolute path of your current working directory

```CLI
$ pwd 
/home/myuser
```

### ls - list

```ls``` lists all contents of your current directory (the one displayed by pwd) 

```CLI
$ ls 
data  info.txt  R 
```

```ls /home``` lists all contents of the directory /home (absolute directory)
```ls data``` lists all contents of the directory data (relative directory)
```ls -al``` lists all contents of the current directory, including hidden files and showing additional information

### cd - change directory

Use ```cd``` to change directory

```CLI
$ pwd 
/home/myuser
$ cd tmp
$ pwd
/home/myuser/tmp
```

Use ```cd ..``` to change to parent directory
Use ```cd ./R``` to change to directory R (from your current directory)
Use ```cd ~``` to change to your home directory

### cp - copy




