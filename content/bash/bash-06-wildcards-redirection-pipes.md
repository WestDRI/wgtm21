+++
title = "Tapping the power of Unix"
slug = "bash-06-wildcards-redirection-pipes"
weight = 6
+++

## Wildcards, redirection to files, and pipes (8 min)

<!-- * open http://bit.ly/bashfile in your browser, it'll download the file bfiles.zip -->
<!-- * unpack bfiles.zip to your Desktop; you should see ~/Desktop/data-shell -->

<!-- ```sh -->
<!-- $ cd <parentDirectoryOf`data-shell`> -->
<!-- $ ls data-shell -->
<!-- $ cd data-shell/molecules -->
<!-- $ ls -->
<!-- $ ls p*   # this is a Unix wildcard; bash will expand it to 'ls pentane.pdb propane.pdb' -->
<!-- $ ls *.pdb   # another wildcard, will expand to "ls cubane.pdb ethane.pdb ...' -->
<!-- $ wc -l *.pdb   # list number of lines in each file -->
<!-- $ wc -l *.pdb > lengths.txt   # redirect the output of the last command into a file -->
<!-- $ more lengths.txt -->
<!-- $ sort -n lengths.txt   # sort numerically, i.e. 2 will go before 10, and 6 before 22 -->
<!-- $ sort -n lengths.txt > sorted.txt -->
<!-- $ head -1 sorted.txt   # show the length of the shortest (number of lines) file -->
<!-- $ wc -l *.pdb | sort -n | head -1   # three commands can be shortened to one - this is called Unix pipe -->
<!-- ``` -->

<!-- Standard input of a process. Standard output of a process. Pipes connect the two. -->

Covered topics: working with multiple files using wildmasks, standard output redirection to a file,
constructing complex commands with Unix pipes.
<!-- 06-pipes.mkv -->
{{< yt lueQ-KxLFYI 63 >}}

<!-- > **Exercise:** build a single command to show the lenth of the longest (number of lines) file -->

<!-- > **Exercise:** Try to explain the difference between these two commands: -->
<!-- > ```sh -->
<!-- > echo hello > test.txt -->
<!-- > echo hello >> test.txt -->
<!-- > ~~~ -->

<!-- > **Quiz 7:** What code would you use to move all the .dat files into the analyzed sub-directory? -->

<!-- > **Quiz 8:** Command to list the three files with the least number of lines. -->

## Aliases

Aliases are one-line shortcuts/abbreviation to avoid typing a longer command, e.g.

```sh
$ alias ls='ls -aFh'
$ alias pwd='pwd -P'
$ alias hi='history'
$ alias top='top -o cpu -s 10 -stats "pid,command,cpu,mem,threads,state,user"'
$ alias cedar='ssh -Y cedar.computecanada.ca'
$ alias weather='curl wttr.in/vancouver'
$ alias cal='gcal --starting-day=1'  # starts on Monday
```

Now, instead of typing `ssh -Y cedar.computecanada.ca`, you can simply type `cedar`. To see all your
defined aliases, type `alias`. To remove, e.g. the alias `cedar`, type `unalias cedar`.

You may want to put all your alias definitions into the file `~/.bashrc` which is run every time you
start a new local or remote shell.
