## Requirements:

* Ubuntu/Debian: 

```sh
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils
```

* Fedora/CentOS/RHEL:

FIXME: you may need to install `xz` to build some CPython version

```sh
yum install zlib-devel bzip2 bzip2-devel readline-devel sqlite sqlite-devel openssl-devel
```

* Mac OS X:

```sh
brew install readline xz
```

**NOTE**: `libssl-dev` is required when compiling Python, installing `libssl-dev` will actually install `zlib1g-dev`, which leads to uninstall and re-install Python versions (installed before installing `libssl-dev`). On Redhat and derivatives the package is named `openssl-devel`.

## Removing a python version

```sh
rm -rf ~/.pyenv/versions/2.7.5
```

## Installing a 32 bit python on 64 bit Mac OS X (this will *not* work on Linux)

```sh
CONFIGURE_OPTS="--with-arch=i386" CFLAGS="-arch i386" LDFLAGS="-arch i386" python-build options
```

## Installing a system-wide Python
If you want to install a Python interpreter that's available to all users and system scripts (no pyenv), use `/usr/local/` as the install path. For example:

```sh
sudo python-build 3.3.2 /usr/local/
```

## Make your pythons a little faster
You can set your CFLAGS to accepted safe values to help get a little more speed.

```sh
CFLAGS='-O2'
```

## Build failed - bad interpreter: Permission denied

If you encounter this error while installing python and your server is a VPS, the **/tmp** directory where python-build download and compile the packages is probably mounted as **noexec**. You can check with your hosting provider if wether they provide a way to bypass this protection.

If the answer is no, just set the **$TMPDIR** environment variable to wherever you have a write + execution rights. For example:

```sh
export TMPDIR="$HOME/src"
```

Please note you'll have to do it every time you'll want to install a new version of python unless you write this command in your `~/.bashrc`.

## Build failed

If you've got something like that:

```sh
$ pyenv install 2.7.5
Downloading http://pyyaml.org/download/libyaml/yaml-0.1.4.tar.gz...
Installing yaml-0.1.4...

BUILD FAILED
```

Please, be sure to have "make" installed (```$ sudo apt-get install make```). On Ubuntu Server, by default, it doesn't.

## Build failed: "ERROR: The Python zlib extension was not compiled. Missing the zlib?"

```sh
Installing Python-2.7.7...

ERROR: The Python zlib extension was not compiled. Missing the zlib?

Please consult to the Wiki page to fix the problem.
https://github.com/yyuu/pyenv/wiki/Common-build-problems

BUILD FAILED
```

* On Mac OS X 10.9, 10.10 and 10.11 you may need to set the CFLAGS environment variable when installing a new version in order for configure to find the zlib headers (XCode command line tools must be installed first):

```sh
CFLAGS="-I$(xcrun --show-sdk-path)/usr/include" pyenv install -v 2.7.7
```

* Alternatively, try reinstalling XCode command line tools for your OS (especially if you just upgraded your OS)

```sh
xcode-select --install
```

## ERROR: The Python ssl extension was not compiled. Missing the OpenSSL lib?

* If you have homebrew openssl and pyenv installed, you may need to tell the compiler where the openssl package is located:

```sh
CFLAGS="-I$(brew --prefix openssl)/include" \
LDFLAGS="-L$(brew --prefix openssl)/lib" \
pyenv install -v 3.4.3
```

or (checked on RHEL6):

```sh
CFLAGS=-I/usr/include/openssl \
LDFLAGS=-L/usr/lib64 \
pyenv install -v 3.4.3
```

* Alternatively, if you installed openssl with macports, use the following paths:

```sh
CFLAGS="-I/opt/local/include/" \
LDFLAGS="-L/opt/local/lib/" \
pyenv install -v 3.4.3
```

* On FreeBSD 10-RELEASE and 11-CURRENT, you may need to recompile ``security/openssl`` without SSLv2 support. (See [#464](https://github.com/yyuu/pyenv/issues/464#issuecomment-152821922)).

## python-build: definition not found

To update your python-build definitions:

If you have python-build installed as an pyenv plugin:
    
```sh
$ cd ~/.pyenv/plugins/python-build && git pull
```
