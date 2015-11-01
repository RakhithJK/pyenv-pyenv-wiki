## Requirements:

* Ubuntu/Debian: 
    ```
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev
    ``` 

* Fedora/CentOS: 
    `yum install zlib-devel bzip2 bzip2-devel readline-devel sqlite sqlite-devel openssl-devel`

* Mac: 
    ```bash brew install readline; brew link readline; pyenv install 2.7.5```


**NOTE**: `libssl-dev` is required when compiling Python, installing `libssl-dev` will actually install `zlib1g-dev`, which leads to uninstall and re-install Python versions (installed before installing `libssl-dev`). On Redhat and derivatives the package is named `openssl-devel`.


## Removing a python version

    rm -rf ~/.pyenv/versions/2.7.5

## Installing a 32 bit python on 64 bit Mac OS X (this will *not* work on Linux)

    CONFIGURE_OPTS="--with-arch=i386" CFLAGS="-arch i386" LDFLAGS="-arch i386" python-build options

## Installing a system-wide Python
If you want to install a Python interpreter that's available to all users and system scripts (no pyenv), use `/usr/local/` as the install path. For example:

    sudo python-build 3.3.2 /usr/local/

## Make your pythons a little faster
You can set your CFLAGS to accepted safe values to help get a little more speed.

    CFLAGS='-g -O2'

comment: why "-g". Will not it make things slower?.

## Build failed - bad interpreter: Permission denied

If you encounter this error while installing python and your server is a VPS, the **/tmp** directory where python-build download and compile the packages is probably mounted as **noexec**. You can check with your hosting provider if wether they provide a way to bypass this protection.

If the answer is no, just set the **$TMPDIR** environment variable to wherever you have a write + execution rights. For example:

    export TMPDIR="$HOME/src"

Please note you'll have to do it every time you'll want to install a new version of python unless you write this command in your `~/.bashrc`.

## Build failed

If you've got something like that:

```
$ pyenv install 2.7.5
Downloading http://pyyaml.org/download/libyaml/yaml-0.1.4.tar.gz...
Installing yaml-0.1.4...

BUILD FAILED
```

Please, be sure to have "make" installed (```$ sudo apt-get install make```). On Ubuntu Server, by default, it doesn't.

## Build failed: "ERROR: The Python zlib extension was not compiled. Missing the zlib?"

```
Installing Python-2.7.7...

ERROR: The Python zlib extension was not compiled. Missing the zlib?

Please consult to the Wiki page to fix the problem.
https://github.com/yyuu/pyenv/wiki/Common-build-problems

BUILD FAILED
```

* On Mac OS X 10.9 and 10.10 you may need to set the CFLAGS environment variable when installing a new version in order for configure to find the zlib headers (XCode command line tools must be installed first):
    ```
    CFLAGS="-I$(xcrun --show-sdk-path)/usr/include" pyenv install -v 2.7.7
    ```

* Alternatively, try reinstalling XCode command line tools for your OS (especially if you just upgraded your OS)
    ```
    xcode-select --install
    ```
## ERROR: The Python ssl extension was not compiled. Missing the OpenSSL lib?

* If you have homebrew openssl and pyenv installed, you may need to tell the compiler where the openssl package is located:
```
CFLAGS="-I$(brew --prefix openssl)/include" \
LDFLAGS="-L$(brew --prefix openssl)/lib" \
pyenv install -v 3.4.3
```
* On FreeBSD 10-RELEASE and 11-CURRENT, you may need to recompile ``security/openssl`` without SSLv2 support. (See [#464](https://github.com/yyuu/pyenv/issues/464#issuecomment-152821922)).

## python-build: definition not found

To update your python-build definitions:

If you have python-build installed as an pyenv plugin:
    
    $ cd ~/.pyenv/plugins/python-build && git pull