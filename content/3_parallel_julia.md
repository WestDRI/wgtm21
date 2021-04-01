+++
title = "Parallel computing in Julia"
slug = "parallel_julia"
+++

{{<cor>}}Tuesday, June 8{{</cor>}}\
{{<cgr>}}9 am–5 pm Pacific Time{{</cgr>}}

This course will start at 9am Pacific Time and will run until 5pm Pacific Time. Its format will be a combination of
several interactive Zoom sessions and the reading materials in-between the Zoom sessions. Course materials will be added
here shortly before the start of the course.

---

Julia is a high-level programming language well suited for scientific computing and data science. Just-in-time
compilation, among other things, makes Julia really fast yet interactive. For heavy computations, Julia supports
multi-threaded and multi-process parallelism, both natively and via a number of external packages. It also supports
memory arrays distributed across multiple processes either on the same or different nodes. In this hands-on workshop, we
will start with a quick review of Julia's multi-threading features but will focus primarily on Distributed standard
library and its large array of tools. We will demo parallelization using three problems: a slowly converging series, a
Julia set, and an N-body solver. We will run examples on a multi-core laptop and an HPC cluster.

**Instructor**: Alex Razoumov (WestGrid)

**Prerequisites:** working knowledge of serial Julia (covered in [our Julia course](../programming_julia)) and
familiarity with Compute Canada's HPC cluster environment, in particular, with the Slurm scheduler (covered in
[our HPC course](../basics_hpc)).


**Software**: All attendees will need a remote secure shell (SSH) client installed on their computer in order to
participate in the course exercises. On Windows we recommend
[the free Home Edition of MobaXterm](https://mobaxterm.mobatek.net/download.html). On Mac and Linux computers SSH is
usually pre-installed (try typing `ssh` in a terminal to make sure it is there).
