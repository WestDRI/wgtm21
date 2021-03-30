+++
title = "Libraries"
slug = "python-10-libraries"
weight = 10
+++

Most of the power of a programming language is in its libraries. This is especially true for Python which is an
interpreted language and is therefore very slow (compared to compiled languages). However, the libraries are often
compiled (can be written in compiled languages such as C/C++) and therefore offer much faster performance than native
Python code.

A library is a collection of functions that can be used by other programs. Python's *standard library* includes many
functions we worked with before (print, int, round, ...) and is included with Python. There are many other additional
modules in the standard library such as math:

```py
print('pi is', pi)
import math
print('pi is', math.pi)
```

You can also import math's items directly:

```py
from math import pi, sin
print('pi is', pi)
sin(pi/6)
cos(pi)
help(math)   # help for libraries works just like help for functions
from math import *
```

You can also create an alias from the library:

```py
import math as m
print m.pi
```

**Quiz 8:** exploring the math library

**Quiz 9:** random numbers

**Quiz 10:** forgot to load the library

**Quiz 11:** degree conversion with math

## Virtual environments and packaging

<!-- Something that comes up often when trying to get people to use python is virtual environments and packaging - it would -->
<!-- be nice if there could be a discussion on this as well. -->

To install a package into the current Python environment from inside a Jupyter notebook, simply do:

```sh
%pip install packageName
```

In Python you can create an isolated environment for each project, into which all of its dependencies will be
installed. This could be useful if your several projects have very different sets of dependencies. On the computer
running your Jupyter notebooks, open the terminal and type:

```sh
pip install virtualenv
virtualenv climate   # create a new virtual environment in your current directory
source climate/bin/activate
which python && which pip
pip install numpy ...
pip install ipykernel   # install ipykernel (IPython kernel for Jupyter) into this environment
python -m ipykernel install --user --name=climate   # add your environment to Jupyter
...
deactivate
```

Quit all your currently running Jupyter notebooks and the Jupyter dashboard. If running on syzygy.ca, logout from your
session and then log back in.

Whether running locally or on syzygy.ca, open the notebook dashboard, and one of the options in `New` below `Python 3`
should be `climate`.

To delete the environment, in the terminal type:

```sh
jupyter kernelspec list                  # `climate` should be one of them
jupyter kernelspec uninstall climate     # remove your environment from Jupyter
/bin/rm -rf climate
```
