---
title: "Software dependencies"
teaching: 5
exercises: 20
editor_options: 
  markdown: 
    wrap: 72
---

::: questions
-   How can I manage package and software dependencies?
:::

::: objectives
-   Know how to track dependencies of a project
-   Set up an environment and make sure others can reproduce your
    environment
:::

## Creating Virtual Environments Using `venv` in Python

Creating a virtual environment with venv is done by executing the
following command:

``` bash
$ python3 -m venv /path/to/new/virtual/environment
```

where `/path/to/new/virtual/environment` is a path to a directory where
you want to place it - conventionally within your software project so
they are co-located. This will create the target directory for the
virtual environment (and any parent directories that don’t exist
already).

::: callout
## What is the `-m` Flag in the `python3` Command?

The Python `-m` flag means "module" and tells the Python interpreter to
treat what follows `-m` as the name of a module and not as a single,
executable program with the same name. Some modules (such as `venv` or
`pip`) have main entry points and the `-m` flag can be used to invoke
them on the command line via the `python` command. The main difference
between running such modules as standalone programs (e.g. executing
"venv" by running the `venv` command directly) versus using `python3 -m`
command seems to be that with latter you are in full control of which
Python module will be invoked (the one that came with your environment's
Python interpreter vs. some other version you may have on your system).
This makes it a more reliable way to set things up correctly and avoid
issues that could prove difficult to trace and debug.
:::

::: challenge
For our project let us create a virtual environment called “venv”.
First, ensure you are within the project root directory, then:

``` bash
$ python3 -m venv venv
```

If you list the contents of the newly created directory "venv", on a Mac
or Linux system (slightly different on Windows as explained below) you
should see something like:

``` bash
$ ls -l venv
```

``` output
total 8
drwxr-xr-x  12 alex  staff  384  5 Oct 11:47 bin
drwxr-xr-x   2 alex  staff   64  5 Oct 11:47 include
drwxr-xr-x   3 alex  staff   96  5 Oct 11:47 lib
-rw-r--r--   1 alex  staff   90  5 Oct 11:47 pyvenv.cfg
```

So, running the `python3 -m venv venv` command created the target
directory called "venv" containing:

-   `pyvenv.cfg` configuration file with a home key pointing to the
    Python installation from which the command was run,
-   `bin` subdirectory (called `Scripts` on Windows) containing a
    symlink of the Python interpreter binary used to create the
    environment and the standard Python library,
-   `lib/pythonX.Y/site-packages` subdirectory (called
    `Lib\site-packages` on Windows) to contain its own independent set
    of installed Python packages isolated from other projects, and
-   various other configuration and supporting files and subdirectories.
:::

::: callout
## Naming Virtual Environments

What is a good name to use for a virtual environment? Using "venv" or
".venv" as the name for an environment and storing it within the
project's directory seems to be the recommended way - this way when you
come across such a subdirectory within a software project, by convention
you know it contains its virtual environment details. A slight downside
is that all different virtual environments on your machine then use the
same name and the current one is determined by the context of the path
you are currently located in. A (non-conventional) alternative is to use
your project name for the name of the virtual environment, with the
downside that there is nothing to indicate that such a directory
contains a virtual environment. In our case, we have settled to use the
name "venv" instead of ".venv" since it is not a hidden directory and we
want it to be displayed by the command line when listing directory
contents (the "." in its name that would, by convention, make it
hidden). In the future, you will decide what naming convention works
best for you. Here are some references for each of the naming
conventions: - [The Hitchhiker's Guide to
Python](https://docs.python-guide.org/dev/virtualenvs/) notes that
"venv" is the general convention used globally - [The Python
Documentation](https://docs.python.org/3/library/venv.html) indicates
that ".venv" is common - ["venv" vs ".venv"
discussion](https://discuss.python.org/t/trying-to-come-up-with-a-default-directory-name-for-virtual-environments/3750)
:::

::: challenge
## Activating and deactivating the virtual environment

Once you’ve created a virtual environment, you will need to activate it.

On Mac or Linux, it is done as:

``` bash
$ source venv/bin/activate
(venv) $ 
```

On Windows, recall that we have `Scripts` directory instead of `bin` and
activating a virtual environment is done as:

``` bash
$ source venv/Scripts/activate
(venv) $ 
```

Activating the virtual environment will change your command line’s
prompt to show what virtual environment you are currently using
(indicated by its name in round brackets at the start of the prompt:
`(venv)`), and modify the environment so that running Python will get
you the particular version of Python configured in your virtual
environment.

You can verify you are using your virtual environment's version of
Python by checking the path using the command `which`:

``` bash
(venv) $ which python3
```

``` output
path/to/new/virtual/environment/venv/bin/python3
```

When you’re done working on your project, you can exit the environment
with:

``` bash
(venv) $ deactivate
```

If you have just done the `deactivate`, ensure you reactivate the
environment ready for the next part:

``` bash
$ source venv/bin/activate
```
:::

::: callout
## Python Within A Virtual Environment

Within an active virtual environment, commands `python3` and `python`
should both refer to the version of Python 3 you created the environment
with (note you may have multiple Python 3 versions installed).

However, on some machines with Python 2 installed, `python` command may
still be hardwired to the copy of Python 2 installed outside of the
virtual environment - this can cause errors and confusion.

You can always check which version of Python you are using in your
virtual environment with the command `which python` to be absolutely
sure. We continue using `python3` in this material to avoid mistakes,
but the command `python` may work for you as expected.
:::

::: challenge
## Installing External Packages Using `pip`

Let's take the example in which our code depends on two *external
packages/libraries* - `numpy` and `matplotlib`. In order for the code to
run on your machine, you need to install these two dependencies into
your virtual environment.

To install the latest version of a package with `pip` you use pip's
`install` command and specify the package’s name, e.g.:

``` bash
(venv) $ python3 -m pip install numpy
(venv) $ python3 -m pip install matplotlib
```

or like this to install multiple packages at once for short:

``` bash
(venv) $ python3 -m pip install numpy matplotlib
```

If you run the `python3 -m pip install` command on a package that is
already installed, `pip` will notice this and do nothing.

To install a specific version of a Python package give the package name
followed by `==` and the version number, e.g.
`python3 -m pip install numpy==1.21.1`.

To specify a minimum version of a Python package, you can do
`python3 -m pip install numpy>=1.20`.

To upgrade a package to the latest version, e.g.
`python3 -m pip install --upgrade numpy`.

To display information about a particular installed package do:

``` bash
(venv) $ python3 -m pip show numpy
```

``` output
Name: numpy
Version: 1.26.2
Summary: Fundamental package for array computing in Python
Home-page: https://numpy.org
Author: Travis E. Oliphant et al.
Author-email: 
License: Copyright (c) 2005-2023, NumPy Developers.
All rights reserved.
...
Required-by: contourpy, matplotlib
```

To list all packages installed with `pip` (in your current virtual
environment):

``` bash
(venv) $ python3 -m pip list
```

``` output
Package         Version
--------------- -------
contourpy       1.2.0
cycler          0.12.1
fonttools       4.45.0
kiwisolver      1.4.5
matplotlib      3.8.2
numpy           1.26.2
packaging       23.2
Pillow          10.1.0
pip             23.0.1
pyparsing       3.1.1
python-dateutil 2.8.2
setuptools      67.6.1
six             1.16.0
```

To uninstall a package installed in the virtual environment do:
`python3 -m pip uninstall <package-name>`. You can also supply a list of
packages to uninstall at the same time.
:::

::: challenge
### Exporting/Importing Virtual Environments Using `pip`

You are collaborating on a project with a team so, naturally, you will
want to share your environment with your collaborators so they can
easily 'clone' your software project with all of its dependencies and
everyone can replicate equivalent virtual environments on their
machines. `pip` has a handy way of exporting, saving and sharing virtual
environments.

To export your active environment - use `python3 -m pip freeze` command
to produce a list of packages installed in the virtual environment. A
common convention is to put this list in a `requirements.txt` file:

``` bash
(venv) $ python3 -m pip freeze > requirements.txt
(venv) $ cat requirements.txt
```

``` output
contourpy==1.2.0
cycler==0.12.1
fonttools==4.45.0
kiwisolver==1.4.5
matplotlib==3.8.2
numpy==1.26.2
packaging==23.2
Pillow==10.1.0
pyparsing==3.1.1
python-dateutil==2.8.2
six==1.16.0
```

The first of the above commands will create a `requirements.txt` file in
your current directory. Yours may look a little different, depending on
the version of the packages you have installed, as well as any
differences in the packages that they themselves use.

The `requirements.txt` file can then be committed to a version control
system (e.g., using Git) and get shipped as part of your software and
shared with collaborators and/or users. They can then replicate your
environment and install all the necessary packages from the project root
as follows:

``` bash
(venv) $ python3 -m pip install -r requirements.txt
```

As your project grows - you may need to update your environment for a
variety of reasons. For example, one of your project's dependencies has
just released a new version (dependency version number update), you need
an additional package for data analysis (adding a new dependency) or you
have found a better package and no longer need the older package (adding
a new and removing an old dependency). What you need to do in this case
(apart from installing the new and removing the packages that are no
longer needed from your virtual environment) is update the contents of
the `requirements.txt` file accordingly by re-issuing `pip freeze`
command and propagate the updated `requirements.txt` file to your
collaborators via your code sharing platform (e.g. GitHub).
:::

::: callout
## Official Documentation

For a full list of options and commands, consult the [official `venv`
documentation](https://docs.python.org/3/library/venv.html) and the
[Installing Python Modules with `pip`
guide](https://docs.python.org/3/installing/index.html#installing-index).
Also check out the guide ["Installing packages using `pip` and virtual
environments"](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/#installing-packages-using-pip-and-virtual-environments).
:::

Source of these exercises is the [Carpentries Intermediate Research
Software Development Skills
(Python)](https://carpentries-incubator.github.io/python-intermediate-development/12-virtual-environments/index.html#creating-virtual-environments-using-venv)
lesson.

## Creating and sharing reproducible environments with `renv` in RStudio

### The need for dependency management
An external R package is any software library that is not included with base R (it doesn’t 
just come automatically with the R installation.) Packages are one of the biggest advantages 
of using R: there are so many packages available to allow us to do so many different things 
without having to code the functions ourselves. However, using packages can result in some 
headaches, too.

Using packages in our code means that the code *depends* on those packages to run correctly 
as it was meant to. If someone else wants to run our code, they will have to install the 
necessary packages first. But what happens if the code was written using a long time ago 
using an old version of a package, and by doing `install.packages` that person gets a newer 
version that does not work the same way? This can also happen when we try to run our own 
code a year after we have written it, after having reinstalled R, or after changing computers. 
Packages are constantly maintained and they can change. Functions can be re-written and 
behave differently than they did when we first wrote the code. Sometimes our code can 
break even if something changes in a package that we are not loading directly, but that 
the package we’re using depends on. Even though it’s good practice to keep our software 
up-to-date, updating packages can break things and generate a lot of frustration.

These frustrations can be greatly reduced by adopting a dependency management system. 
Dependency management is the process of keeping track of dependencies in our code. This 
means keeping track of which packages we are loading, which packages those packages depend 
on, and which version of each package we are using.

### The `renv` package
The `renv` package is a dependency management system for R. Normally, when you install an 
R package, this gets saved in your user library, which is centralized somewhere in your 
computer (find out where using `.libPaths()`). Each time you load a package in an R session, 
the package will be loaded from that centralized library. The basic concept behind `renv` is 
to de-centralize this process by having Project-specific libraries. This means that you can 
have different RStudio Projects each with their own version of the same package. The library 
and all your package dependencies are a property of an RStudio Project. However, because 
`renv` uses a global package cache that is shared across all the projects that use `renv`, 
packages are not physically duplicated (which would be very inefficient in terms of space.)

Having Project-specific libraries means that installing a new version of a package in one 
Project won’t break any others that may rely on a different version. It also means that your
RStudio Project is truly a portable unit, where it’s easy to get all your dependencies working
if you transport the Project on a different computer. This also helps make your code 
reproducible because you can share your project environment alongside the code so that 
somebody else can automatically reproduce it on their computer.

::: challenge
## Using `renv` in RStudio

Using renv and creating lockfiles is very easy, requiring little to no modification to your 
existing workflows. Everything happens inside an R project, so make sure you create a 
separate project for each analysis for which you want to make a reproducible environment. 
You will also need to install renv before starting:

```r
install.packages('renv')
```

When you are ready to start working, run:

```r
renv::init()
```

This will initialize a new environment specific to your current project. You can now work 
as you normally would: writing code, installing packages, and loading them as and when you 
need. 
Initializing `renv` on a project will save four files to your project directory:

- An `.Rprofile` file, which will activate your environment each time you open a new 
project session;
- An `renv.lock` file, which describes the state of your project’s library (what 
packages are loaded and in what version) at some point in time;
- An `renv/activate.R` file which is the script run by `.Rprofile`;
- And an `renv/library` folder which is your local project library.

The first three files should be put under version control. The library itself is 
automatically put in `.gitignore` by `renv` (it can’t hurt to double check). After 
your project-local environment is set up, you can keep working on your project normally.

When you are ready to take a snapshot of your current environment run:

```r
renv::snapshot()
```

To save the state of the project environment to the lockfile (`renv.lock`) in your project 
home directory. This details of which packages you used and their versions are now recorded 
to ensure that you environment is reproducible. You can continue working now and make further 
changes, and update the lockfile by running `renv::snapshot()` again.

Perhaps you have made changes to your environment (eg updated a package that breaks your code). 
You can return to your previous state saved in the lockfile by running:

```r
renv::restore()
```

this will return to the packages and version the last time you called `renv::snapshot()`.

But what if you already have a project and you want to start using renv to manage the code 
and packages. No problem. Simply open the project and run `renv::init()`. The newly-created 
project environment search for any packages loaded in R files within the project, install 
them to the local package library, when you call `renv::snapshot()` these packages will be 
included in the lockfile.

:::

:::callout
Tip: run all `renv::` commands directly in the R console. There is no need to save them in your 
scripts because they only need to be run once, or infrequently, per project.
:::

:::challenge
## Restoring an existing project using renv

Every time you open a project for which `renv` has been set up, `renv` automatically runs and 
checks that the package versions you have installed on your computer match those of the 
project. If they match, there is nothing to do (perhaps that was the case for you today). 
But if there are any mismatches (as might have happened to you today), `renv` will print a 
warning resembling the following:

```r
Project '~/Desktop/myproject' loaded. [renv 0.16.0]
The project library is out of sync with the lockfile.
Use `renv::restore()` to install packages recorded in the lockfile.
```

If this happens, simply run `renv::restore()` from the console pane to download and 
install the package versions needed to match the project’s requirements. For example, 
if the project uses tidyverse 1.3.2 and you have an older version tidyverse 1.3.1 installed 
on your computer, renv will upgrade your RStudio installation to tidyverse 1.3.2. 
(This works conversely as well: if the project uses an older version of a package you 
have installed, `renv` will attempt to download and install the older version for you. 
Don’t worry about losing the newer version. `renv` ensures that all versions of all packages
remain installed on your computer, available for use by projects as needed).

In sum, in order to collaborate using `renv`, one should:

- Initialize renv using `renv::init()`
- Share project sources (data and code), and include `renv.lock`, `.Rprofile`, and 
`renv/activate.R` to ensure that collaborators download and install the right 
version of the packages when starting the project.
- When a collaborator opens the project, `renv` will automatically bootstrap and 
download the appropriate version of all dependencies.
- If updates are made save them with `renv::snapshot()`
- After that, collaborators can use `renv::restore()` to restore the project library 
on their machine.

:::

Source of these exercises are the [Introduction to Reproducible Publications with RStudio](https://ucsbcarpentry.github.io/Reproducible-Publications-with-RStudio-Quarto/03-collaboration/05-renv/index.html)
and [Tools for Reproducible Science](https://ecorepsci.github.io/reproducible-science/renv.html) lessons.


::: keypoints
Python keypoints:

-   Virtual environments keep Python versions and dependencies required
    by different projects separate.

-   A virtual environment is itself a directory structure.

-   Use `venv` to create and manage Python virtual environments.

-   Use `pip` to install and manage Python external (third-party)
    libraries.

-   `pip` allows you to declare all dependencies for a project in a
    separate file (by convention called `requirements.txt`) which can be
    shared with collaborators/users and used to replicate a virtual
    environment.

-   Use `python3 -m pip freeze > requirements.txt` to take snapshot of
    your project's dependencies.

-   Use `python3 -m pip install -r requirements.txt` to replicate
    someone else's virtual environment on your machine from the
    `requirements.txt` file.

R keypoints:

-   `renv` is a handy tool for capturing your project’s package dependencies

-   Initialize renv using `renv::init()`
-   Share project sources (data and code), and include `renv.lock`, `.Rprofile`, and 
`renv/activate.R` to ensure that collaborators download and install the right 
version of the packages when starting the project.

-   When a collaborator opens the project, `renv` will automatically bootstrap and 
download the appropriate version of all dependencies.

:::
