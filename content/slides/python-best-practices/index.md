---
title: "Python best practices"
date: 2021-11-11T12:25:14+01:00
draft: false
---

## Table of contents

- Writing pythonic code
- Packaging and dependency management
- Working with notebooks

---

## Writing pythonic code

---

### The Zen of Python, by Tim Peters

```python
import this
```

```text
Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
```

---

### What does "pythonic" mean?

- Python code is considered _pythonic_ if it:
  - conforms to the Python philosophy;
  - takes advantage of the language's specific features.
- Pythonic code is **idiomatic Python code** that strives to be clean, concise and readable.

---

### Example: swapping two variables

```python
# Non-pythonic
tmp = a
a = b
b = tmp

# Pythonic
a, b = b, a
```

---

### Example: iterating on a list

```python
my_list = ["a", "b", "c"]

# Non-pythonic
i = 0
while i < len(my_list):
    do_something(my_list[i])
    i += 1

# Still non-pythonic
for i in range(len(my_list)):
    do_something(my_list[i])

# Pythonic
for item in my_list:
    do_something(item)
```

---

### Example: indexed traversal

```python
# Non-pythonic
for i in range(len(my_list)):
    print(i, "->", my_list[i])

# Pythonic
for i, item in enumerate(my_list):
    print(i, "->", item)
```

---

### Example: searching in a list

```python
fruits = ["apples", "oranges", "bananas", "grapes"]
fruit = "cherries"

# Non-pythonic
found = False
size = len(fruits)
for i in range(0, size):
    if fruits[i] == fruit:
        found = True

# Pythonic
found = fruit in fruits
```

---

### Example: generating a list

This feature is called [list comprehension](https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions).

```python
numbers = [1, 2, 3, 4, 5, 6]

# Non-pythonic
squares = []
for i in range(len(numbers)):
    if numbers[i] % 2 == 0:
        squares.append(numbers[i] * 2)
    else:
        squares.append(numbers[i])

# Pythonic
squares = [x * 2 if x % 2 == 0 else x for x in numbers]
```

---

### Code style

- [PEP8](https://www.python.org/dev/peps/pep-0008/) is the official style guide for Python:
  - use 4 spaces for indetation;
  - define a maximum value for line length (around 80 characters);
  - organize imports at beginning of file;
  - surround binary operators with a single space on each side;
  - ...
- Code style should be enforced upon creation by a tool like [black](https://github.com/psf/black).

---

### Beyond PEP8

Focusing on style and PEP8-compliance might make you miss more fundamental code imperfections.

{{< youtube wf-BqAjZb8M >}}

---

### Code linting

- _Linting_ is the process of checking code for syntactical and stylistic problems before execution.
- It is useful to catch errors and improve code quality in dynamically typed, interpreted languages, where there is no compiler.
- Several linters exist in the Python ecosystem. The most commonly used is [pylint](https://pylint.org/).

---

### Type annotations

- Added in Python 3.5, [type annotations](https://www.python.org/dev/peps/pep-0484/) allow to add type hints to code entities like variables or functions, bringing a statically typed flavour to the language.
- [mypy](http://mypy-lang.org/) can automatically check the code for annotation correctness.

```python
def greeting(name: str) -> str:
    return 'Hello ' + name

greeting('Alice')  # OK
greeting(3)  # mypy error: incompatible type "int"; expected "str"
```

---

## Packaging and dependency management

---

### Managing dependencies in Python

- Most Python apps depend on third-party libraries and frameworks (NumPy, Flask, Requests...).
- These tools may also have external dependencies, and so on.
- **Dependency management** is necessary to prevent version conflicts and incompatibilities. it involves two things:
  - a way for the app to declare its dependencies;
  - a tool to resolve these dependencies and install compatible versions.

---

### Semantic versioning

- Software versioning convention used in many ecosystems.
- A version number comes as a suite of three digits `X.Y.Z`.
  - X = major version (potentially including breaking changes).
  - Y = minor version (only non-breaking changes).
  - Z = patch.
- Digits are incremented as new versions are shipped.

---

### pip and requirements.txt

A `requirements.txt` file is the most basic way of declaring dependencies in Python.

```txt
certifi>=2020.11.0
chardet==4.0.0
click>=6.5.0, <7.1
download==0.3.5
Flask>=1.1.0
```

The [pip](https://pypi.org/project/pip/) package installer can read this file and act accordingly, downloading dependencies from [PyPI](https://pypi.org/).

`> pip install -r requirements.txt`

---

### Virtual environments

- A **virtual environment** is an isolated Python environment where a project's dependencies are installed.
- Using them prevents the risk of mixing dependencies required by different projects on the same machine.
- Several tools exist to manage virtual environments in Python, for example [virtualenv](https://virtualenv.pypa.io) and [conda](https://docs.conda.io).

---

### conda and environment.yml

Installed as part of the [Anaconda](https://www.anaconda.com/) distribution, the [conda](https://docs.conda.io) package manager reads an `environment.yml` file to install the dependencies associated to a specific virtual environment.

```yaml
name: example-env

channels:
  - conda-forge
  - defaults

dependencies:
  - python=3.7
  - matplotlib
  - numpy
```

---

### Poetry

Based on a `pyproject.toml` file, [Poetry](https://python-poetry.org) is a recent virtual environment, packaging and dependency management tool for Python.

```bash
# Create a new poetry-compliant project
poetry new <project name>

# Initialize an already existing project
poetry init

# Install defined dependencies
poetry install
```

---

### The pyproject.toml file

Soon-to-be standard for configuring Python projects.

```toml
[tool.poetry]
name = "propetry example"
version = "0.1.0"
description = ""

[tool.poetry.dependencies]
python = "^3.7"
jupyter = "^1.0.0"
matplotlib = "^3.3.2"
sklearn = "^0.0"
pandas = "^1.1.3"
ipython = "^7.0.0"

[tool.poetry.dev-dependencies]
pytest = "^6.1.1"
```

---

### Caret requirements

Offers a way to precisely define dependency versions.

| Requirement | Versions allowed |
| :---------: | :--------------: |
|   ^1.2.3    |  >=1.2.3 <2.0.0  |
|    ^1.2     |  >=1.2.0 <2.0.0  |
|   ~1.2.3    |  >=1.2.3 <1.3.0  |
|    ~1.2     |  >=1.2.0 <1.3.0  |
|    1.2.3    |    1.2.3 only    |

---

### The poetry.lock file

- The first time Poetry install dependencies, it creates a `poetry.lock` file that contains the exact versions of all installed packages.
- Subsequent installs will use these exact versions to ensure consistency.
- Removing this file and running another Poetry install will fetch the latest matching versions.

---

## Working with notebooks

---

TODO
