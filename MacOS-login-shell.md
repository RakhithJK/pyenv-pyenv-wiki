# Configure the terminal to run your shell as a login shell

The stock shell configuration examples for Pyenv 2.0.0-2.2.5 for MacOS assume that the shell in the terminal runs as a login shell.

## Check if the current shell is a login shell

* Bash:

  ```bash
  shopt -q login_shell && echo 'Login shell' || echo 'Not login shell'
  ```
* Zsh:

  ```zsh
  if [[ -o login ]]; then echo "login shell"; else echo "not login shell"; fi
  ```

* Fish:

  ```fish
  status --is-login; and echo "login shell"; or echo "not login shell"
  ```

## Set the shell to run as a login shell

There are two possible ways here.

### Set the shell as your login shell (recommended)

* `System Preferences` > `Users and groups` > Open the padlock to allow changes >
Right click on the corresponding user's name > `Advanced options` > Select the
shell from the dropdown list next to `Login shell`

* Then, in the Terminal app: `Preferences` > `General` > `Open shells with` > `Predefined login shell`

### Configure the terminal to explicitly run a shell as a login shell

* In the Terminal app: `Preferences` > `General` > `Open shells with` > `Command (full path)`

  * Zsh: `/bin/zsh --login`
  * Bash: `/bin/bash -l`
  * Fish: `<path to fish executable> --login`
