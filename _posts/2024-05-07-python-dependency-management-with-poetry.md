---
layout: single
title: "python: dependency management with poetry"
categories: python
tag: [python, dependency-management, virtualenv]
---
## Introduction

In this post, I am going talk about managing dependency for python applications using `Poetry`.

## What is Poetry?

"_Poetry is a tool for dependency management and packaging in Python. It allows you to declare the libraries your project depends on and it will manage (install/update) them for you. Poetry offers a lockfile to ensure repeatable installs, and can build your project for distribution"_ [[Poetry Website]](https://python-poetry.org/docs/).

Basically it does the work of pip (python package manager) and virtualenv(dependency management and virtualenv) all together.

## Why shift from virtualenv to Poetry?

In a [previous post](https://rogerkimjazzlover.github.io/cmpnyinfo/cmpnyinfo-the-first-step/), I briefly talked about version control and dependency management in python using `virtualenv`. However, I got to work on a new project as a backend developer, project ['TOYKI'](https://toyki-homepage.vercel.app/), with my college colleague. ['TOYKI'](https://toyki-homepage.vercel.app/) is a service that provides opportunities to overcome the limitations of offline human relationships and enables everyone to build social networks more easily. Learn more in our [website](https://toyki-homepage.vercel.app/).

TOYKI project is larger in scale compared to my previous projects, and more people will be working on it. So we seeked for a more professional and handy tool, and found Poetry. The handy features of Poetry, such as
1. automatically updating `pyproject.toml` file
2. the `poetry.lock` file
3. Integration of package management and virtualenv.

and more, made us use it for our version control.

## Install

Please refer to [official documentation](https://python-poetry.org/docs/#installing-with-the-official-installer)
- https://python-poetry.org/docs/#installing-with-the-official-installer

If you already have ***pip*** in your device,
- ```pip install poetry```

You can also install using ***curl***,
- ```curl -sSL https://install.python-poetry.org | python3 -```
- In linux/Unix, it will be stored in `~/.local/share/pypoetry`
- You might need to manually add it to PATH in your `.bashrc` or `.bash_profile` file. 
   - ```export PATH="$HOME/.local/share/pypoetry:$PATH"```

## Virtual Environment

You can create a virtual environment using Poetry as well. By default, the `.venv` file will be stored in the home directory. However, I prefer the ***.venv file to be in project folder.***
- ```poetry config virtualenvs.in-project true```

Now you have to ***activate*** the virtual environment.
- ```poetry shell```

Other commands
- ```python -m poetry env list``` -> show all the list of venvs in your pwd or above. ***However***, if you set the path for .venv file to be in your project-folder, this command is ***practically useless***.
- ```python3 -m poetry env remove path```
- ```python3 -m poetry env info``` -> show the info about the venv

## Basics

### Create new project

```python3 -m poetry new project_name```

This will create a new directroy from your current working directory with your `project_name`.
```
project_name
├── pyproject.toml
├── README.md
├── project_name
│   └── __init__.py
└── tests
    └── __init__.py
```
### pyproject.toml
**`pyproject.toml`**: file stores the information about the dependencies/packages. It's just like `requirements.txt` file. The difference is that it will get _automatically updated_.

### Add&Install dependency

If you have a pre-configured `pyproject.toml` file, and want to install dependencies stated in the `pyproject.toml` file,
- ```python poetry install```

### poetry.lock
When you first run this command without a pre-configured **`poetry.lock`** file that was written previously by other developers, then it will create one for you.
- **`poetry.lock`**: this file stores the information about the dependencies/packages that should not be automatically installed with latest version when using `python poetry install`. By default, poetry will install the latest versions of the packages in the `pyproject.toml` file when you run `python poetry install` without a `poetry.lock` file. It ensures that everybody is using the exact same version of the dependencies!

If you want to add/remove a dependency or python package,
- ```python poetry add package_name```
- ```python poetry add "package_name=version.version.version"```
- ```python poetry remove package_name```


**Other Basics**
- ```python poetry show``` -> show all the packages

## Contact Me:

Roger Kim

[Github](https://github.com/RogerKimJazzLover)

e-mail: <minseungkim1017@gmail.com> 