See [[Authoring plugins]] for instructions on how to write new commands for
pyenv or hook into its functionality.

A plugin can be installed by dropping it in as a sub-directory of
`$PYENV_ROOT/plugins`, or it can be located elsewhere on the system as long as
`pyenv-*` executables are placed in the `$PATH` and hooks are installed
accordingly somewhere in `$PYENV_HOOK_PATH`.

## Official plugins

* [virtualenv] - the standard way to manage virtualenv with pyenv (formerly as known as [python-virtualenv](https://github.com/pyenv/python-virtualenv))
* [virtualenvwrapper](https://github.com/pyenv/pyenv-virtualenvwrapper) - allow you to play pyenv with virtualenvwrapper
* [pip-migrate] - Migrate pip packages from a Python version to another
* [update](https://github.com/pyenv/pyenv-update) - Update pyenv and plugins
* [installer](https://github.com/pyenv/pyenv-installer) - This tools is used to install `pyenv` and friends
* [doctor](https://github.com/pyenv/pyenv-doctor) - Verify pyenv installation
* [ccache](https://github.com/pyenv/pyenv-ccache) - Make Python build faster, by leverage `ccache`.

[virtualenv]: https://github.com/pyenv/pyenv-virtualenv
[pip-migrate]: https://github.com/pyenv/pyenv-pip-migrate

## Community plugins
Thanks to the hard work of the community, there are numerous other pyenv plugins to extend functionality for other use cases.

These are not maintained or tested by the `pyenv` team, so use at your own risk!

* [implicit](https://github.com/concordusapps/pyenv-implict) - Allow pyenv to guess the python version from the program name.
* [alias](https://github.com/s1341/pyenv-alias) - Allows installation of python instances using user-supplied names. This allows multiple instances of the same python version to be installed.
* [alias-latest-patch-version](https://github.com/upside-services/pyenv-alias-latest-patch-version) - allows you to specify Major.minor version that maps to the latest patch release.
* [default-packages](https://github.com/jawshooah/pyenv-default-packages) - Installs a set of default packages any time you install a new version of python or create a new virtualenv
* [pip-update](https://github.com/massongit/pyenv-pip-update), [pip-upgrade](https://github.com/zyrikby/pyenv-pip-upgrade) - Update all libraries managed by pip or conda in multiple environments.
* [choice](https://github.com/fizista/pyenv-choice) - Allows you to choose which version of Python you will use for a given program name, if there are multiple versions of this program.
* [fix-version](https://github.com/sprout42/pyenv-fix-version) - Provides a `pyenv fix-version` command to try and fix up any missing library dependencies there may be for an installed python version.
* [link](https://github.com/real-yfprojects/pyenv-link) - Allows you to use arbitrary venvs with pyenv by linking them into your pyenv root.
* [virtualenv-migrate](https://github.com/ashwinvis/pyenv-virtualenv-migrate) - Combines the functionalities of pyenv's [virtualenv] and [pip-migrate] plugins to migrate virtualenvs en masse.