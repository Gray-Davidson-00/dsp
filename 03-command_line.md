# Learn command line

Please follow and complete the free online [Bash Scripting Tutorial](https://ryanstutorials.net/bash-scripting-tutorial/) or [Codecademy's Learn the Command Line](https://www.codecademy.com/learn/learn-the-command-line). These are helpful tutorials. You should be able to go through these in a couple of hours.

**Note:** Bash is not installed on a PC. Rather, PC users must install Cygwin. Once Cygwin has been installed, the command line interface witll _emulate_ bash. You can find all information regarding Cygwin [here](https://www.cygwin.com/).

---

### Q1.  Cheat Sheet of Commands  

Here's a list of items with which you should be familiar:  
* show current working directory path
* creating a directory
* deleting a directory
* creating a file using `touch` command
* deleting a file
* renaming a file
* listing hidden files
* copying a file from one directory to another

Make a cheat sheet for yourself: a list of at least **ten** commands and what they do.  (Use the 8 items above and add a couple of your own.)  

`pwd` * show current working directory path

`mkdir dir_name` * creating a directory

`rm -r dir_name` * deleting a directory

`touch filename.ext` * creating a file using `touch` command

`rm filename` * deleting a file

`cp old_name.ext new_name.ext` * renaming a file

`ls -a` * listing hidden files

`cp filename.ext directory` * copying a file from one directory to another

`cd` * path switches you into the directory you specify (paths are relative to current directory)

`ls` * lists the contents of the current directory

`ls -t` * lists contents ordered by modification date

`ls -l` * lists in long format

---

### Q2.  List Files in Unix   

What do the following commands do:  
`ls`  lists files in a directory

`ls -a`  includes hidden files

`ls -l`  lists in long format

`ls -lh`  appears to have something to do with abbreviations.  numbers of bytes such as 4387 are abbreviated to 4.3k

`ls -lah` lists in long format including hidden files with abbreviations

`ls -t`  lists files ordered by modification date

`ls -Glp`  lists visible files in long format with directory names in blue (-G) followed by a "/" (-p) 

---

### Q3.  More List Files in Unix  

Explore these other [ls options](http://www.techonthenet.com/unix/basic/ls.php) and pick 5 of your favorites:

`ls -R` lists contents and subdirectories

`ls -r` lists contents in reverse order

`ls -d`  displays only directories

`ls -m`  lists contents as a list with comma delimiters

`ls -u`  lists contents by access time, not creation timestamp

---

### Q4.  Xargs   

What does `xargs` do? Give an example of how to use it.

xargs is a command which converts input from stdin to arguments to a command.  This is necessary because, while some commands such as grep can take input in several forms, others such as echo can only take input as arguments, not as stdin.  

...better description from https://shapeshed.com/unix-xargs/

"The xargs command in UNIX is a command line utility for building an execution pipeline from standard input. Whilst tools like grep can accept standard input as a parameter, many other tools cannot. Using xargs allows tools like echo and rm and mkdir to accept standard input as arguments."

And that website goes on: 
"By default xargs reads items from standard input as separated by blanks and executes a command once for each argument. In the following example standard input is piped to xargs and the mkdir command is run for each argument, creating three folders."

So we pass three inputs separated by blanks as stdin to mkdir (which can only take arguments) and by inserting xargs we convert the input and allow mkdir to use it to creat ethree directories.  

Examle from the website:
`echo 'one two three' | xargs mkdir`

`ls`

`one two three`
 

