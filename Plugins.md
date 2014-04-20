See [[Authoring plugins]] for instructions on how to write new commands for
pyenv or hook into its functionality.

A plugin can be installed by dropping it in as a sub-directory of
`$PYENV_ROOT/plugins`, or it can be located elsewhere on the system as long as
`pyenv-*` executables are placed in the `$PATH` and hooks are installed
accordingly somewhere in `$PYENV_HOOK_PATH`.

## Approved plugins

This list is edited by pyenv maintainers.

* [virtualenv](https://github.com/yyuu/pyenv-virtualenv) - the standard way to manage virtualenv with pyenv (formerly as known as [python-virtualenv](https://github.com/yyuu/python-virtualenv))
* [virtualenvwrapper](https://github.com/yyuu/pyenv-virtualenvwrapper) - allow you to play pyenv with virtualenvwrapper
* [pip-rehash](https://github.com/yyuu/pyenv-pip-rehash) - Automatically run `pyenv rehash` every time you install a new package via pip
* [pip-migrate](https://github.com/yyuu/pyenv-pip-migrate) - Migrate pip packages from a Python version to another
* [update](https://github.com/yyuu/pyenv-update) - Update pyenv and plugins
* [installer](https://github.com/yyuu/pyenv-installer) - This tools is used to install `pyenv` and friends
* [doctor](https://github.com/yyuu/pyenv-doctor) - Verify pyenv installation
* [implicit](https://github.com/concordusapps/pyenv-implict) - Allow pyenv to guess the python version from the program name.
* [register](https://github.com/doloopwhile/pyenv-register) - Register system installed pythons to pyenv environment
* [ccache](https://github.com/yyuu/pyenv-ccache) - Make Python build faster, with using the leverage of `ccache`.
* [which-ext](https://github.com/yyuu/pyenv-which-ext) - Integrate pyenv and system commands. In particular the users of [Anaconda](https://store.continuum.io/cshop/anaconda/).