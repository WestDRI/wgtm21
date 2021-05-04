+++
title = "HPC morning session"
slug = "hpc1"
+++

<!-- In this session, I will introduce myself, will review the program for today and distribute usernames and -->
<!-- passwords to log in to the training cluster. I will also share the afternoon exercises. -->

1. Instructor / helpers / course introduction.
1. Distribute the usernames, share the password.
1. Let's try to log in to the training cluster.
1. Download [today's materials](http://bit.ly/introhpc) (ZIP file with slides and codes inside).
1. Review the program for this morning: you have **1h49m** of videos to watch.

By mid-day you should be familiar with:

- Compute Canada cluster hardware
  - cluster intended purpose and specs
  - filesystems
  - allocation policies
- how to ssh into a cluster
- how to edit remote files
- how to transfer files between your computer and an HPC cluster
- using software modules
- compiling serial, shared-memory and distributed-memory codes
- basic parallel programming ideas in OpenMP, MPI, Chapel, Python Dask
- writing and using makefiles
- installing Python or R packages/libraries in your own directories on the cluster

Some of the hands-on exercises we will do in the mid-day Zoom session:

- Edit a remote file in nano or vi or emacs.
- Try to understand what the default GNU compiler module does: run `module show` on it, print `PATH`
  variable, locate the GNU C compiler.
- Check if your favourite research software is installed on the cluster.
- Write a makefile from scratch.
- Try left+right or upper+lower split panes in tmux on the cluster.
