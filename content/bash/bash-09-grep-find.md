+++
title = "Grep and find"
slug = "bash-09-grep-find"
weight = 9
+++

## Searching inside files with `grep` (4 min)

<!-- ```sh -->
<!-- $ cd ~/Desktop/data-shell/writing -->
<!-- $ more haiku.txt -->
<!-- ``` -->

<!-- First let's search for text in files: -->
<!-- ```sh -->
<!-- $ grep not haiku.txt     # let's find all lines that contain the word 'not' -->
<!-- $ grep day haiku.txt     # now search for word 'day' -->
<!-- $ grep -w day haiku.txt        # search for a separate word 'day' (not 'today', etc.) -->
<!-- $ grep -w today haiku.txt   # search for 'today' -->
<!-- $ grep -w Today haiku.txt   # search for 'Today' -->
<!-- $ grep -i -w today haiku.txt       # both upper and lower case 'today' -->
<!-- $ grep -n -i -w today haiku.txt    # -n prints out numbers the matching lines -->
<!-- $ grep -n -i -w -v the haiku.txt   # -v searches for lines that do not contain 'the' -->
<!-- $ man grep -->
<!-- ``` -->

<!-- More than two arguments to grep: -->
<!-- ```sh -->
<!-- $ grep pattern file1 file2 file3   # all argument after the first one are assumed to be filenames -->
<!-- $ grep pattern *.txt   # the last argument will expand to the list of *.txt files -->
<!-- ``` -->

<!-- > **Quiz 12:** grep command. -->

<!-- 09-grep.mkv -->
{{< yt mbZ8nB-V4zQ 63 >}}

## Finding files with `find` (5 min)

<!-- Now on to finding files: -->
<!-- ```sh -->
<!-- cd ~/Desktop/data-shell/writing -->
<!-- $ find . -type d     # search for directories inside current directory -->
<!-- $ find . -type f     # search for files inside current directory -->
<!-- $ find . -maxdepth 1 -type f     # depth 1 is the current directory -->
<!-- $ find . -mindepth 2 -type f     # current directory and one level down -->
<!-- $ find . -name haiku.txt      # finds specific file -->
<!-- $ ls data       # shows one.txt two.txt -->
<!-- $ find . -name *.txt      # still finds one file -- why? answer: expands *.txt to haiku.txt -->
<!-- $ find . -name '*.txt'    # finds all three files -- good! -->
<!-- ``` -->

<!-- Let's wrap the last command into $() (called *command substitution*), as if it was a variable: -->

<!-- ```sh -->
<!-- $ echo $(find . -name '*.txt')   # will print ./data/one.txt ./data/two.txt ./haiku.txt -->
<!-- $ ls -l $(find . -name '*.txt')   # will expand to ls -l ./data/one.txt ./data/two.txt ./haiku.txt -->
<!-- $ wc -l $(find . -name '*.txt')   # will expand to wc -l ./data/one.txt ./data/two.txt ./haiku.txt -->
<!-- $ grep elegant $(find . -name '*.txt')   # will look for 'elegant' inside all *.txt files -->
<!-- ``` -->

<!-- > **Quiz 13:** combining grep and find. -->

<!-- > **Exercise:** write a function 'countFiles()' that counts the number of files in each directory that -->
<!-- > you pass to it and prints it after the directory name. -->

<!-- 09-find.mkv -->
{{< yt AnwsnESj82Q 63 >}}

## Combining `find` and `grep` (4 min)
<!-- ## Running a command on the results of `find` -->

<!-- You always can do something like this: -->

<!-- ```sh -->
<!-- $ for f in $(find . -name "*.txt") -->
<!-- > do -->
<!-- >   command on $f -->
<!-- > done -->
<!-- ``` -->

<!-- However, you can actually make it a one-liner: -->

<!-- ```sh -->
<!-- find . -name "*.txt" -exec command {} \;       # important to have spaces -->
<!-- ``` -->

<!-- -- this will run the command on each item in the output of find. -->

<!-- 09-findgrep.mkv -->
{{< yt aFrMKkjMIHY 63 >}}
