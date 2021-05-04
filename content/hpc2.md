+++
title = "HPC mid-day session"
slug = "hpc2"
+++

<!-- In this session, I will cover the program for today, answer any questions -->
<!-- and share the afternoon exercises. -->

### Part 1: morning materials

1. Answer any questions.
1. Go together through the challenges, do some exercises, and debug problems.

### Part 2: afternoon materials

1. Review the program for this afternoon: you have **1h15m** of videos to watch.

By the end of the day you should be familiar with:

- how jobs are scheduled in Slurm
- submitting serial, shared-memory, distributed-memory and hybrid jobs
- submitting array jobs
- running interactive jobs, and switching between interactive and batch jobs for the same task
- how to estimate memory requirements of a completed Slurm job

Some of the hands-on exercises we will do in the afternoon Zoom session:

- Using a serial job, time optimized (-O2) vs. unoptimized C code.
- Using a serial job, time a C code vs. a Python code.
- Submit an array job for different number of terms in the summation of \pi.
- Try scaling an MPI job with 1 -> 2 -> 4 -> 8 cores and measuring the speedup.
- Test a code inside an interactive job.

<!-- - Edit a remote file in nano or vi or emacs. -->
<!-- - Try to understand what the default GNU compiler module does: run `module show` on it, print `PATH` -->
<!--   variable, locate the GNU C compiler. -->
<!-- - Check if your favourite research software is installed on the cluster. -->
<!-- - Write a makefile from scratch. -->
<!-- - Try left+right or upper+lower split panes in tmux on the cluster. -->
