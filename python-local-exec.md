The `python-local-exec` command is **deprecated** as of pyenv 0.2.0 and will be removed in the next major release.

## What is python-local-exec?

`python-local-exec` was introduced in pyenv 0.1.0 as a drop-in replacement for the standard Python shebang line:

    #!/usr/bin/env python-local-exec

With `python-local-exec` in place, scripts in an application with a `.python-version` or `.pyenv-version` file use the application-specific Python version, regardless of what directory they're run from. This is useful for running scripts in cron jobs without needing to `cd` into the application first.

## Why is it deprecated?

The functionality provided by `python-local-exec` has been rolled into the standard `python` shim provided by pyenv. 

Now, when you run scripts or binstubs in an application with a `.python-version` file, pyenv will automatically use the application's specified Python version, regardless of what directory they're run from.

To upgrade, first ensure your team and its servers are on pyenv 0.2.0 or later. Adjust your shebangs back to:

    #!/usr/bin/env python

Then be sure to regenerate your shims with `pyenv rehash`.

## Can I silence the warning message?

Set `PYENV_SILENCE_WARNINGS=1` in your environment to silence the `python-local-exec` deprecation warning message.
