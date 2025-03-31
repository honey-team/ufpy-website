---
title: Getting started
description: How to install and use ufpy package.

tags:
  - information

hide:
  - navigation
---

# `ufpy` package

## Introduction

Ufpy (Useful Python) - is a package for simplifying Python programs using many useful features.

Now Ufpy has these features:

- [`UDict`](useful_classes/udict.md "Useful dict.").
- [`uSTL` package](uSTL/index.md).
    - [`Stack`](uSTL/stack.md).
- Generators of classes methods:
    - [`cmp_generator`](useful_features/generators.md "Compare generator. In latest python version were deleted __cmp__ method. With this generator you can use __cmp__ in your class")
    - [`r_generator`](useful_features/generators.md "Reverse generator. Generating __r...__ methods for math operations")
    - [`i_generator`](useful_features/generators.md "I methods generator. Generating __i...__ method for math operations")
- [many protocols for type hinting.](type_checking/protocols.md)
- [many type alias for type hinting.](type_checking/type_alias.md)

## Installing

To install `ufpy`, you need `python 3.12+` and `pip`.
After installing, use this command in your `cmd`/`bash` terminal:

=== "You have one python version"
    === "WIndows"
        ```shell
        pip install ufpy
        ```
    === "Linux"
        In Linux there isn't abillity to install packages globally (except Fedora, you can use `pip3`). But you can create `venv`!
        ```shell
        # If you haven't venv package -> install it
        sudo apt install python3.12-venv # On Debian, replace 3.12 with your version
        sudo dnf install python3.12-venv # On Fedora

        # Create venv
        python3.12 -m venv venv # replace 3.12 with your version
        ```
        Then activate it and install `ufpy`!
        ```shell
        source venv/bin/activate
        pip install ufpy
        ```


=== "Several versions"
    === "Windows"
        ```shell
        python -3.12 -m pip install ufpy
        # or
        py -3.12 -m pip install ufpy
        ```
    === "Linux"
        Create `venv` with specific python version.
        ```shell
        # If you haven't venv package -> install it
        sudo apt install python3.12-venv # On Debian, replace 3.12 with your version
        sudo dnf install python3.12-venv # On Fedora

        # Create venv
        python3.12 -m venv venv # replace 3.12 with your version
        ```
        Then activate it and install `ufpy`!
        ```shell
        source venv/bin/activate
        pip install ufpy
        ``` 

## Importing and writing some code

After installing, you can use `ufpy` package in all your projects with `3.12+` python version.
Just import `ufpy` or import certain classes, functions and variables.

```python
import ufpy
from ufpy import UDict
```

Enjoy!

## About the site

Site was made using `mkdocs` with `mkdocs material` theme. You can use search: just click `Search`
text input at the top of the page or use the ++s++ or ++f++ hotkeys. You can switch themes using the
button on the left and access the `ufpy` repository using the button on the right.

## Contribute

You can also contribute to `ufpy` package or `ufpy` docs site. Just 
[go to `ufpy` repository](https://github.com/honey-team/ufpy) using
button in right-top of page. For contributing to site you can
[go to `ufpy-website` repository](https://github.com/honey-team/ufpy-website).
