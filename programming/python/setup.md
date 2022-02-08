---
title: Project setup - Python
description: 
published: true
date: 2022-02-08T19:54:51.530Z
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

* Configuration in: `pyproject.toml`.
* With coverage reporting and failure under 100% coverage.
* HTML report for detailed analysis.

### black

```bash
black (path/to/code)
```

Configuration in: `pyproject.toml`

### flake8

```bash
flake8 (path/to/code)
```

* Configuration in: `setup.cfg`
* plugins:
  * annotations
  * black
  * bandit
  * bugbear
  * darglint
  * docstring
  * import-order

### mypy

```bash
mypy (path/to/code)
```
Configuration in: `pyproject.toml`

# Todo

* checkout tox vs nox
* https://cjolowicz.github.io/posts/hypermodern-python-02-testing/#endtoend-testing
* pytype 
* typeguard 
* sphinx 
* https://github.com/pyupio/safety

# References

1. black manual
1. flake8 manual + github
1. [sqlalchemy](https://github.com/sqlalchemy/sqlalchemy/)
1. pytest manual
1. [Hyper moden python](https://cjolowicz.github.io/posts/hypermodern-python-01-setup/), while I found most information by checking out various tools, which tend to refer to each other, this blog series is a nice summary.
