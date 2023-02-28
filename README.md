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
* `poetry build` works 🤷🏻‍♂️
    ```console
    $ poetry build
    Building poetry-multiple-py-versions (0.1.0)
    - Building sdist
    - Built poetry_multiple_py_versions-0.1.0.tar.gz
    - Building wheel
    - Built poetry_multiple_py_versions-0.1.0-py2.py3-none-any.whl
    ```
* `/home/ubuntu/.pyenv/versions/3.7.16/bin/python -m venv .venv3.7.16`
* `.venv3.7.16/bin/python -m pip install dist/poetry_multiple_py_versions-0.1.0-py2.py3-none-any.whl`
* `.venv3.7.16/bin/poetry_multiple_py_versions` works ✅
* `/home/ubuntu/.pyenv/versions/3.10.10/bin/python -m venv .venv3.10.10`
* `.venv3.10.10/bin/python -m pip install dist/poetry_multiple_py_versions-0.1.0-py2.py3-none-any.whl`
* `.venv3.10.10/bin/poetry_multiple_py_versions` works ✅
* maybe because typer tests the package on all [python versions](https://github.com/tiangolo/typer/blob/master/.github/workflows/test.yml#LL14C7-L15C69).
* now lets update main.py:15 from `def shoot():` to `def shoot() -> str | None:`
* `poetry build`
* `.venv3.7.16/bin/python -m pip install dist/poetry_multiple_py_versions-0.1.0-py2.py3-none-any.whl --force-reinstall`
* `.venv3.7.16/bin/poetry_multiple_py_versions` does not work ❌
    ```console
    $ .venv3.7.16/bin/poetry_multiple_py_versions
    Traceback (most recent call last):
    File ".venv3.7.16/bin/poetry_multiple_py_versions", line 5, in <module>
        from poetry_multiple_py_versions.main import app
    File "/home/ubuntu/dev/saurabh-glam/poetry-multiple-py-versions/.venv3.7.16/lib/python3.7/site-packages/poetry_multiple_py_versions/main.py", line 15, in <module>
        def shoot() -> str | None:
    TypeError: unsupported operand type(s) for |: 'type' and 'NoneType'
    ubuntu@ip-172-31-17-152:~/dev/saurabh-glam/poetry-multiple-py-versions
    ```