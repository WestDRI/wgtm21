+++
title = "Scheduling"
slug = "hpc-04-scheduling"
weight = 4
+++

#### Slurm intro (8 min)

<!-- 04a-slurm.mp4 -->
{{< yt Qd39UkdajwQ 63 >}}

#### Job billing with core equivalents (2 min)

<!-- 04b-equivalents.mp4 -->
{{< yt GjI8Fmzo20A 63 >}}

#### Submitting serial jobs (12 min)

<!-- 04c-serial.mp4 -->
{{< yt sv5lUnoBV30 63 >}}

#### Submitting shared-memory jobs (9 min)

<!-- 04d-openmp.mp4 -->
{{< yt rIxTP8d8PaM 63 >}}

#### Submitting MPI jobs (8 min)

<!-- 04e-mpi.mp4 -->
{{< yt 7RWpRtCCPz8 63 >}}

#### Slurm jobs and memory (8 min)

<!-- 04f-memory.mp4 -->
{{< yt zaYUIjsuKoU 63 >}}

#### Hybrid and GPU jobs (5 min)

<!-- 04g-hybrid-gpu.mp4 -->
{{< yt -1g2WM9kG88 63 >}}

#### Interactive jobs (8 min)

An interactive job will give you a bash shell on one the nodes that was allocated to your job. There you
can start a test run, debug your code, start a VNC/ParaView/VisIt/etc server and connect to it from a
client on your computer, etc. Note that interactive jobs typically have a short maximum runtime, usually
3 hours.

One of the main takeaways from this course is to learn how to transition between `sbatch` and `salloc`
commands. You may debug your workflow with `salloc`, transition to production jobs with `sbatch`, and
then find that you need to use `salloc` again to debug problems and to analyze your large datasets.

<!-- 04h-interactive.mp4 -->
{{< yt Ye7IrSxaN2k 63 >}}

#### Getting information and other Slurm commands (6 min)

<!-- 04i-info.mp4 -->
{{< yt I_U5u9F-_no 63 >}}
