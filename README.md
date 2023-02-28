# poetry-multiple-py-versions

## setup 1:

* `pyenv install 3.7.16`
* `poetry env use /home/ubuntu/.pyenv/versions/3.7.16/bin/python`
* `poetry install`
* `poetry run poetry_multiple_py_versions` ✅


## setup 2:

* `pyenv install 3.10.10`
* update `pyproject.toml` from `python = "=3.7.16"` to `python = "=3.10.10"`
* `poetry env use /home/ubuntu/.pyenv/versions/3.10.10/bin/python`
* `poetry install`
* `poetry run poetry_multiple_py_versions` ✅