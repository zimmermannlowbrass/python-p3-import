# Import

## Learning Goals

- Importing modules

***

## Key Vocab

- **Module**: a file containing Python definitions and statements. A module's
functions, classes, and global variables can be accessed by other modules.
- **Package**: a collection of modules that can be accessed as a group using
the package name.
- **`import`**: the Python keyword used to access data from other packages and
modules inside of the current module.
- **PyPI**: the **Py**thon **P**ackage **I**ndex. A repository of Python
packages that can be downloaded and made available to your application.
- **`pip`**: the command line tool used to download packages from PyPI. `pip`
is installed on your computer automatically when you download Python.
- **Virtual Environment**: a collection of modules, packages, and scripts that
can be activated or deactivated at any time.
- **Pipenv**: a virtual environment tool that uses `pip` to manage the modules,
packages, and scripts that you intend to use in your application.

***

## Introduction

As your programs gets longer, you may want to split them into several files
for easier maintenance. You may also want to use a handy function that you’ve
written in several programs without copying its definition into each program,
or functions that others wrote to save you a bit of development time.
All imports start from files (also called **modules**). Using the **import**
keyword, we can access whole modules or the classes, functions, and objects
inside from any other module.

***

## Importing a Module

Lets use the Python `os` module as an example.
We will use the name property to demonstrate the different ways to import.

Open the Python shell and enter the following code:

```console
$ import os
$ os.name
# => 'posix'
```

"posix", or the Portable Operating System Interface, is the name of the module
that code is executed from in the Python shell.

A module may have multiple functions and definitions.
What if we only want to use a few of them? A more concise way of importing is
only importing the things we need. Lets say we want to import only the `name`
property in the `os` module. We can do this by using the from keyword.

```console
$ from os import name
$ name
# => 'posix'
```

Note how we did not need to prepend `os` to the `name`.

The `from` keyword also allows us to import everything from a library using the
`*` operator.

```console
$ from os import *
$ name
# => 'posix'
```

This can be bad practice, because it is less concise and you may run
into namespace issues. (What if we had called another variable `name`?) When
using the `*` operator we don't know exactly what we are taking from the module,
leading to less readable code.

***

## Absolute Imports

An absolute import specifies the module to be imported using the full path
 from the project root directory.

```bash
project
├── package1
│   ├── module1.py
│   └── module2.py
├── package2
│   ├── module3.py
│   ├── module4.py
│   ├── module5.py
│   └── subpackage1
│       └── module6.py
└── test.py
```

Lets use the above file structure to practice. All the code below will be in `test.py`

```py
# project/test.py
#Lets assume there is a function called function1 in all these modules. We can import it using the following code

from package1 import module1

module1.function1()
```

```py
#test.py
# We can explicitly import functions by 

from package1.module1 import function1

function1()
```

How do we import module 6?

```py
#test.py
# We can append the path from root to the module6 to the package.  
from package1.subpackage1.module6 import function1

function1()
```

Pros and cons of absolute imports

Absolute imports remain valid even if the current location of the import
 statement changes. For example, if we move the `test.py` file to a sub
  directory the imports would still be valid.

Why should we not use Absolute Imports?

Lets say we have want to import a module from a long nested
 directory structure. The import statement
would be huge.

```py
from package1.subpackage1.subpackage2.subpackage3.module1 import function1
```

We can avoid this by using relative imports.

***

## Relative Imports

The reason why relative imports exist is because they allow us
to rearrange the structure of large packages without having to edit
  sub-packages. If we rearrange a large package
with absolute imports we will have to change all the paths in every
 file's import statements to match the new location.

Lets use the following directory structure

```bash
my_package/
    __init__.py
    subpackage1/
        __init__.py
        module1.py
        module2.py
    subpackage2/
        __init__.py
        module3.py
    module_4.py
```

In the top-level `__init__.py` add the following code

```py
from . import subpackage1
from . import subpackage2
```

Go to the `__init__.py` file in the `subpackage1` module and add the following code:

```py
from . import module1
from . import module2
```

Now if we want to import `function1` from `module2` in `module1`. We can add the following code
to `module1`.

```py
from .module2 import function1
```

Now you can go to the parent directory of `my_package` and import the package.
Lets use the Python repl to demonstrate this. We will execute a function in the `module1`
called `function1`

```bash
$ python
>>>import my_package
>>>my_package.subpackage1.module1.function1()
```

If you need to go up multiple levels in the directory structure you can use additional periods.

```py
from ..module2 import function1

```

Relative imports are great if you have lots of code files that are related.

***

## Conclusion

We can use import statements to pull code from various different sources like the
Python standard libraries, other modules within our project and Python packages we
pull using the `pip` command which we will learn more about in the following lessons.

***

## Resources

- [Python 3 Documentation](https://docs.python.org/3/)
- [Python import system](https://docs.python.org/3/reference/import.html)
