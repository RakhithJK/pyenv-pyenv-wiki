## Requirements:

* Ubuntu/Debian: 

```sh
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
xz-utils tk-dev libffi-dev liblzma-dev
```
Alternative of libreadline-dev:
```sh
sudo apt install libedit-dev
```

* Fedora/CentOS/RHEL(aws ec2):

```sh
sudo yum install zlib-devel bzip2 bzip2-devel readline-devel sqlite sqlite-devel \
openssl-devel xz xz-devel libffi-devel
```
Alternative of openssl-devel:
```sh
sudo yum install compat-openssl10-devel --allowerasing
```

* openSUSE

```sh
zypper in zlib-devel bzip2 libbz2-devel readline-devel sqlite3 sqlite3-devel libopenssl-devel xz xz-devel
```

* Alpine

```sh
apk add libffi-dev ncurses-dev openssl-dev readline-dev tk-dev xz-dev zlib-dev
```

* macOS:

```sh
brew install readline xz
```

  When running Mojave or higher (10.14+) you will also [need to install the additional SDK headers](https://developer.apple.com/documentation/xcode_release_notes/xcode_10_release_notes#3035624) by downloading them from [Apple Developers](https://developer.apple.com/download/more/?q=Command%20Line%20Tools). You can also check under `/Library/Developer/CommandLineTools/Packages/` as some versions of Mac OS will have the `pkg` locally.

```sh
sudo installer -pkg /Library/Developer/CommandLineTools/Packages/macOS_SDK_headers_for_macOS_10.14.pkg -target /
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

If you encounter this error while installing python and your server is a VPS, the **/tmp** directory where python-build download and compile the packages is probably mounted as **noexec**. You can check with your hosting provider if whether they provide a way to bypass this protection.

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

* On Mac OS X 10.9, 10.10, 10.11 and 10.13 you may need to set the CFLAGS environment variable when installing a new version in order for configure to find the zlib headers (XCode command line tools must be installed first):

```sh
CFLAGS="-I$(xcrun --show-sdk-path)/usr/include" pyenv install -v 2.7.7
```

* If you installed zlib with Homebrew, you can set the CPPFLAGS environment variable:
```sh
CPPFLAGS="-I/usr/local/opt/zlib/include" pyenv install -v 3.7.0
```

* Alternatively, try reinstalling XCode command line tools for your OS and when running Mojave or higher (10.14+) you will also [need to install the additional SDK headers](https://developer.apple.com/documentation/xcode_release_notes/xcode_10_release_notes#3035624)

```sh
xcode-select --install
sudo installer -pkg /Library/Developer/CommandLineTools/Packages/macOS_SDK_headers_for_macOS_10.14.pkg -target /
```

If you experience both issues with openssl and zlib, you can specify both search paths as a compiler flag:

```sh
CFLAGS="-I$(brew --prefix openssl)/include -I$(xcrun --show-sdk-path)/usr/include" LDFLAGS="-L$(brew --prefix openssl)/lib"
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
Note: Python 3.7.0 will not compile on RHEL6 because it requires OpenSSL 1.0.2 or 1.1 and RHEL6 provides 1.0.1e

```
  Could not build the ssl module!
  Python requires an OpenSSL 1.0.2 or 1.1 compatible libssl with X509_VERIFY_PARAM_set1_host().
  LibreSSL 2.6.4 and earlier do not provide the necessary APIs, https://github.com/libressl-portable/portable/issues/381
```
(assuming, of course, you don't compile and install your own openssl... don't know if that's possible.)

or (checked on Arch Linux):

```sh
LDFLAGS="-L/usr/lib/openssl-1.0" \
CFLAGS="-I/usr/include/openssl-1.0" \
pyenv install -v 3.4.3
```

* Alternatively, if you installed openssl with macports, use the following paths:

```sh
CFLAGS="-I/opt/local/include/" \
LDFLAGS="-L/opt/local/lib/" \
pyenv install -v 3.4.3
```

* On FreeBSD 10-RELEASE and 11-CURRENT, you may need to recompile ``security/openssl`` without SSLv2 support. (See [#464](https://github.com/yyuu/pyenv/issues/464#issuecomment-152821922)).

* On Debian stretch (and Ubuntu bionic), libssl-dev is OpenSSL 1.1.x, but support for that was only added in Python 2.7.13, 3.5.3 and 3.6.0.  To install earlier versions, you need to replace `libssl-dev` with `libssl1.0-dev`.  This is being tracked in https://github.com/pyenv/pyenv/issues/945.

## python-build: definition not found

To update your python-build definitions:

If you have python-build installed as an pyenv plugin:
    
```sh
$ cd ~/.pyenv/plugins/python-build && git pull
```

## Mojave: missing "my_config.h"

Instead of `brew install mysql`, use `brew install mysql@5.7`. Then run:
```
export PATH="/usr/local/opt/mysql@5.7/bin:$PATH"
export LDFLAGS="-L/usr/local/opt/mysql@5.7/lib"
export CPPFLAGS="-I/usr/local/opt/mysql@5.7/include"
```