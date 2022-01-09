# GEOG 6960 Open Source Geospatial Tools
## Brief Introduction to Linux
#### Monday, January 28 2014

## Objectives

In today's class we will start using GRASS GIS from the command line. As this is running on a Linux server, we will first review some of the basics of working in a Unix system. This document is adapted from the introduction to linux from LSU HPC. 

## Command-Line Interface

Like the family of UNIX *-like operating systems before it, the primary interface to Linux is the command-line. The command-line is still the most powerful and direct way to interact with the system. Shells are how command-line interfaces are implemented in Linux. Each shell has varying capabilities and features and the user should choose the shell that best suits their needs. The shell is simply an application running on top of the kernel and provides a powerful interface to the system.

### The *nix Shell

The shell is your workspace in the terminal. It is a command language interpreter that executes commands read from the standard input device or from a file.


| Shell Name | Developed by | Where | Remark |
| ------------ | ------------- | ------------ | --------- |
| BSH (Bourne-Again SHell) | Brian Fox and Chet Ramey  | Free Software Foundation | Most common shell in Linux |
| CSH (C SHell) | Bill Joy  | University of California (For BSD) | The C shells syntax and usage are very similar to the C programming language |
| KSH (Korn SHell) | David Korn  | AT & T Bell Labs |  |
| TCHS | See the man page  |  | Enhanced version of CSH |

To find available shells in your system type:

	cat /etc/shells

`cat` types out the contents of a file as you saw above. The file "shells" in the "/ etc" directory holds all available shells in the system.

To find your current shell type:

	echo $SHELL

The command `echo` echos or types what follows it. The `$` sign says echo the cont ents of the following system variable. The `SHELL` is a system variable set up in your init file or by using the `export` command.


### Environment Variables

####What are they?

The shell's environment is that umbrella of persistent knowledge under which the shell operates. This information is stored as "environmental variables", which are global variables that may be used at any point by the shell -- either internally or when explicitly required by the user. Other variables can be customized by the user using a specific set of files contained in their HOME directory. 

#### Why should I know about them?
Being able to know which environment variables affect which aspect of your environment means that you are able to customize your environment. In many shell scripts and using many applications or programming languages you will need to know the values of these variables.
Your global environment consists of environment varibles such as:

`PATH` the variable that allows us to locate a command. Which gives all of the directories that the system should search through when looking for a specific command. To see what is in your path:

	echo $PATH

`PWD` which holds the path of the working directory:

	echo $PWD

`HOME` which holds the user's home directory:

	echo $HOME

`USER` holds the user name of the current account:

	echo $USER

To see the overall value of YOUR environment:

	env | less


### Filesystem Information

UNIX uses a true hierarchical filesystem, which is very different from the Windows structure. The UNIX filesystem starts at a single point: / (pronounced "root" [not to be confused with the root user or /root, the root user's home directory]).
Components

The UNIX filesystem is comprised of several parts:

- file: Files contain data, either for users or the system. The data can be text or binary.
- directory: A directory is a collection of files, like a folder in Windows.
- links: Links are pointers to existing files or directories, similar to shorcuts in Windows.
- special file: Special files include:
	- sockets
	- pipes
	- character
	- block
	- These special files are used by the kernel and running applications to control the flow of data in the system.

#### Everything is a file

One of the most difficult thing to grasp about the UNIX filesystem is that everything in UNIX is treated as a file. This includes directories, special files, partitions, disk drives, mice, serial ports, printers, displays, network interfaces, etc. Everything!
Open the Terminal window and navigate to the /dev directory by typing:

	cd /dev
	
Then list the files in this directory:

	ls
	
Note that the list includes USB ports, CD/DVD-drives, etc. 

#### Mounts (disk, NFS)

The UNIX filesystem is analogous to a tree. The root, /, is the root of the hypothetical tree and directories are the branches. The UNIX filesystem can have other filesystems attached onto them, and may be comprised of many different filesystems.
The `mount` command is used to attach other file systems or to show existing attachments.

#### Common UNIX Directory Structure

The UNIX filesystem is traditionally divided into a number of common directories. The series of directories, seperated by a slash ("/") and often ending with a file, is called a path. Each directory path has a specific function. Below is a table listing some of the common directories and their normal use:

| Path | Windows equivalent | Description | 
| ------------ | ------------- | ------------ | 
| / | C:  | The start or 'root' of the filesystem | 
| /home | My Documents or Profiles  | User's private files | 
| /usr or /usr/local | Program Files  | Installed software | 
| /dev | Windows or Windows\System  | Device drivers | 
| /etc | The Registry or .ini files | Application and operating system configuration information | 
| /tmp |Windows\Temp  | Temporary system files | 
| /bin or /sbin | Windows  | System executable files | 


In the Terminal window, type 

	cd / 

and press enter/return to "change directory" to the "root" directory.

This is the directory that all other directories spring from. Which, as in a tree is why it is called "root". In the Terminal window, type 

	pwd
	
(don't forget to press enter/return) to "print the working directory".

Now type 

	cd 

to change back to your account's home directory, the  type 
	
	pwd
	
to "print the working directory".

Now go to the /home directory and list all the current users accounds (directories)

	cd /home
	ls

Now return to your home directory and list the files there:

	cd
	ls
	
Note that adding the parameter `-al` provides more information about the files

	ls -al
	
	
### Command-line Primer

The following are some of the more frequently used filesystem commands:

| Command | Description | DOS/Windows Equivalent |
| --------| ----------- | ---------------------- |
| awk | File processing and report generating	| N/A |
| cat | Show contents of a file	 | type or double-clicking a file |
| cd | Change directory	 | cd or double-clicking a folder |
| cp | Copy a file |	copy or dragging a file |
| file	| Determine file type | file extension or right-click properties |
| find | Find a file | Windows Explorer Find |
| grep | Find lines in a file | N/A |
| gzip | File compresser | WinZip/7Zip |
| less | Display a file one page at a time (extended version of more) | more
| ln | Link a file to another file | Create Shortcut |
| ls | Display files in a directory | dir or Windows Explorer
| mkdir | Create a directory | mkdir or creating a folder |
| more | Display a file one page at a time | more |
| mv | Move or rename a file | rename or dragging a file
| rm | Remove a file | delete or deleting a file |
| rmdir | Remove a (empty) directory | rmdir or deleting a folder |
| sed | Stream editor | N/A |
| tar | Archive creator | N/A |
| unzip | File compresser | WinZip/7Zip |
| vim | Edit a file | edit or notepad |
| wc | Count words, lines and characters in a file | N/A|

### Exercises

For the exercises, you will need the file *nc_spm_latest.tar.gz* from Canvas. Download this file, and copy it to your 'grassdata' directory on the server using WinSCP. 

Now log in to the server using XMing and putty. Once there, change to your GRASS data directory, and list the files that are to check that you have copied the file to the right place:

	cd /home/****/grassdata
	ls -l *.tar.gz
	
The file is a gzipped archive file (these will have the extension *.tgz or *.tar.gz). To open these and extract the files, we need two programs: **gunzip** and **tar**. We start by decompressing the file using **gunzip**

	gunzip nc_spm_latest.tar.gz
	ls -l *.tar

You should see that the .gz extension has been removed, and the size has increased. Now we can list the contents of the archive file:

	tar tvf nc_spm_latest.tar
	
The parameter `tvf` tells tar to simply list the contents rather than extracting. Remember that the terminal allows tab completion. So rather than typing the entire file name, try typing 'nc_' and pressing 'TAB', and the file name should complete. Now we extract the contents, simply by changing the `t` to an `x`:

	tar xvf nc_spm_latest.tar
	ls

[You can combine these two steps into one: `tar zxvf` both decompresses the archive and extracts the contents.] Change directory to the new directory and list the contents:

	cd nc_spm_08
	ls -al 

You should see a set of directories, and some files. The first column gives the file permissions (more on this later). If the first letter is a 'd' then this is a directory. Alternatively, type `ls -alG` and the directories will be shown in a different color. 

Now look at the contents of a file:

	cat VERSION.txt
	
In the Terminal window type

	cp VERSION.txt myfile1

to copy the version file you just looked at, making a second identical file with a new name, "myfile1".

In the Terminal window type

	file myfile1 
to determine the file type.

To create a new directory called "mydir" type:
	
	mkdir mydir

To copy the readme file into mydir keeping the name "readme" type:

	cp VERSION.txt mydir/.

To copy the readme file into mydir with another name "myreadme" type:

	cp VERSION.txt mydir/myVERSION.txt

To list all the files in the new directory "mydir" type:

	ls -l mydir

To copy the directory "c.linux" to the directory "mydir" with the same name type:

	cp -r sqlite mydir/.

To find the number of newlines, words and bytes in a file type:

	wc VERSION.txt

To rename a file type:

	mv VERSION.txt myVERSION.txt

Copy again so you can remove:

	cp myVERSION.txt VERSION.txt

To remove a file type:

	rm myVERSION.txt


### Users and Groups

In Linux a user is identified by their username. Linux usernames are similar to Windows logon IDs. Linux maintains a list of users, called a name space, either locally on each individual machine or across the network via NIS for a group of machines.

User == uid

Each user on a Linux machine has a unique username that corresponds to a unique uid. The uid is a numeric value used to determine if the user is authorized to perform a particular task. It is important to note that the Linux operating system is concerned only with the numeric value of the uid and not the text that describes the user's name.

Group == gid

Groups are also associated with unique numbers called gids. Users may belong to more than one group, although they can be associated with only one group at a time. Groups may have zero, one, or more members. Like uids, the Linux operating system is concerned only with the numeric value of the gid and not the textual name of the group.

#### Authentication

Each time a user tries to login, Linux attempts to authenticate that user against a name space. The login process prompts for a username and, usually, a password. Linux then encrypts the entered password and checks to see if the encrypted text matches the stored version of the user's encrypted password. If there is a match, the user is authenticated; if not, the user is denied access.

#### Permissions

Since Linux treats everything as a file, learning about file permisions is very important. Linux allows access to a file based upon affiliation as defined by user, group, and other. The possible permissions for each affiliation are read (r), write (w), and execute (x). Linux actually uses one bit to indicate these three permissions for each of the three affiliations.

In the Terminal window, type 

	ls -l /etc/passwd

Your output should look similar to this:
> -rw-r--r--    1 root     root         1755 Mar 10 13:48 /etc/passwd

The first dash is a flag specifying the type of file. The next three characters are the permissions for the user who owns the file. The next three characters are the permissions for the group associated with the file. The final three characters are the permissions for any user who is not the owner of the file nor belongs to the group associated with the file.

Each of the permissions has a different meaning depending on whether it is set for a file or a directory:

| Type | r | w | x |
| ---- | - | - | - |
| File | Can read the file | Can change the contents or delete the file | Can execute the file |
| Directory | Can see a listing of files in the directory | Can create new files in the directory or delete files from the directory | Can change into that directory |

In the case of the /etc/passwd file, only the account 'root' (the superuser) can write to the file, but everyone can read it. 


### Beginning Shell Scripting

We will now try some examples of shell scripting using the BASH shell. This is the easiest way to automate tasks in Unix, including analyses in GRASS. You will need a text editor to write the scripts, and there are several that can be used, including:

Here we will use vim, a standard text editor that can be used through the terminal. To start this with a new script, type:

    vim myscript.sh

A window will open that looks like this:

More detail on the vim editor is given below, but for now, press 'i' to enter text insertion mode, then type the following lines

>\#!/bin/bash

>clear 

>echo "Hello World - this is my first shell script"

Now hit the `ESC` button to leave text insertion mode, and type `:wq` to save your input and quit the editor. After writing your scripts you need to change the permissions, so the execute permission is on for the user, the the script can be run from the command line by prefacing it with `./`:

    chmod u+x myscript
    ./myscript.sh

Lets create another script to print user information, who is currently logged in , current date & time:

    vim ginfo.sh

Enter the following text:
>\#!/bin/bash

>clear

>echo "Hello $USER"

>echo "Today is \c ";date

>echo "Number of user login : \c" ; who | wc -l

>echo "Calendar"

>cal

>exit 0

Now, exit the file as before (`ESC` then `:wq`), set the permissions, then execute the script.

### Viewing Files

One of the things that are very important is to see some of the information in a given file. Make sure you are in the 'nc_spm_08' directory, and we will look at the file HISTORY.txt. Commands to do this include:

`cat` - shows you the contents of an entire file (you will see only the last screen full of lines). 

    cat HISTORY.txt

`less` - shows you the contents of an entire file one screen at a time: 

    less HISTORY.txt

 - to go to the next screen hit the space bar 
 - to see only the next line hit the Return key 
 - to quit more hit the "q" key

`head` - shows you the first 10 lines of a file

    head HISTORY.txt

to see fewer or more lines us the -n option

    head -3 HISTORY.txt

`tail` - shows you the last 10 lines of a file

    tail HISTORY.txt
    tail -3 HISTORY.txt

### Redirection and I/O
Most command line programs will take some form of input, and give some form of output. By default, this is either taken from STDIN and written to STDOUT (i.e. the terminal). Redirection allows you to use files instead for this, using the `>` and `<` symbols. For example, the following takes the output of the `ls` function and writes it to a file

    ls /etc > filelist.txt
    head filelist.txt
    
The next example uses the `cat` command, and takes input from the file *VERSION.txt* in the 'nc_spm_08' directory]

    cat < VERSION.txt

The other part of redirection uses pipes to pass output from one program to a second. Using pipes is extremely useful in Linux, as it allows you to combine several simple command line programs to make a fairly complex set of file and data manipulation. A pipe between two programs is given by the `|` symbol. For example, this lists the files in the directory, then passes this list through the `sort` function with a `-r` parameter to do a reverse sort:

    ls | sort -r
    
Here the pipe has the line count command (`wc`) read its input from the `ls` command's output. The result is the number of files in the directory.

    ls | wc -l
    
And here we pipe the output of `ls` through `grep` to select only the lines with the character string 'li' in them

    ls | grep li

### Learning vi/vim

Vi and vim are text editors (vim is an 'improved' version of vi). Vi comes on every UNIX-like system by default, and vim is usually available. While there are many other text editors, and different people believe different ones are the best, we will look at vi/vim here as it can always be found on a UNIX-like OS, unless the system administrator has removed it (Not likely). We will concentrate on vim as it is a little easier to use, but the basic commands can be used in vi, if this is all that is available.

Vi/vim has two modes:

- command mode - allows you to use the normal keys to give movement and text editing commands, copying and pasting, etc
- text mode - allows you to use the normal keys to enter text into your file

To create a file, choose a name that doesn't exist in the directory, e.g. `vim newfile`. This creates the new file, opens it and puts you in command mode. Lets create a new file, a list of files for the North Carolina dataset. 

    ls > filelist.txt
    vim filelist.txt

The file opens in command mode. If the file doesn't exist then you will see a screen with tildes "~". If the file does exist you will see the first page of text in the file. 

Basic movement commands. 
You must be in command mode to move around to get into command mode press the escape key . Once you are in command mode you can use the arrow keys and page-up and page-down to move around. Other useful commands for movement:

- H - moves you to the first character of the "highest" line on the screen
- M - moves you to the first character at the "middle" of the screen
- L - moves you to the first character at the "bottom" of the screen
- $ - moves you to the end of the current line
- ^ - moves you to the beginning of the current line
- Control key plus "f" moves you one page toward the beginning of the file
- Control key plus "b" move you one page toward the end of the file
- the colon key, ':', followed by a line number to go to that line

In order to add, delete or change text, we need to change to text mode. In order to enter text mode, you need to use one of the following commands:

 - i - insert new text to the left of the character the cursor is on 
 - I - insert new text to the left of the first non-blank character on the line 
 - a - insert new text to the right of the character the cursor is on 
 - A - insert new text to the right of the last character on the line
 - o - inserts a new line below the line the cursor is on 
 - O - inserts a new line above the line the cursor is on

Now that we know the basic commands, we can make some changes to this file:

- Go to the start of the first line
- hit the 'O' key to insert a line above the existing text
- Enter some text here to describe the file.
- hit the escape key 
- Type :wq

Typing ":wq" saves and closes the file. The ":" tells vi that a command is coming up next, the "w" tells vi to write the file to disk (save the file)
and the "q" tells vi to quit. If you don't type the "q" vi saves the file and lets you continue. If you have made changes that you don't want to keep, then typeing ":q!" will quit without saving. 

#### Copying and pasting

The three main commands for copying and pasting are:

- d - cut text
- y - copy text
- p - paste text

Reopen the file you have been using in vim, and try the following

- Go to the first character of any line, and while in command mode, press "d". Nothing will happen until you press the direction key. Up or down will cut the line above or below the cursor, and left or right will cut the first character in that direction. Press right to cut the character under the cursor
- Now move to the end of the line and press "p" to paste the text to the right of where the cursor is. Pressing "shift-p" will paste to the left
- Now repeat this, but instead of pressing "d" in the first step, press "y" to copy
- If you use these commands after having enter a number, then you will cut or copy that number of characters. Go to the start of any line and press "5y", then go to the end and press "p". The first five characters will be copied and pasted
- To move an entire line, the easiest way is to put the cursor on the line, and press "dd". The line will be cut, then move to where you want the line and press "p" to paste. As before, entering a number before the "dd" will cut multiple lines. 

#### Find and replace
Vi/vim  has a quite sophisticated (and pretty complex) find and replace method. To find anything in the file, simply use "/" while in command mode. For example "/a" will find all the 'a's in the file. Press "n" to move to the next one. 

Find and replace is done using the ":s" command. This takes two arguments, the character string to search for, and the character string to put in its place. Try the following

- Go to the line that reads 'landsat'. Make sure you are in the command mode (press `ESC`) and type `:s/a/u`. Press return and the first 'a' will be chanegd to a 'u'. 
- Go to the line that reads 'PERMANENT'. Type `:s/E/D/g`. Appending the "g" onto the end now changes all the first character to the second (NB you are not restricted to single characters here). 
- To replace every instance of a character, use a '%' between the ':' and the 's'. For example: `:%s/txt/csv/g` will change every 'txt' to a 'csv'
- We can also target the replacements to particular set of lines. Type `:1,3s/csv/txt/g` to change the string 'csv' to 'txt' on the first three lines only

There is much more that can be done, including the use of regular expressions. A good site for examples and tutorials is the [vim site][1].

### Getting Help from the System

- Man pages give the syntax of a command in UNIX like operating systems. These are manuals which give you information on the commands: syntax, options, etc. To access these pages for a command type `man command-name`. 
Type:

    man cp

This gives the information on the cp (copy) command. Press 'q' to quit. 

Other options
The command `whatis` gives a one-line description of the command but doesn't include the options.

    whatis cp

apropos keyword
The command 'apropos' gives a list of commands with this keyword in their description

    apropos copy

Open source software is generally tightly linked to the development of the internet, and the greatest source of help, tutorials and examples can be found there. Particularly recommended are

- [Stack exchange][2]
- [The Linux Documentation Project][3]
- [The O'Reilly series of books][4]

-------------------
Simon Brewer 01/21/14

  [1]: http://www.vim.org/
  [2]: http://stackexchange.com
  [3]: http://www.tldp.org/
  [4]: http://www.oreilly.com/
