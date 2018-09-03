pyenv is a tool for simple Python version management.

To install pyenv, please refer to the [Readme](https://github.com/pyenv/pyenv/).

## Troubleshooting / FAQ

### Python scripts or shell scripts that use python keep failing

If you experience failure while executing a script that issues `python` command or executes another python script:
 - try executing the command again in the appropriate `pyenv shell`
 - check if the command is a python script or invokes a python script and fix the shebang to `#!/usr/bin/env python`
 
Such failures usually show up as:
  - incompatible python version, but you are certain that you have correct version installed
  - module not found but you are certain that the module is installed
  - the issue can be traced back to something related to `PYTHONPATH`

Also, see below for suggested build environment.

### Suggested build environment

pyenv will try its best to download and compile the wanted Python version,
but sometimes compilation fails because of unmet system dependencies, or
compilation succeeds but the new Python version exhibits weird failures at
runtime. The following instructions are our recommendations for a sane build
environment.

* **Mac OS X:**

  If you haven't done so, install Xcode Command Line Tools
  (`xcode-select --install`) and [Homebrew](http://brew.sh/). Then:

```sh
# optional, but recommended:
brew install openssl readline sqlite3 xz zlib
```

* **Ubuntu/Debian/Mint:**

```sh
apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev
```

* **CentOS/Fedora 21 and below:**

FIXME: you may need to install `xz` to build some CPython version

```sh
yum install gcc zlib-devel bzip2 bzip2-devel readline-devel sqlite sqlite-devel openssl-devel tk-devel libffi-devel
```

* **Fedora 22 and above:**

FIXME: you may need to install `xz` to build some CPython version

```sh
dnf install -y gcc zlib-devel bzip2 bzip2-devel readline-devel sqlite sqlite-devel openssl-devel tk-devel libffi-devel
```

* **openSUSE:**

FIXME: you may need to install `xz` to build some CPython version

```sh
zypper install gcc automake openssl-devel ncurses-devel readline-devel zlib-devel tk-devel
```

* **Arch Linux:**

FIXME: you may need to install `xz` to build some CPython version

```sh
pacman -S base-devel openssl zlib
```

* **Solus:**

```
sudo eopkg it -c system.devel
sudo eopkg install git gcc make zlib-devel bzip2-devel readline-devel sqlite3-devel openssl-devel tk-devel
```

* **Linuxbrew:**

```sh
brew install bzip2 openssl readline sqlite xz
```


See also [Common build problems](https://github.com/pyenv/pyenv/wiki/Common-build-problems) for further information.

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
git clone https://github.com/pyenv/pyenv-doctor.git "$(pyenv root)/plugins/pyenv-doctor"
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

### Debugging pyenv

The `PYENV_DEBUG` is the environment variable to debug logging in pyenv. You can try to enable debug logging by setting something in the environment variable like `PYENV_DEBUG=1 pyenv versions`.

### How to build CPython with Framework support on OS X

Some of 3rd party tool like [PyInstaller](https://github.com/pyinstaller/pyinstaller) might require CPython installation built with `--enable-framework`. You can build CPython with shared library as follows.

```sh
$ env PYTHON_CONFIGURE_OPTS="--enable-framework" pyenv install 3.5.0
```

### How to build CPython with `--enable-shared`

Some of 3rd party tool like [PyInstaller](https://github.com/pyinstaller/pyinstaller) might require CPython installation built with `--enable-shared`. You can build CPython with shared library as follows.

```sh
$ env PYTHON_CONFIGURE_OPTS="--enable-shared" pyenv install 3.5.0
```

Since pyenv (precisely, python-build) will build CPython with configuring RPATH, you don't have to set `LD_LIBRARY_PATH` to specify library path on GNU/Linux.
