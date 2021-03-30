+++
title = "Scripts and functions"
slug = "bash-08-scripts-functions"
weight = 8
+++

## Shell scripts (9 min + 3 min)

We now know a lot of UNIX commands! Wouldn't it be great if we could save certain commands so that we
could run them later or not have to type them out again? As it turns out, this is extremely easy to
do. Saving a list of commands to a file is called a "shell script". These shell scripts can be run
whenever we want, and are a great way to automate our work.

<!-- ```sh -->
<!-- $ cd ~/Desktop/data-shell/molecules -->
<!-- $ nano process.sh -->
<!-- 	#!/bin/bash         # this is called sha-bang; can be omitted for generic (bash/csh/tcsh) commands -->
<!-- 	echo Looking into file octane.pdb -->
<!-- 	head -15 octane.pdb | tail -5       # what does it do? -->
<!-- $ bash process.sh   # the script ran! -->
<!-- ``` -->

<!-- Alternatively, you can change file permissions: -->

<!-- ```sh -->
<!-- $ chmod u+x process.sh -->
<!-- $ ./process.sh -->
<!-- ``` -->

<!-- Let's pass an arbitrary file to it: -->
<!-- ```sh -->
<!-- $ nano process.sh -->
<!-- 	#!/bin/bash -->
<!-- 	echo Looking into file $1       # $1 means the first argument to the script -->
<!--     head -15 $1 | tail -5 -->
<!-- $ ./process cubane.pdb -->
<!-- $ ./process propane.pdb -->
<!-- ``` -->

<!-- * head -15 "$1" | tail -5     # placing in double-quotes lets us pass filenames with spaces -->
<!-- * head $2 $1 | tail $3        # what will this do? -->
<!-- * $# holds the number of command-line arguments -->
<!-- * $@ means all command-lines arguments to the script (words in a string) -->

<!-- > **Quiz 11:** script.sh in molecules Users/nelle/molecules. -->

<!-- > **Exercise:** write a script that takes any number of filenames, e.g., "scriptName.sh cubane.pdb -->
<!-- > propane.pdb", for each file prints the number of lines and its first five lines, and separates the -->
<!-- > output from different files by an empty line. -->

<!-- 08-scripts.mkv -->
{{< yt UGZI6_HDyDc 63 >}}

Here is a an example of processing files with scripts:

<!-- 08-script-molecules.mkv -->
{{< yt rNnrcqkhXQo 63 >}}






<!-- ## If statements -->

<!-- Let's write and run the following script: -->

<!-- ```sh -->
<!-- $ nano check.sh -->
<!--     for f in $@ -->
<!--     do -->
<!--       if [ -e $f ]      # make sure to have spaces around each bracket! -->
<!--       then -->
<!--         echo $f exists -->
<!--       else -->
<!--         echo $f does not exist -->
<!--       fi -->
<!--     done -->
<!-- $ chmod u+x check.sh -->
<!-- $ ./check.sh a b c check.sh -->
<!-- ``` -->

<!-- * Full syntax is: -->

<!-- ```sh -->
<!-- if [ condition1 ] -->
<!-- then -->
<!--   command 1 -->
<!--   command 2 -->
<!--   command 3 -->
<!-- elif [ condition2 ] -->
<!-- then -->
<!--   command 4 -->
<!--   command 5 -->
<!-- else -->
<!--   default command -->
<!-- fi -->
<!-- ``` -->

<!-- Some examples of conditions (**make sure to have spaces around each bracket!**): -->

<!-- * [ $myvar == 'text' ] checks if variable is equal to 'text' -->
<!-- * [ $myvar == number ] checks if variable is equal to number -->
<!-- * [ -e fileOrDirName ] checks if fileOrDirName exists -->
<!-- * [ -d name ] checks if name is a directory -->
<!-- * [ -f name ] checks if name is a file -->
<!-- * [ -s name ] checks if file name has length greater than 0 -->

<!-- > **Exercise:** write a script that complains when it does not receive arguments. -->



## Variables (7 min)

<!-- We already saw variables that were specific to scripts ($1, $@, ...) and to loops ($file). Variables can be used -->
<!-- outside of scripts: -->

<!-- ```sh -->
<!-- $ myvar=3        # no spaces permitted around the equality sign! -->
<!-- $ echo myvar     # will print the string 'myvar' -->
<!-- $ echo $myvar    # will print the value of myvar -->
<!-- ``` -->

<!-- Sometimes you see notation: -->

<!-- ```sh -->
<!-- $ export myvar=3 -->
<!-- ``` -->

<!-- Using 'export' will make sure that all inherited processes of this shell will have access to this -->
<!-- variable. Try defining the variable *newvar* without/with 'export' and then running the script: -->

<!-- ```sh -->
<!-- $ nano process.sh -->
<!-- 	#!/bin/bash -->
<!--     echo $newvar -->
<!-- ``` -->

<!-- You can assign a command's output to a variable to use in another command (this is called *command -->
<!-- substitution*) -- we'll see this later when we play with 'find' command. -->

<!-- ```sh -->
<!-- $ printenv    # print all declared variables -->
<!-- $ env         # same -->
<!-- $ unset myvar   # unset a variable -->
<!-- ``` -->

<!-- Environment variables are those that affect the behaviour of the shell and user interface: -->

<!-- ```sh -->
<!-- $ echo $HOME -->
<!-- $ echo $PATH -->
<!-- $ echo $PWD -->
<!-- $ echo $PS1 -->
<!-- ``` -->

<!-- It is best to define custom environment variables inside your ~/.bashrc file. It is loaded every time you -->
<!-- start a new shell. -->

<!-- 08-variables.mkv -->
{{< yt nNf4Xb56yEs 63 >}}




## Functions (13 min)

Functions are similar to scripts, except that we reference a function by its name. Therefore, once
defined, a function can be run in any directory, whereas running a script in another directory requires
its path.

A convenient place to put all your function definitions is `~/.bashrc` file which is run every time you
start a new shell (local or remote).

<!-- Like in any programming language, in bash a function is a block of code that you can access by its -->
<!-- name. The syntax is: -->

<!-- ```sh -->
<!-- functionName() { -->
<!--   command 1 -->
<!--   command 2 -->
<!--   ... -->
<!-- } -->
<!-- ``` -->

<!-- Inside functions you can access its arguments with variables $1 $2 ... $# $@ -- exactly the same as in -->
<!-- scripts. Functions are very convenient because you can define them inside your ~/.bashrc -->
<!-- file. Alternatively, you can place them into a file and then **source** them whenever needed: -->

<!-- ```sh -->
<!-- $ source allMyFunctions.sh -->
<!-- ``` -->

<!-- Here is our first function: -->

<!-- ```sh -->
<!-- greetings() { -->
<!--   echo hello -->
<!-- } -->
<!-- ``` -->

<!-- Let's write a function 'combine()' that takes all the files we pass to it, copies them into a -->
<!-- randomly-named directory and prints that directory to the screen: -->

<!-- ```sh -->
<!-- combine() { -->
<!--   if [ $# -eq 0 ]; then -->
<!--     echo "No arguments specified. Usage: combine file1 [file2 ...]" -->
<!--     return 1        # return a non-zero error code -->
<!--   fi -->
<!--   dir=$RANDOM$RANDOM -->
<!--   mkdir $dir -->
<!--   cp $@ $dir -->
<!--   echo look in the directory $dir -->
<!-- } -->
<!-- ``` -->

<!-- > **Exercise:** write a function to swap two file names. Add a check that both files exist, before -->
<!-- > renaming them. -->

<!-- > **Exercise:** write a function archive() that takes a directory as an argument, packs it into a gzipped -->
<!-- > tar archive (often called *tarball*) and deletes the original directory. -->

<!-- > **Exercise:** write the reverse function unarchive() that replaces a gzipped tarball with a directory. -->

<!-- 08-functions.mkv -->
{{< yt gSCRWUG9fy4 63 >}}
