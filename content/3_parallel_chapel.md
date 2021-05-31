+++
title = "Parallel programming in Chapel"
slug = "parallel_chapel"
+++

{{<cor>}}Tuesday, June 1{{</cor>}}\
{{<cgr>}}9 am–5 pm Pacific Time{{</cgr>}}

This course will start at 9am Pacific Time and will run until 5pm Pacific Time. Its format will be a combination of
several interactive Zoom sessions and the reading materials in-between the Zoom sessions. Course materials will be added
here shortly before the start of the course.

---

This course is a general introduction to the main principles of parallel programming, using Chapel programming language
to illustrate the basic concepts and ideas. Chapel is a relatively new language for both shared- and distributed-memory
programming, with easy-to-use, high-level abstractions for both task and data parallelism that make it ideal for
learning parallel programming for a novice HPC user. Chapel is incredibly intuitive, striving to merge the ease-of-use
of Python and the performance of traditional compiled languages such as C and Fortran. Parallel constructs that
typically take tens of lines of MPI code can be expressed in only a few lines of Chapel code. Chapel is open source and
can run on any Unix-like operating system, with hardware support from laptops to large HPC systems.

**Instructor**: Alex Razoumov (WestGrid)

**Prerequisites:** working knowledge of the Linux Bash shell and familiarity with Compute Canada's HPC cluster
  environment, in particular, with the Slurm scheduler (covered in [our HPC course](../basics_hpc)).

**Software**: All attendees will need a remote secure shell (SSH) client installed on their computer in order to
participate in the course exercises. On Windows we recommend
[the free Home Edition of MobaXterm](https://mobaxterm.mobatek.net/download.html). On Mac and Linux computers SSH is
usually pre-installed (try typing `ssh` in a terminal to make sure it is there). No need to install Chapel on your
computer.

{{< figure src="/img/solveMulti.gif" >}}

{{<cor>}}Zoom{{</cor>}} {{<s>}} {{<cgr>}}9:00am-10:00am Pacific{{</cgr>}} \
{{<linktitle url="../chapel1" text="Morning opening session">}}

<!-- {{<cbr>}}On your own{{</cbr>}} \ -->
<!-- {{<nolinktitle>}}Basic language features{{</nolinktitle>}} \ -->
<!-- {{<nolinktitle>}}Task parallelism{{</nolinktitle>}} -->

{{<cbr>}}On your own{{</cbr>}} \
{{<linktitle url="../chapel/chapel-01-base" text="Basic language features">}} \
{{<linktitle url="../chapel/chapel-02-task-parallelism" text="Task parallelism">}} &nbsp; (try to get here as far as you can)

{{<cor>}}Zoom{{</cor>}} {{<s>}} {{<cgr>}}12:00pm-2:00pm Pacific{{</cgr>}} \
{{<linktitle url="../chapel2" text="Mid-day session">}}

<!-- {{<cbr>}}On your own{{</cbr>}} \ -->
<!-- {{<nolinktitle>}}Data parallelism{{</nolinktitle>}} -->

{{<cbr>}}On your own{{</cbr>}} \
{{<linktitle url="../chapel/chapel-03-domain-parallelism" text="Data parallelism">}}

{{<cor>}}Zoom{{</cor>}} {{<s>}} {{<cgr>}}3:30pm-5:00pm Pacific{{</cgr>}} \
{{<nolinktitle>}}Cover challenges, do some exercises, and wrap up the course.{{</nolinktitle>}}
