[![PyPI version](https://badge.fury.io/py/scipy-quadopt.svg)](https://badge.fury.io/py/scipy-quadopt)
[![PyPi downloads](https://img.shields.io/pypi/dm/scipy-quadopt)](https://img.shields.io/pypi/dm/scipy-quadopt)
[![DOI](https://zenodo.org/badge/355471428.svg)](https://zenodo.org/badge/latestdoi/355471428)
[![Total alerts](https://img.shields.io/lgtm/alerts/g/satzbeleg/scipy-quadopt.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/satzbeleg/scipy-quadopt/alerts/)
[![Language grade: Python](https://img.shields.io/lgtm/grade/python/g/satzbeleg/scipy-quadopt.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/satzbeleg/scipy-quadopt/context:python)
[![scipy-quadopt](https://snyk.io/advisor/python/scipy-quadopt/badge.svg)](https://snyk.io/advisor/python/scipy-quadopt)

# scipy-quadopt
Wrapper and utility functions to apply scipy's SLSQP algorithm to quadratic optimization problems with resource constraints and upper boundaries.

## Usage

```py
import numpy as np
import scipy_quadopt as sqp

# goodness scores
good = np.array([.51, .53, .55, .57])

# similarity matrices
simi_1 = np.array([
    [1, .9, .8, .7],
    [.9, 1, .6, .5],
    [.8, .6, 1, .4],
    [.7, .5, .4, 1],
])

simi_2 = np.array([
    [1, .7, .8, .3],
    [.7, 1, .4, .2],
    [.8, .4, 1, .6],
    [.3, .2, .6, 1],
])

# preference parameters
lam = 0.4
beta_1 = 0.25
beta_2 = 0.75

# compute weights
simi = sqp.aggregate_matrices(simi_1, beta_1, simi_2, beta_2)
weights, _ = sqp.get_weights(good, simi, lam)
```

## Appendix

### Installation
The `scipy-quadopt` [git repo](http://github.com/satzbeleg/scipy-quadopt) is available as [PyPi package](https://pypi.org/project/scipy-quadopt)

```
pip install scipy-quadopt
pip install git+ssh://git@github.com/satzbeleg/scipy-quadopt.git
```

### Install a virtual environment

```
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt --no-cache-dir
pip install -r requirements-dev.txt --no-cache-dir
```

(If your git repo is stored in a folder with whitespaces, then don't use the subfolder `.venv`. Use an absolute path without whitespaces.)

### Python commands

* Jupyter for the examples: `jupyter lab`
* Check syntax: `flake8 --ignore=F401 --exclude=$(grep -v '^#' .gitignore | xargs | sed -e 's/ /,/g')`
* Run Unit Tests: `PYTHONPATH=. pytest`

Publish

```sh
pandoc README.md --from markdown --to rst -s -o README.rst
python setup.py sdist 
twine upload -r pypi dist/*
```

### Clean up 

```
find . -type f -name "*.pyc" | xargs rm
find . -type d -name "__pycache__" | xargs rm -r
rm -r .pytest_cache
rm -r .venv
```


### Support
Please [open an issue](https://github.com/satzbeleg/scipy-quadopt/issues/new) for support.


### Contributing
Please contribute using [Github Flow](https://guides.github.com/introduction/flow/). Create a branch, add commits, and [open a pull request](https://github.com/satzbeleg/scipy-quadopt/compare/).


### Acknowledgements
This work was funded by the Deutsche Forschungsgemeinschaft (DFG, German Research Foundation) - [433249742](https://gepris.dfg.de/gepris/projekt/433249742). Project duration: 2020-2023.
