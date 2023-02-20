The command to build with PGO in [Building for maximum performance -- Python-Build README](https://github.com/pyenv/pyenv/blob/master/plugins/python-build/README.md#building-for-maximum-performance) doesn't directly translate to MacOS because as of this writing, Apple's latest CLang (14.0.0) doesn't support `-march=native`.

To use it, you can compile CPython with CLang 15 from Homebrew's LLVM (`brew install llvm`).

Note however that this is not an officially supported setup. Homebrew's LLVM is known to break the build for some combinations of CPython, MacOS and XCode versions and there might be other unexpected breakages or slight incompatibilities. This was also not tested when compiling for x86_64 with Apple Silicon. Use at your own risk!

```
env PATH="/opt/homebrew/opt/llvm/bin:$PATH" PYTHON_CONFIGURE_OPTS='--enable-optimizations --with-lto' PYTHON_CFLAGS='-march=native -mtune=native' pyenv install 3.10
```