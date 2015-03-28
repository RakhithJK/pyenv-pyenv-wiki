pyenv is a tool for simple Python version management.

To install pyenv, please refer to the [Readme][install].

## Troubleshooting / FAQ

### How is this better than pythonbrew and pythonz?

See [[Why pyenv?]]

### What is allowed in a `.python-version` file?

The string read from a `.python-version` file must match the name of an existing
directory in `~/.pyenv/versions/`. You can see the list of installed Python
versions with `pyenv versions`.

If you're using [python-build][], typically this will be one of [its Python version
names][versions].

Other version managers might allow fuzzy version matching on the string read
from `.python-version` file, e.g. they might allow "3.3" (without patch suffix)
to match the latest Python 3.3 release. **pyenv will not support this**, because
such behavior is unpredictable and therefore harmful.

### How to verify that I have set up pyenv correctly?

1.  Check that `pyenv` is in your PATH:

    ```sh
    which pyenv
    ```

2.  Check that pyenv's shims directory is in PATH:

    ```sh
    echo $PATH | grep --color=auto "$(pyenv root)/shims"
    ```

    If not, see the [`pyenv init` step][init] in installation instructions.

### pyenv is installed but things just aren't working for me!

Please search [existing issues][issues] and open a new one if you can't find any answers. Here's a script that dumps information about your current environment; you can use [Gist][] to paste it online and share the URL to it in your bug report:

```sh
git clone https://github.com/yyuu/pyenv-doctor.git "$(pyenv root)/plugins/pyenv-doctor"
pyenv doctor
```

### Which shell startup file do I put pyenv config in?

Typically it's one of the following:

* bash: `~/.bash_profile`
* zsh: `~/.zshrc`
* ksh: `~/.kshrc`
* other: `~/.profile`

With bash on Ubuntu, you probably already have a `~/.profile`. In that case you
should add pyenv config there instead of creating a `~/.bash_profile`. However,
since this file is read only once per desktop login, you may achieve quicker
results by adding pyenv to `~/.bashrc` instead.

See [[Unix shell initialization]] for more info about how config files get
loaded.