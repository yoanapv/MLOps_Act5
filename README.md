# Activity Session 5: pre-commit
Student: A01688744 - Norma Yoana Pérez Villalva

## Pre-commits
Pre-commits are automated checks that run on your code before you commit changes, helping ensure code quality and consistency. In this guide, we'll use the `pre-commit` tool to set up pre-commits for Python projects in Visual Studio Code (VSC).

### Prerequisites

1. Python is installed on your system.
2. Visual Studio Code (VSC) is installed on your system.
3. `pip` is installed on your system.

### Step 1: Install `pre-commit`

First, you need to install the `pre-commit` tool on your system. Open your terminal or command prompt and run the following command:

```bash
pip install pre-commit
```

### Step 2: Install libraries
```bash
pip install autopep8 flake8 isort autoflake ruff
```

### Step 3: Create a Pre-Commit Configuration File
Create a file named `.pre-commit-config.yaml` in the root of your Python project. This file will define the pre-commit hooks to be executed.

### Step 4: Configure Pre-Commit Hooks
In the `.pre-commit-config.yaml` file, define the pre-commit hooks you want to run. Each hook represents a specific check on your code. There are many pre-configured hooks available, and you can also create custom hooks if needed.

Here's the code `.pre-commit-config.yaml` with the pre-commit hooks we will use:

```yaml
repos:
- repo: https://github.com/pre-commit/mirrors-autopep8
  rev: ''  # Specify a specific version/tag/commit or leave empty for the latest version
  hooks:
    - id: autopep8
      exclude: '^$'  # Specify files or patterns to exclude, '^$' excludes nothing (all files will be checked)
      args: [--verbose]

- repo: https://github.com/PyCQA/flake8
  rev: 6.0.0
  hooks:
    - id: flake8
      args: [--ignore=E501]

- repo: https://github.com/PyCQA/isort
  rev: 5.12.0
  hooks:
    - id: isort
      name: isort (python)
      args: ["--profile", "black", "--filter-files"]

-   repo: https://github.com/PyCQA/autoflake
    rev: v2.2.0
    hooks:
    - id: autoflake

- repo: https://github.com/astral-sh/ruff-pre-commit
  rev: v0.0.280
  hooks:
    - id: ruff
      name: ruff
      args: [--fix]
      language: system
      types_or: [ python, pyi ]

```

### Step 5: Initialize Pre-Commit for Your Project
After creating the `.pre-commit-config.yaml` file, initialize pre-commit for your project. Open your terminal or command prompt, navigate to the root directory of your project, and run the following command:
```bash
pre-commit install
```
Output
```bash
pre-commit installed at .git/hooks/pre-commit
```
> **NOTE**  
If you want to see the default hidden folder `.git`, follow the steps in this link: https://linuxpip.org/vscode-show-hidden-files/

### Step 6: Commit Your Changes
With the pre-commit hooks installed, you can now make changes to your Python code. When you're ready to commit your changes, run the following command to trigger the pre-commit checks:

```bash
git commit -m "add pre-commit file"
```

### Step 7. Add a new file
* Please create a python file called `iris.py`, and copy the following code into it.

## Code
The following Python code will be used to test the repos in that you have included in the `.pre-commit-config.yaml` file.

* Modify the Python `iris.py` file with this code:
    ```python
    import os # This is an unused import
    import json # This is an unused import
    from sklearn.datasets import load_iris # Import in incorrect order

    import numpy as np # Import in incorrect order
    import json # This is an unused import

    from my_library import test # This is an unused import
    from sklearn.linear_model import LogisticRegression # Import in incorrect order

    # Load data from sklearn
    X, y = load_iris(return_X_y=True)

    # Train the model using regresion logistic
    clf = LogisticRegression(solver='lbfgs',max_iter=1000,multi_class='multinomial').fit(X, y)
    # Define iris types
    iris_type = {0: 'setosa',1: 'versicolor',2: 'virginica'}


    # Define dummy values
    sepal_length, sepal_width, petal_length, petal_width = 2, 3, 4, 6

    X = [sepal_length, sepal_width, petal_length, petal_width]


    # Make a prediction

    prediction = clf.predict_proba([X])
    print({'class': iris_type[np.argmax(prediction)],'probability':round(max(prediction[0]), 2)})
    ```
    
* Do the commit to activate the pre-commit. The `iris.py` file output should look like this:
    ```python
    import numpy as np
    from sklearn.datasets import load_iris
    from sklearn.linear_model import LogisticRegression

    # Load data from sklearn
    X, y = load_iris(return_X_y=True)

    # Train the model using regresion logistic
    clf = LogisticRegression(
        solver='lbfgs',
        max_iter=1000,
        multi_class='multinomial').fit(X, y)
    # Define iris types
    iris_type = {0: 'setosa', 1: 'versicolor', 2: 'virginica'}


    # Define dummy values
    sepal_length, sepal_width, petal_length, petal_width = 2, 3, 4, 6

    X = [sepal_length, sepal_width, petal_length, petal_width]


    # Make a prediction

    prediction = clf.predict_proba([X])
    print({'class': iris_type[np.argmax(prediction)],
        'probability': round(max(prediction[0]), 2)})
    ```

    The corrected code above should be the one that is going to be sent to the repository.

## END