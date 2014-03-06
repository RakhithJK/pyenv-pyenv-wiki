### pyenv _does..._

* Let you **change the global Python version** on a per-user basis.
* Provide support for **per-project Python versions**.
* Allow you to **override the Python version** with an environment
  variable.
* Search commands from **multiple versions of Python at a time**.
  This may be helpful to test across Python versions with [tox](http://pypi.python.org/pypi/tox).

### In contrast with pythonbrew and pythonz, pyenv _does not..._

* **Depend on Python itself.** pyenv was made from pure shell scripts.
    There is no bootstrap problem of Python.
* **Need to be loaded into your shell.** Instead, pyenv's shim
    approach works by adding a directory to your `$PATH`.
* **Manage virtualenv.** Of course, you can create [virtualenv](http://pypi.python.org/pypi/virtualenv)
    yourself, or [pyenv-virtualenv](https://github.com/yyuu/pyenv-virtualenv)
    to automate the process.
