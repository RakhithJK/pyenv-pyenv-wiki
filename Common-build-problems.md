**First of all, make sure you have installed Python's dependencies and build tools** as per https://github.com/pyenv/pyenv/wiki#suggested-build-environment , before any further troubleshooting.

**Open the build log** (the path to it is printed after the "BUILD FAILED" message) **and look for any error messages in it** (they are usually marked with the word "error"). If there are many error messages, the earliest one typically points to the root cause.

**If your error message is not listed in the below table of contents** (TOC), **try searching this page for the message's parts** (best for parts that would likely remain the same between distributions and library versions). If multiple different error messages have the same cause, we list them in the corresponding section's text rather than in the TOC.

- [Prerequisites](#prerequisites)
- [Removing a python version manually](#removing-a-python-version-manually)
- [Installing a 32 bit python on 64 bit Mac OS X (this will *not* work on Linux)](#installing-a-32-bit-python-on-64-bit-mac-os-x-this-will-not-work-on-linux)
- [Installing a system-wide Python](#installing-a-system-wide-python)
- [Build failed - bad interpreter: Permission denied](#build-failed-bad-interpreter-permission-denied)
- [Build failed](#build-failed)
- [Build failed: "ERROR: The Python zlib extension was not compiled. Missing the zlib?"](#build-failed-error-the-python-zlib-extension-was-not-compiled-missing-the-zlib)
- [Build failed: Resource temporarily unavailable](#build-failed-resource-temporarily-unavailable)
- [ERROR: The Python ssl extension was not compiled. Missing the OpenSSL lib?](#error-the-python-ssl-extension-was-not-compiled-missing-the-openssl-lib)
- [python-build: definition not found](#python-build-definition-not-found)
- [macOS: "ld: symbol(s) not found for architecture x86_64" (#1245)](#macos-ld-symbol-s-not-found-for-architecture-x86-64-1245)
- [Python cannot find a dependent dynamic library even though it's installed](#python-cannot-find-a-dependent-dynamic-library-even-though-its-installed)
- ["python-build: definition not found" or another new feature missing even though you have a new enough Pyenv](#python-build-definition-not-found-or-another-new-feature-missing-even-though-you-have-a-new-enough-pyenv)
- ["configure: error: internal configure error for the platform triplet, please file a bug report" in MacOS](#configure-error-internal-configure-error-for-the-platform-triplet-please-file-a-bug-report-in-macos)
- [Keg-only Homebrew packages are forcibly linked / added to PATH](#keg-only-homebrew-packages-are-forcibly-linked--added-to-path)
- [On Apple Silicon, when building for ARM64, a dependency is present in x64 Homebrew but not arm64 Homebrew](#on-apple-silicon-when-building-for-arm64-a-dependency-is-present-in-x64-homebrew-but-not-arm64-homebrew)
## Prerequisites

Below are some alternative packages that are not in the recommended set and should generally only be considered when there are special needs and/or problems with those in it.
<!- Updates to the recommended set should go on the above link rather than here! ->

* Ubuntu/Debian: 

    * Alternative to libreadline-dev:

        ```sh
        sudo apt install libedit-dev
        ```


    * An [inferior alternative](https://github.com/docker-library/python/issues/235) to `libncursesw5`:

        ```sh
        sudo apt install libncurses5-dev
        ```


* Fedora/CentOS/RHEL(aws ec2):

    * Alternative to openssl-devel:

        * If you need OpenSSL 1.0:
    
            ```sh
            sudo yum install compat-openssl10-devel --allowerasing
            ```

        * If you need OpenSSL 1.1:

            ```sh
            sudo yum install openssl11-devel --allowerasing
            ```

    If your `yum` doesn't support the `--allowerasing` flag, use `yum swap` instead, e.g.:

    ```sh
    sudo yum swap openssl-devel openssl11-devel
    ```


* Arch and derivatives

    Installing an older version of ncurses, `ncurses5`, requires an [AUR Helper](https://wiki.archlinux.org/index.php/AUR_helpers) to install. If using [YAY](https://aur.archlinux.org/packages/yay/):

    ```sh
    yay -S ncurses5-compat-libs 
    ```

* macOS 14+ - Apple Silicon

    Installing versions of Python `>=3.12.1` on some machines may require `ncurses`, which seem to be missing. Install it with:

    ```sh
    brew install ncurses 
    ```

## Removing a python version manually

```sh
rm -rf ~/.pyenv/versions/"X.Y.Z"
```
Where "X.Y.Z" is the version that you want to remove. To list installed versions:

```sh
pyenv versions
```

## Installing a 32 bit python on 64 bit Mac OS X (this will *not* work on Linux)

```sh
CONFIGURE_OPTS="-with-arch=i386" CFLAGS="-arch i386" LDFLAGS="-arch i386" python-build options
```

## Installing a system-wide Python
If you want to install a Python interpreter that's available to all users and system scripts (no pyenv), use `/usr/local/` as the install path. For example:

```sh
sudo python-build 3.3.2 /usr/local/
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

Please, make sure that "make" is installed (```$ sudo apt-get install make```). In Ubuntu Server, by default, it isn't.

## Build failed: "ERROR: The Python zlib extension was not compiled. Missing the zlib?"

```sh
Installing Python-2.7.7...

ERROR: The Python zlib extension was not compiled. Missing the zlib?

Please consult to the Wiki page to fix the problem.
https://github.com/pyenv/pyenv/wiki/Common-build-problems

BUILD FAILED
```

* On Mac OS X 10.9, 10.10, 10.11 and 10.13 you may need to set the CFLAGS environment variable when installing a new version in order for configure to find the zlib headers (XCode command line tools must be installed first):

```sh
CPPFLAGS="-I$(xcrun -show-sdk-path)/usr/include" pyenv install -v 2.7.7
```

* If you installed zlib with Homebrew, you can set the CPPFLAGS environment variable:
```sh
CPPFLAGS="-I$(brew --prefix zlib)/include" pyenv install -v 3.7.0
```

* Alternatively, try reinstalling XCode command line tools for your OS

If you experience both issues with openssl and zlib, you can specify both search paths as a compiler flag:

```sh
CPPFLAGS="-I$(brew --prefix openssl)/include -I$(xcrun -show-sdk-path)/usr/include" LDFLAGS="-L$(brew --prefix openssl)/lib"
```

If you experience issues with readline, you can also specify this as a compiler flag:

```sh
CPPFLAGS="-I$(brew --prefix openssl)/include -I$(brew --prefix readline)/include -I$(xcrun -show-sdk-path)/usr/include" LDFLAGS="-L$(brew --prefix openssl)/lib -L$(brew --prefix readline)/lib"
```

If you are using macOS 10.14.6 with XCode 10.3, add the following:

```sh
SDKROOT=${XCODE_ROOT}/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.14.sdk \
MACOSX_DEPLOYMENT_TARGET=10.14
```

If you are using Ubuntu/Debian, you need the following packages:
```sh
sudo apt install zlib1g zlib1g-dev libssl-dev libbz2-dev libsqlite3-dev
```

## Build failed: Resource temporarily unavailable
If you see the string "resource temporarily unavailable" (often after "fork: "), then you may be on a shared host or other machine with low resource limits. Try running only a single job at a time to reduce resource usage:
```sh
MAKE_OPTS='-j 1' pyenv install 3.12.1
```

## ERROR: The Python ssl extension was not compiled. Missing the OpenSSL lib?

### 0. First, check
* if you actually have OpenSSL and its headers installed (and for the right architecture and ecosystem if there are more than one at your machine)
  * Ubuntu: `sudo apt install libssl-dev`
  * Fedora: `sudo dnf install openssl-devel`
* if the problem is resolved by upgrading Pyenv to the latest release and to the head version

### 1. **OpenSSL is installed to an uncommon location.**

Pass the location of its headers and libraries explicitly:
(the openssl folder can be found by running `openssl version -d`)

```sh
CPPFLAGS="-I<openssl install prefix>/include" \
LDFLAGS="-L<openssl install prefix>/lib" \
pyenv install -v <python version>
```

or, alternatively, [for Python 3.7+](https://bugs.python.org/issue32598), instead of `CPPFLAGS` and `LDFLAGS`:

```sh
CONFIGURE_OPTS="-with-openssl=<openssl install prefix>"
```

or

```sh
LDFLAGS="-Wl,-rpath,<openssl install prefix>/lib" \
CONFIGURE_OPTS="-with-openssl=<openssl install prefix>" \
pyenv install -v <python version>
```

E.g. (invocations that worked for various people):

* RHEL6:

    ```sh
    CPPFLAGS=-I/usr/include/openssl \
    LDFLAGS=-L/usr/lib64 \
    pyenv install -v 3.4.3
    ```

* CentOS 7 with OpenSSL 1.1.1:

    ```sh
    CPPFLAGS="$(pkg-config --cflags openssl11)" \
    LDFLAGS="$(pkg-config --libs openssl11)" \
    pyenv install -v 3.10.6
    ```

* Arch Linux:

    ```sh
    LDFLAGS="-L/usr/lib/openssl-1.0" \
    CPPFLAGS="-I/usr/include/openssl-1.0" \
    pyenv install -v 3.4.3
    ```

* If you installed openssl with macports or homebrew:

    ```sh
    CPPFLAGS="-I/opt/local/include/" \
    LDFLAGS="-L/opt/local/lib/" \
    pyenv install -v 3.4.3
    ```

* On Ubuntu 14.04 on Dreamhost, an extra flag is required for Python 3.7+:
    * First, follow these instructions: https://help.dreamhost.com/hc/en-us/articles/360001435926-Installing-OpenSSL-locally-under-your-username
    * Then, run:
      ```sh
      CPPFLAGS=-I$HOME/openssl/include \
      LDFLAGS=-L$HOME/openssl/lib \
      SSH=$HOME/openssl
      pyenv install -v 3.7.2
      ```

### 2. **Your OpenSSL version is incompatible with the Python version you're trying to install**

Old Python versions (for CPython, <3.5.3 and <2.7.13) require OpenSSL 1.0 while newer systems provide 1.1, and vice versa.  
Note that OpenSSL 1.0 is EOL and by now practically unusable on the Internet due to using obsolete standards.

Install the right OpenSSL version, and point the build to its location as per above if needed.

E.g.:

* On Debian stretch and Ubuntu bionic, `libssl-dev` is OpenSSL 1.1.x, but support for that was only added in Python 2.7.13, 3.5.3 and 3.6.0.  To install earlier versions, you need to replace `libssl-dev` with `libssl1.0-dev`.

  ```sh
  sudo apt-get remove libssl-dev
  sudo apt-get update
  sudo apt-get install libssl1.0-dev
  ```

  https://github.com/pyenv/pyenv/issues/945#issuecomment-409627448 has a more complex workaround that preserves `libssl-dev`.

* On FreeBSD 10-RELEASE and 11-CURRENT, you may need to recompile ``security/openssl`` without SSLv2 support. (See [#464](https://github.com/yyuu/pyenv/issues/464#issuecomment-152821922)).

* On Debian Jessie, you can use backports to install OpenSSL 1.0.2: `sudo apt -t jessie-backports install openssl`


## python-build: definition not found

To update your python-build definitions:

If you have python-build installed as an pyenv plugin:
    
```sh
$ cd ~/.pyenv/plugins/python-build && git pull
```

## macOS: "ld: symbol(s) not found for architecture x86_64" (#1245)

From ([#1245](https://github.com/pyenv/pyenv/issues/1245)).

This may be caused by an incompatible version of `ar` bundled with brew-distributed binutils.
This is the reason why `binutils` is keg-only.

To fix, uninstall binutils `brew remove binutils`, or remove them from PATH, or execute the install command with `AR=/usr/bin/ar`.

## Python cannot find a dependent dynamic library even though it's installed

If you're getting messages like this:

```
libreadline.so.7: cannot open shared object file: No such file or directory
```

or

```
ImportError: dlopen(/Users/durand/.pyenv/versions/3.10.1/lib/python3.10/site-packages/scipy/linalg/_fblas.cpython-310-darwin.so, 2): Library not loaded: /opt/homebrew/opt/gcc/lib/gcc/11/libgfortran.5.dylib
  Referenced from: /Users/durand/.pyenv/versions/3.10.1/lib/python3.10/site-packages/scipy/linalg/_fblas.cpython-310-darwin.so
  Reason: image not found
```

but you do have the corresponding package installed.

**Check if the dynamic library's version you have installed is the same as what Python expects:**

```
$ ls /lib/libreadline.so*
/lib/libreadline.so  /lib/libreadline.so.8  /lib/libreadline.so.8.0
```

Beside build time, this can also happen for an already installed version if:

* You've installed a prebuilt version that was built for a different environment

    Many installation scripts for prebuilt versions give you a warning in such a case.

    * Replace the prebuilt version with a source one (usually, these are suffixed with `-src` if both a prebuilt and a source versions are provided); or
    * (not recommended, will make the system harder to maintain) Get or compile the right version of the library
        * it needs to be compiled for your system to avoid binary incompatibilies, so the best bets are either building from source or getting a binary from an official source for your distro

* You've updated a dependent library on your system to a version with a different library filename (generally, to a new major version) since the time you had compiled Python

    * The easiest way is to rebuild all affected Python installations against the new version of the library with `pyenv install <version> -force`
    * If this happens for a specific 3rd-party Python package, you need to rebuild just that package.
    * [There's a 3rd-party plugin](https://github.com/pyenv/pyenv/wiki/Plugins) that attempts to detect and do this automatically.

## "python-build: definition not found" or another new feature missing even though you have a new enough Pyenv

If your Pyenv is installed with Homebrew, check if you have a second, old Pyenv installed and earlier on `PATH`:

```
zsh % whence -a pyenv
pyenv
/Users/admin/.pyenv/bin/pyenv     <-- an extraneous Pyenv in /Users/admin/.pyenv
/usr/local/bin/pyenv

bash $ which -a pyenv
/Users/admin/.pyenv/bin/pyenv
/usr/local/bin/pyenv
```

If yes, [remove it](https://github.com/pyenv/pyenv#uninstalling-pyenv).

## "configure: error: internal configure error for the platform triplet, please file a bug report" in MacOS

```
checking for the platform triplet based on compiler characteristics... darwin
configure: error: internal configure error for the platform triplet, please file a bug report
```

This means that *the Python version you're installing doesn't support your MacOS and/or XCode version.* In particular:

* XCode 13.3+ is officially supported by CPython since 3.8.13 and 3.9.8. We use downstream patches to support it in some older versions, too, see ["Python versions with extended support" in the README](https://github.com/pyenv/pyenv#python-versions-with-extended-support).
* The ARM64 architecture is supported since 3.8.10 and 3.9.1

## Keg-only Homebrew packages are forcibly linked / added to PATH

Some keg-only (explanation is below) Homebrew packages are known to break Pyenv builds if forcibly linked/added to `PATH`.
Unlink/Remove them from your `PATH`.

Known error messages they cause:

* Homebrew `binutils` on `PATH`:
  * `configure: error: Unexpected output of 'arch' on OSX`
* Homebrew `llvm` on `PATH`:
  * `warning: pointer is missing a nullability type specifier`
  * `llvm-ar: error: libpython3.10.a: Invalid record`
* Homebrew `coreutils` only causes breakage if non-prefixed executables are added to `PATH`.

Some Homebrew packages are installed as "keg-only" -- i.e. their executables are not linked to `$(brew --prefix)/bin`.
This is typically done because then they would override stock MacOS software (the specific reason is mentioned in `brew info` output), causing breakages. The same happens if you manually add them to `PATH` as specified in their `brew info` output.

## On Apple Silicon, when building for ARM64, a dependency is present in x64 Homebrew but not arm64 Homebrew

Known errors and their resolutions:
* `dyld[88714]: symbol not found in flat namespace '_libintl_bindtextdomain'`, `__locale_textdomain in _localemodule.o ld: symbol(s) not found for architecture arm64`
  * Install `gettext` into the arm64 Homebrew
* `unsupported hash type blake2s`
* `ld: warning: ignoring file /usr/local/Cellar/<...>/libb2.dylib: found architecture 'x86_64', required architecture 'arm64'`
* `[ERROR] _blake2 failed to import: dlopen(<...>/_blake2.cpython-312-darwin.so, 0x0002): symbol not found in flat namespace '_blake2b_final'`
  * Install `libb2` into the arm64 Homebrew or uninstall it from the x64 Homebrew

Since x64's Homebrew is in `/usr/local`, it's always in the compiler's search path. We however prepend `/opt/homebrew` to the compiler's search path when compiling for arm64 (actually, when `brew` on `PATH` is pointing there).

So if a library is installed and linked in the x64 Homebrew but not in Arm64 Homebrew, the compiler still finds it, even if it's compiling for arm64. However, linking with it fails as it's for the wrong architecture.