+++
title = "Multi-threading - part 1"
slug = "julia-02-threads1"
weight = 2
katex = true
markup = "mmark"
+++

Let's start Julia by typing `julia` in bash:

```julia
using Base.Threads   # otherwise would have to preface all functions/macros with 'Threads.'
nthreads()           # by default, Julia starts with a single thread of execution
```

If instead we start with `julia -t 4` (or prior to v1.5 with `JULIA_NUM_THREADS=4 julia`):

```julia
using Base.Threads
nthreads()           # now we have access to 4 threads
```

When launched from this interface, these four threads will run on two CPU cores on the login node -- more of a
concurrent (than parallel) run, especially considering the number of people logged into Cassiopeia's login node right
now. Soon, when doing benchmarking, we'll switch to running Julia inside Slurm jobs on compute nodes, but for now let's
continue on the login node.

Let's run our first multi-threaded code:

```julia
@threads for i=1:10   # parallel for loop using all threads
    println("iteration $i on thread $(threadid())")     # notice bash-like syntax
end
```

This would split the loop between 4 threads running on two CPU cores: each core would be taking turns running two of
your threads (and likely threads from other users).

Let's now fill an array with values in parallel:

```julia
a = zeros(10)   # 64-bit floating array
@threads for i=1:10
    a[i] = threadid()   # should be no collision: each thread writes to its own part
end
a
```

Here we are filling this array in parallel, and no thread will overwrite another thread's result. In other words, this
code is **thread-safe**.

> **Note:** @threads macro is well-suited for shared-memory data parallelism without any reduction. Curiously, @threads
>   does not have any data reduction built-in, which is a serious omission that will likely be addressed in future
>   versions.

Let's initialize a large floating array:

```julia
nthreads()       # still running 4 threads
n = Int64(1e8)   # integer number
a = zeros(n);
typeof(a)        # how much memory does this array take?
```

and then fill it with values using a single thread, and time this operation:

```julia
@time for i in 1:n
    a[i] = log10(i)
end
```

On Cassiopeia I get 14.38s, 14.18s, 14.98s with one thread.

> **Note:** There is also `@btime` from BenchmarkTools package that many people would suggest you should use
> instead. Here `@time` is perfectly good for our purposes.

Let's now time parallel execution with 4 threads on 2 CPU cores:

```julia
using Base.Threads
@time @threads for i in 1:n
    a[i] = log10(i)
end
```

On Cassiopeia I get 6.57s, 6.19s, 6.10s -- this is ~2X speedup, as expected.

### Let's add reduction: summation $$~~\sum_{i=1}^{10^6}i~~$$ via threads




```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```

```julia
```
