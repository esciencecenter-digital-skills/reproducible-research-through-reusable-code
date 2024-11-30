---
title: "Coding conventions and modular coding"
teaching: 5
exercises: 30
---

:::::::::::::::::::::::::::::::::::::: questions 

- Why should you follow software code style conventions?
- What code style conventions can you use in Python and R?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Know how to write readable code
- Know how to write modular code

::::::::::::::::::::::::::::::::::::::::::::::::

## Coding conventions and style guides

Readable code - for others and our future selves - should be descriptive, cleanly 
and consistently formatted, and use sensible, descriptive names for variables, functions 
and modules.  

In order to help us format our code, we can follow guidelines known as a style guide. 
A style guide is a set of conventions that we agree upon with our colleagues
or community, to ensure that people produce code which looks similar in style.
The most important thing about a style guide is that it provides consistency, making 
code easier to read and also easier to write - because you need to make fewer decisions.

::: challenge

::: tab
### Python style guide
Head over to [this lesson about the Python style guide](https://carpentries-incubator.github.io/python-intermediate-development/15-coding-conventions/index.html#python-coding-style-guide).  

Then take a look at (a part of) your own Python script, and identify where the guidelines 
have not been followed. Check the following:

- [Indentation](https://carpentries-incubator.github.io/python-intermediate-development/15-coding-conventions/index.html#indentation)
- [Whitespace in Expressions and Statements](https://carpentries-incubator.github.io/python-intermediate-development/15-coding-conventions/index.html#whitespace-in-expressions-and-statements)
- [Naming conventions](https://carpentries-incubator.github.io/python-intermediate-development/15-coding-conventions/index.html#naming-conventions)
- [Comments](https://carpentries-incubator.github.io/python-intermediate-development/15-coding-conventions/index.html#comments)

Fix the discovered inconsistencies and commit them to your working branch on GitHub.

### R (Tidyverse) style guide
Head over to [the Tidyverse style guide](https://style.tidyverse.org/).  

Then take a look at (a part of) your own R script, and identify where the guidelines 
have not been followed. Check the following:

- [Indentation](https://style.tidyverse.org/functions.html#multi-line-function-definitions)
- [Spacing](https://style.tidyverse.org/syntax.html#spacing)
- [File](https://style.tidyverse.org/files.html) and [object](https://style.tidyverse.org/syntax.html) 
naming conventions
- [Comments](https://style.tidyverse.org/functions.html#comments)

Fix the discovered inconsistencies and commit them to your working branch on GitHub.
You can use the [styler](http://styler.r-lib.org/) (with RStudio add-in) and [lintr](https://github.com/r-lib/lintr)
packages to (re-)style your code.

:::

:::

## Modular coding 

TBA

:::::::::::::::::::::::::::::::::::::::: keypoints

- Coding conventions help you create more readable code that is easier to reuse and contribute to.
- Consistently formatted code including descriptive variable and function names is easier to read and write

::::::::::::::::::::::::::::::::::::::::::::::::::
