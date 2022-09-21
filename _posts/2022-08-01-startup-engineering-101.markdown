---
layout: post
tag: Learn
title: Startup Engineering 101
description: Software engineering best practices for fast-moving startups.
image: assets/posts/startup-engineering-101/splash.jpg
author: tlyleung
comments: false
---

“Move fast and break things” is a mantra popularised by Facebook during its growth phase. If you aren’t moving so fast that things are breaking, you’re not moving fast enough. This viewpoint is shared by many startups iterating quickly in search of product-market fit. But is there such a thing as too fast?

For technical founders, this article will be a routine list of non-negotiable engineering best practices. Still, for non-technical founders that are making their first engineering hires --- whether it’s contracting an offshore team on a freelancing platform or hiring an engineering student in university --- this list can be a helpful guide on how sacrificing a little short-term speed can help you thrive in the long run.

We’ve all seen it. Projects that slow to a crawl until a complete rewrite can no longer be put off. Most times, this occurs gradually. More and more features are built on top of an already shaky codebase and development loses momentum because even a small change can unearth a never-ending series of bugs that need to be fixed. Other times, switching developers can suddenly bring these issues to light. The new developer just finding it impossible to build on the work of the previous developer.

The recommendations below aren’t a guarantee of product success, but they will ensure that there’ll be significantly less technical debt. Examples will use the Python ecosystem, but the recommendations apply universally.

## Source Code

- **Code formatter:** use a code formatter (e.g. [Black](https://black.readthedocs.io/)) to output consistently formatted code. This removes the overhead of immaterial (but often heated) discussions of code formatting minutiae, such as tabs vs. spaces, the width of indents, single vs. double quotes, etc. Using a code formatter means that developers can write code in their own style, but all code checked into the repository is automatically reformatted.

  ```console
  $ black
  ```

  For languages with imported modules, additional tools like [isort](https://pycqa.github.io/isort/) can sort imports consistently.

  ```console
  $ isort --profile black
  ```

- **Linter:** use a linter (e.g. [Flake8](https://flake8.pycqa.org/)) to warn of syntax errors and possible bugs. There are varying degrees of strictness that can be fine-tuned, but users generally apply an accepted strictness level, e.g. a reasonable default for Flake8 is:

  ```console
  $ flake8 --max-line-length=88 --extend-ignore=E203,E501
  ```

- **Type checker:** use a type checker (e.g. [Mypy](https://mypy.readthedocs.io/)) with type annotations to find type-related bugs. Although Python is a dynamically typed programming language, meaning that types don’t need to be defined, type annotations produce code that is easier to understand and maintain.


  ```console
  $ mypy
  ```

- **Version control:** use version control (e.g. [Git](https://git-scm.com/)) to ensure that all the files in a single change are grouped together in a commit. Version control allows developers to see how files are modified, which facilitates knowledge sharing as well as allowing developers to atomically rollback a change. Having another engineer review code before committing a change to the codebase is recommended. This is done for correctness, comprehensibility, approval and knowledge sharing.

    A pre-commit hook should automatically run the code formatter, linter, type checker and test suite before committing a change to the codebase.

    Commit messages should follow a specific format for clarity and consistency. The commit message should use the imperative mood, be capitalised and not end with a period, e.g. "Add dropout to linear layer". See [How to Write a Git Commit Message](https://cbea.ms/git-commit/) for more details.

    Specific to data science and machine learning is the use of Jupyter notebooks. While they can be a powerful tool for exploratory work, notebooks are a mixture of text, code, rich media output and metadata, packaged in a JSON format. The use of notebooks can make it hard for a version control system to track changes. A common way to get around this is to use the [Jupytext](https://jupytext.readthedocs.io/) plugin to sync notebooks with Python files so that only the Python files are checked into the version control system. The output cells should be deleted  since they can be regenerated from the input cells.

## Documentation

- **In-code Documentation:** use a combination of module, class and function/method docstrings and block/inline comments.

    Docstrings are strings that document a Python module, class, function or method. A module docstring describes the contents and usage of the module. A class docstring describes the class and its attributes. A function/method docstring consists of a description of the function/method, its parameters, return value and exceptions that can be raised. HTML documentation can be automatically generated from consistent docstrings by a tool such as [Sphinx](https://www.sphinx-doc.org/). See the [Comments and Docstrings section](https://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings) of the [Google Style Guide](https://google.github.io/styleguide/pyguide.html) for more details.

    Block and inline comments are used to explain tricky parts of the code. Block comments explain complicated operations before they happen, while inline comments explain non-obvious operations at the end of a line.

- **Design Document:** a design document is a live document that covers the system’s current design. A good design document should cover:
    - design goals
    - implementation strategy
    - key design decisions, emphasising trade-offs
    - alternative designs, emphasising pros/cons
    - system architecture diagram
    - system-context diagram
    - system constraints
    - load testing methodology

## Testing

Automated testing lets you have confidence that the code works and that it conforms to its intended design. Running the entire test suite before a change is committed to the codebase ensures that the change doesn’t break any existing features. There are different types of tests:

- **Unit tests:** test each component of the system in isolation.
- **System tests:** test user interaction with the system.
- **Integration tests:** test how various parts of the system interact.

Some tests that are specific to Machine Learning models:

- **Model inference reproducibility test:** ensure same outputs when predicting using the same model. 
- **Model training reproducibility test:** ensure same outputs when predicting using a model retrained with the same data and hyperparameters.
- **Data perturbation test:** ensure small changes in input don’t lead to large changes in output.
- **Data invariance test:** ensure changes to non-predictive inputs don’t lead to changes in output.
- **Data directional expectation test:** ensure changes to inputs lead to predictable directional changes in output (this may not work due to feature collinearity).
