---
title: Project setup - Python
description: 
published: true
date: 2022-02-08T18:31:07.235Z
tags: 
editor: markdown
dateCreated: 2022-02-08T18:27:45.879Z
---

# Project setup - Python

See [bob](/programming/python/project/bob)

The bob project integrates:
* unit testing with pytest.
* code formatting with black.
* type checking with mypy.
* linting with flake8 and pylint.
* testing all the above with tox.


### pytest

```bash
pytest
```

Configuration in: `pyproject.toml`

### black

```bash
black (path/to/code)
```

Configuration in: `pyproject.toml`

### flake8

```bash
flake8 (path/to/code)
```

Configuration in: `setup.cfg`

### mypy

```bash
mypy (path/to/code)
```
Configuration in: `pyproject.toml`
