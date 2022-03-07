---
layout: post
title: Must know CLI-commands for Data Scientists
---

Learn the most important Linux CLI commands that help you become a more efficient and productive data scientist!

## Intro

CLI stands for Command Line Interface. It is a program that accepts text input to execute operating system functions. Bash is a popular Unix shell to run CLI commands.

* Use ```man``` to view the manual of a command. Example: ```man man``` shows the manual for the ```man``` command. Use Space to skip to the next page and :q to quit.
* Use ```hist``` to show the history of commands used
* Use "Up Key" to show the last command
* Use "Tab Key" for auto-completion
* Use ```>``` to redirect the output from screen to a file 
(e.g. ```ls > out.txt``` writes the output of the ls command into the file out.txt)
* Use ```|``` to "pipe" the output from one command as input for the next command 
(e.g. ```head -n 10 info.txt | tail -n 2``` takes the first ten lines of info.txt and then shows the last 2 lines of those 10 lines)
* Use ```Ctrl + C``` to stop a running program

## Files & Directories

### pwd (print working directory)

```pwd``` prints the absolute path of your current working directory

```console
$ pwd 
/home/myuser
```

### ls (list)

```ls``` lists all contents of your current directory (the one displayed by pwd) 

```console
$ ls 
data  info.txt  R 
```

* ```ls /home``` lists all contents of the directory /home (absolute directory)
* ```ls data``` lists all contents of the directory data (relative directory)
* ```ls -al``` lists all contents of the current directory, including hidden files and showing additional information
* ```ls -R``` lists everything underneath a directory

### cd (change directory)

Use ```cd``` to change directory

```console
$ pwd 
/home/myuser
$ cd tmp
$ pwd
/home/myuser/tmp
```

* Use ```cd ..``` to change to parent directory
* Use ```cd ./R``` to change to directory R (from your current directory)
* Use ```cd ~``` to change to your home directory

### cp (copy)

```cp``` let you copy a file or directory

```console
$ ls 
data  info.txt  R 
$ cp info.txt info2.txt
$ ls 
data  info.txt  info2.txt  R 
```

You can copy multiple files into a directory too.
In this example, we copy the files info.txt and info2.txt into the data directory.

```console
$ ls 
data  info.txt  info2.txt  R 
$ cp info.txt info2.txt data
$ ls data
info.txt  info2.txt
```

### mv (move)

```mv``` let you move (and rename) a file or directory

To move file info2.txt into data directory:

```console
$ ls 
data  info.txt  info2.txt  R 
$ mv info2.txt data
$ ls
data  info.txt  R 
```

To rename file info.txt to info3:

```console
$ ls 
data  info.txt  R 
$ mv info.txt info3.txt
$ ls
data  info3.txt  R 
```

To rename a directory:

```console
$ ls 
data  info.txt  R 
$ mv data data2
$ ls
data2  info.txt  R 
```


### rm (remove)

Use ```rm``` to remove (delete) a file or directory

To delete a single file:

```console
$ ls 
data  info.txt  info2.txt  info3.txt  R 
$ rm info3.txt
$ ls
data  info.txt  info2.txt  R 
```

To delete multiple files:

```console
$ ls
data  info.txt  info2.txt  R 
$ rm info.txt info2.txt
$ ls
data  R 
```

To delete a directory you must use ```rmdir``` (to prevent you accidentally deleting an entire directory)

### rmdir (remove directory)

Use ```rmdir``` to remove a directory 

```console
$ ls
data  data2  info.txt  info2.txt  R 
$ rmdir data2
$ ls
data  info.txt  info2.txt  R 
```

### mkdir (make directory)

Use ```mkdir``` to remove a directory

```console
$ ls
data  info.txt  info2.txt  R 
$ mkdir data2
$ ls
data  data2  info.txt  info2.txt  R 
```

### Wildcards

You can use wildcards to define which files to use.

* ```*``` is used for "any string"
* ```?``` is used for "any single character"
* ```[...]``` is used for a list of single characters (e.g. [234] accepts the character 2,3, and 4)
* ```{..., ...}``` is used for a list of patterns (e.g. {*.txt, *.csv} accepts all files with extensions txt and csv)
 
## View content

### cat (concatenate)

Use ```cat``` to view the content of a text-file:

```console
$ ls
data  info.txt  info2.txt  R 
$ cat info.txt
This is written in info.txt
```

You can "concatenate" the content of multiple text-files:

```console
$ ls
data  info.txt  info2.txt  R 
$ cat info.txt info2.txt
This is written in info.txt
This is written in info2.txt
```

### head (view top lines)

Use ```head``` to view the top 10 lines of a text-file:

```console
$ ls
data  info.txt  info2.txt  info3.txt R 
$ head info3.txt
Line 1 ...
Line 2 ...
Line 3 ...
Line 4 ...
Line 5 ...
Line 6 ...
Line 7 ...
Line 8 ...
Line 9 ...
Line10 ...
```

To control the number of lines:

```console
$ head -n 3 info3.txt
Line 1 ...
Line 2 ...
Line 3 ...
```

### tail (view bottom lines)

Use ```tail``` to view the bottom 10 lines of a text file. You can control the number of lines too: 

```console
$ tail -n 3 info3.txt
Line 18 ...
Line 19 ...
Line 20 ...
```

### cut (view columns)

Use ```cut``` to view columns of a text file

```console
$ cat data.csv
1, "Robert", 100
2, "Joe", 200
3, "Jack", 150
$ cut -d , f 2-3 data.csv
"Robert", 100
"Joe", 200
"Jack", 150
```

* -d = defining the delimiter (in this case we use ",")
* -f = defining the fields (columns) to view (in this case columns 2-3)

## Search content

### grep (search text)

Use ```grep``` to search for text or patterns in text files

* ```grep Robert data.csv``` will print all lines containing the string Robert in data.csv
* ```grep -c Robert data.csv``` will search for the string Robert in data.csv and returns the count of matchning
* ```grep -c -i Robert data.csv``` will search for the string Robert in data.csv and returns the count of matchning, ignoring upper/lower case
* ```grep -v Robert data.csv``` will print all lines NOT containing the string Robert

### wc (word count)

Use ```wc``` to count newlines, words and bytes

```console
$ cat info.txt
hello world
$ wc info.txt
 1  2 12 info.txt
```

## sort & uniq (Sort & Unique)

### sort

Use ```sort``` to sort lines of a text-file

* ```sort data.csv``` sorts lines in data.csv
* ```sort -r data.csv``` sorts lines in data.csv and reverse order
* ```sort -b data.csv``` sorts lines in data.csv and ignore leading blanks
* ```sort -f data.csv``` sorts lines in data.csv case insensitive
* ```sort -n data.csv``` sorts lines in data.csv compare according to string numerical value
 
### uniq

Use ```uniq``` to remove duplicate lines from a text-file

* ```uniq data.csv``` removes duplicate lines from a text-file
* ```uniq -c data.csv``` removes duplicate lines from a text-file and print count
