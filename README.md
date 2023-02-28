# poetry-multiple-py-versions

## setup 1:

* `pyenv install 3.7.16`
* `poetry env use /home/ubuntu/.pyenv/versions/3.7.16/bin/python`
* `poetry install`
* `poetry run poetry_multiple_py_versions` ✅


## setup 2: (cont from setup 1)

* `pyenv install 3.10.10`
* update `pyproject.toml` from `python = "=3.7.16"` to `python = "=3.10.10"`
* `poetry env use /home/ubuntu/.pyenv/versions/3.10.10/bin/python`
* `poetry install`
* `poetry run poetry_multiple_py_versions` ✅

## setup 3: (cont from setup 2)

* update `pyproject.toml` remove `python = "=3.10.10"`.
* `poetry install`
* `poetry run poetry_multiple_py_versions` ✅
* `poetry run python --version` gives -- `Python 3.10.10`

## setup 4: (cont from setup 3)

* `rm poetry.lock`
* `poetry install` gives
    ```console
    $ poetry install
    Updating dependencies
    Resolving dependencies... (0.3s)

    The current project's Python requirement (>=2.7,<2.8 || >=3.4) is not compatible with some of the required packages Python requirement:
    - typer requires Python >=3.6, so it will not be satisfied for Python >=2.7,<2.8 || >=3.4,<3.6

    Because no versions of typer match >0.7.0,<0.8.0
    and typer (0.7.0) requires Python >=3.6, typer is forbidden.
    So, because poetry-multiple-py-versions depends on typer (^0.7.0), version solving failed.

    • Check your dependencies Python requirement: The Python requirement can be specified via the `python` or `markers` properties
        
        For typer, a possible solution would be to set the `python` property to ">=3.6"

        https://python-poetry.org/docs/dependency-specification/#python-restricted-dependencies,
        https://python-poetry.org/docs/dependency-specification/#using-environment-markers
    ```
