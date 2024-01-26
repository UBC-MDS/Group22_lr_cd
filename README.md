# lr_cd

[![Documentation Status](https://readthedocs.org/projects/lr-cd/badge/?version=latest)](https://lr-cd.readthedocs.io/en/latest/?badge=latest) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) ![version](https://img.shields.io/github/v/release/UBC-MDS/lr_cd) ![release](https://img.shields.io/github/release-date/UBC-MDS/lr_cd)

**lr_cd**: A better implementation of the linear regression in Python!

---------------------------------------------------------------------------------------

## Project Summary

We implement the linear regression by coordinate descent (CD) algorithm in this Python package. Please refer to the link for additional details about the [coordinate descent (CD) algorithm](https://en.wikipedia.org/wiki/Coordinate_descent) if you are unfamiliar with it.

Our package will have three major parts, including 1. simulated data generation, 2. coordinate descent algorithm, and 3. visualization of data and fitted linear regression line.

## Contributors

[Andy Zhang](https://github.com/andyzhangstat) for algorithm, [Sam Fo](https://github.com/fohy24) for data generation, and
[Jing Wen](https://github.com/Jing-19) for visualization.

## Functions

There are three major functions in this package:

- `generate_data_lr(n, n_features, theta, noise=0.2, random_seed=123)`: this function generates many random data points based on the theta coefficients, which will later be used for model fitting.
- `coordinate_descent(X, y, ϵ=1e-6, max_iterations=1000)`: this function performs coordinate descent to minimize the mean squared error of linear regression and therefore outputs the optimized intercept and coefficients vector.
- `plot_lr(X, y, intercept, coef)`: this function returns a scatter plot of the observed data points overlayed with a regression with optimized intercept and coefficients vector.

## Common Parameters

- `n` (integer): Number of data points.
- `n_features` (integer): Number of features to generate, excluding the intercept.
- `theta` (ndarray): True scalar intercept and coefficient weights vector. The first element should always be the intercept.
- `noise` (float): Standard deviation of a normal distribution added to the generated target y array as noise.
- `random_seed` (integer): Random seed to ensure reproducibility.
- `X` (ndarray): Feature data matrix, the independent variable.
- `y` (ndarray): Response data vector, the dependent variable. Both 'X' and 'y' should have the same number of observations.
- `ϵ` (float, optional): Stop the algorithm if the change in weights is smaller than the value (default is 1e-6).
- `max_iterations` (int, optional): Maximum number of iterations (default is 1000).
- `intercept` (float): Optimized intercept generated by the 'lr_cd' function. It will be used to calculate the estimated values using observed data 'X'.
- `coef` (ndarray): Optimized coefficient weights vector. It will be used to calculate the estimated values using observed data 'X'.

## Python Ecosystem Context

**lr_cd** establishes itself as a valuable enhancement to the Python ecosystem.
`LinearRegression` in Python package `scikit-learn` has a similar functionality. However, we use a different algorithm in the implementation and believe it will be a better one. `sklearn.linear_model.LinearRegression` contains a few optimization functions: `scipy.linalg.lstsq`, `scipy.sparse.linalg.lsqr` and `scipy.optimize.nnls` which basically rely on the singular value decomposition of feature matrix X. See the links for more information on [`sklearn.linear_model.LinearRegression`](https://scikit-learn.org/stable/modules/linear_model.html#ordinary-least-squares).

- **Beginner-Friendly** : **lr_cd** is quite easy to use for
beginners in Python and statistics. The well-written functions allow users to play with various simulated data and generate beautiful plots with little effort.

- **Reliable-Alternative** : The coordinate descent algorithm is known for fast convergence in various convex optimization problems. And current python package can be easily extended to a list of statistical models like Ridge Regression and Lasso Regression.

## Prerequisites

Make sure Miniconda or Anaconda is installed on your system

## Installation

#### Step 1: Clone the Repository

```bash
git clone git@github.com:UBC-MDS/lr_cd.git
cd lr_cd  # Navigate to the cloned repository directory
```

#### Step 2: Create and Activate the Conda Environment

```bash
# Method 1: create Conda Environment from the environment.yml file
conda env create -f environment.yml  # Create Conda environment
conda activate lr_cd  # Activate the Conda environment

# Method 2: create Conda Environment 
conda create --name lr_cd python=3.9 -y
conda activate lr_cd
```

#### Step 3: Install the Package Using Poetry

Ensure the Conda environment is activated (you should see (lr_cd) in the terminal prompt)

```bash
poetry install  # Install the package using Poetry
```

#### Step 4: Get the coverage

```bash
# Check line coverage
pytest --cov=lr_cd

# Check branch coverage
pytest --cov-branch --cov=lr_cd
poetry run pytest --cov-branch --cov=src
poetry run pytest --cov-branch --cov=lr_cd --cov-report html
```

## Troubleshooting

1. Environment Creation Issues: Ensure environment.yml is in the correct directory and you have the correct Conda version

2. Poetry Installation Issues: Verify Poetry is correctly installed in the Conda environment and your pyproject.toml file is properly configured

## Usage

We can use this package to find the optimized intercept and coefficients vector of linear regression. In the following example, we generate a simulated data set with feature matrix and response first. By the coordinate descent algorithm, we obtain the optimized intercept and coefficients. Finally, we visualize both the simulated data and fitted line in one figure.

Example usage:

```python
>>> from lr_cd.lr_data_generation import generate_data_lr
>>> import numpy as np
>>> theta = np.array([4, 3])
>>> X, y = generate_data_lr(n=10, n_features=1, theta=theta)

>>> from lr_cd.lr_cd import coordinate_descent
>>> intercept, coef, _ = coordinate_descent(X, y)

>>> from lr_cd.lr_plotting import plot_lr
>>> plot_lr(X, y, intercept, coef)
```

<img src="<https://github.com/UBC-MDS/lr_cd/blob/main/img/plot.png?raw=true">  height="300">

## Documentations

Online documentation is available [here]().

Publishing on [TestPyPi]() and [PyPi]().

## Contributing

Interested in contributing? Check out the contributing guidelines. Please note that this project is released with a Code of Conduct. By contributing to this project, you agree to abide by its terms.

## License

`lr_cd` was created by Sam Fo, Jing Wen, Andy Zhang. It is licensed under the terms of the MIT license.

## Credits

`lr_cd` was created with [`cookiecutter`](https://cookiecutter.readthedocs.io/en/latest/) and the `py-pkgs-cookiecutter` [template](https://github.com/py-pkgs/py-pkgs-cookiecutter).
