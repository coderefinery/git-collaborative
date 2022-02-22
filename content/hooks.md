# Hooks

```{objectives}
- Learn how to couple scripts to Git repository events.
```

```{instructor-note}
- 10 min teaching/demonstration
```


Sometimes you would like Git events (commits, pushes, etc.) to **trigger scripts**
which take care of some tasks.  **Hooks are scripts that are executed
before/after certain Git events**.  They can be used to enforce nearly any kind of
policy for your project.  There are client-side and server-side hooks.


## Client-side hooks

You can find and edit them here:

```console
$ ls -l .git/hooks/
```

- `pre-commit`: before commit message editor (example: make sure tests pass)
- `prepare-commit-msg`: before commit message editor (example: modify default messages)
- `commit-msg`: after commit message editor (example: validate commit message pattern)
- `post-commit`: after commit process (example: notification)
- `pre-rebase`: before rebase anything (example: disallow rebasing published commits)
- `post-rewrite`: run by commands that rewrite commits
- `post-checkout`: after successful `git checkout` (example: generating documentation)
- `post-merge`: after successful merge
- `pre-push`: runs during `git push` before any objects have been transferred
- `pre-auto-gc`: invoked just before the garbage collection takes place

See also <https://pre-commit.com>,
a framework for managing and maintaining multi-language pre-commit hooks.

Example for a `pre-commit` hook which checks whether a Python code is [PEP 8](https://www.python.org/dev/peps/pep-0008/)-compliant
using [pycodestyle](http://pycodestyle.pycqa.org):

```console
#!/usr/bin/env bash

# ignore errors due to too long lines
pycodestyle --ignore=E501 myproject/
```


## Server-side hooks

You can typically edit them through a web interface on GitHub/GitLab.

- `pre-receive`: before accepting any references
- `update`: like `pre-receive` but runs once per pushed branch
- `post-receive`: after entire process is completed

- Typical use:
    - Maintenance work
    - Automated tests
    - Refreshing of documentation/website
    - Sanity checks
    - Code style checks
    - Email notification
    - Rebuilding software packages


## Actions, workflows, and continuous integration services

GitHub and GitLab let you define workflows/actions/recipes which are triggered
by e.g. `git push` or by a release (tag creation).  They can be customized and
almost any automation you can think of becomes possible.

These services use hooks under the hood. These days, project are more likely to
use these higher-level services rather than Git hooks directly.

You can read more about these services here:
- [GitHub Actions](https://docs.github.com/en/actions)
- [GitLab CI](https://docs.gitlab.com/ee/ci/)

In our projects we use these services to:
- Build websites
- Build documentation
- Run tests
- Create containers
- Package and upload packages
- Spellchecking
