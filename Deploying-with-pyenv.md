Setting up pyenv on a production server is exactly the same as in development.
Some considerations for a hypothetical deployment strategy:

* It is suggested that there is a single user for deployment, e.g. "app" user
* `PYENV_ROOT` is at the default location: `~app/.pyenv`
* Ruby versions are either installed or symlinked to `~app/.pyenv/versions`
* pyenv version 0.2 or greater is recommended.

Users of Capistrano may find these projects useful:

* [capistrano-pyenv](https://github.com/yyuu/capistrano-pyenv)

## Ensure consistent PATH for processes

Interactive, non-interactive shells, cron jobs, and similar processes for the
"app" user all must ensure that pyenv is present in the PATH:

    export PATH=~/.pyenv/shims:~/.pyenv/bin:"$PATH"
