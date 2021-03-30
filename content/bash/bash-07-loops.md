+++
title = "Loops"
slug = "bash-07-loops"
weight = 7
+++

# Bash loops (9 min)

<!-- ```sh -->
<!-- $ cd ~/Desktop/data-shell/creatures -->
<!-- $ ls   # shows basilisk.dat unicorn.dat -- let's pretend there are several hundred files here -->
<!-- ``` -->

<!-- Let's say we want to rename -->
<!-- basilisk.dat -> original-basilisk.dat -->
<!-- unicorn.dat -> original-unicorn.dat -->

<!-- We could try -->

<!-- ```sh -->
<!-- $ mv *.dat original-*.dat   # getting an error -->
<!-- ``` -->

<!-- Remember if more than two arguments to mv, the last argument is the destination directory, but there is -->
<!-- no directory matching original-*.dat, so we are getting an error. The proper solution is to use loops. -->

<!-- ```sh -->
<!-- $ for filename in basilisk.dat unicorn.dat     # filename is the loop variable here -->
<!-- > do -->
<!-- >   ls -l $filename                 # get the value of the variable by placing $ in front of it -->
<!-- > done -->
<!-- ``` -->

<!-- $filename is equivalent to ${filename} -->

<!-- Let's simplify the previous loop: -->
<!-- ```sh -->
<!-- $ for f in *.dat -->
<!-- > do -->
<!-- >   ls -l $f -->
<!-- > done -->
<!-- ``` -->

<!-- Let's include two commands per each loop iteration: -->
<!-- ```sh -->
<!-- $ for f in *.dat -->
<!-- > do -->
<!-- >   echo $f -->
<!-- >   head -3 $f -->
<!-- > done -->
<!-- ``` -->

<!-- Now to renaming basilisk.dat -> original-basilisk.dat, unicorn.dat original-unicorn.dat: -->
<!-- ```sh -->
<!-- $ for f in *.dat -->
<!-- > do -->
<!-- > cp $f original-$f -->
<!-- > done -->
<!-- ``` -->

<!-- > **Quiz 9:** Output of a loop. -->

<!-- > **Quiz 10:** Write a loop. -->

<!-- The general syntax is -->

<!-- ```sh -->
<!-- $ for <variable> in <collection> -->
<!-- > do -->
<!-- >   commands with $variable -->
<!-- > done -->
<!-- ``` -->

<!-- where a collection could be a explicit list of items, a list produced by a wildmask, or a collection of -->
<!-- numbers/letters. For example: -->

<!-- ```sh -->
<!-- $ echo {1..10}   # this is called brace expansion -->
<!-- $ echo {1,2,5}    # very useful for loops or for including into large paths with multiple items, e.g. -->
<!-- $ cd ~/Desktop/data-shell/creatures -->
<!-- $ ls -l ../molecules/{ethane,methane,pentane}.pdb -->
<!-- $ echo {a..z}    # can also use letters -->
<!-- $ echo {a..z}{1..10}   # this will produce 260 items -->
<!-- $ echo {a..z}{a..z}    # this will produce 676 items -->
<!-- $ seq 1 2 10      # step=2, so can use: for i in $(seq 1 2 10) -->
<!-- $ for ((i=1; i<=5; i++)) do echo $i; done   # can use C-style loops -->
<!-- ``` -->

<!-- 07-loops.mkv -->
{{< yt cCunoOIksAE 63 >}}
