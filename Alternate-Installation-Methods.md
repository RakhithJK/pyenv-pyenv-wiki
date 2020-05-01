**Pyenv maintainers encourage you to install pyenv using either the [GitHub checkout method](https://github.com/pyenv/pyenv#basic-github-checkout) or via [Homebrew](https://github.com/pyenv/pyenv#homebrew-on-macos)**

However, there are other unofficial ways which you can install pyenv which are listed here. The following methods are not tested, maintained, or supported by the pyenv team:

### ZPlug plugin manager for Zsh
_suggested by @andypalmer in [#1598](https://github.com/pyenv/pyenv/pull/1598)_

Add the following line to your `.zshrc`:

```zplug "RiverGlide/zsh-pyenv", from:gitlab```

Then install the plugin

~~~ zsh
  $ source ~/.zshrc
  $ zplug install
~~~
The ZPlug plugin will install and initialise `pyenv` and add `pyenv` and `pyenv-install` to your `PATH`

#### Upgrading via ZPlug

To upgrade to the latest version of pyenv, update the ZPlug plugin:

```sh
$ zplug update RiverGlide/zsh-pyenv
```

