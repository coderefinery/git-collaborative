---
layout: episode
title: "Hooks"
teaching: 5
exercises: 0
questions:
  - "How can we automate tasks depending on events in the Git repository?"
objectives:
  - "Learn how to couple scripts to Git repository events."
---

## Hooks

Sometimes you would like Git events (commits, pushes, etc.) to trigger scripts which take care of some tasks.

Hooks are scripts that are executed before/after certain events.

You can find and edit them here:

```shell
$ ls -l .git/hooks/
```

They can be used to enforce nearly any kind of policy for your project.

There are client-side and server-side hooks.


### Client-side hooks

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


### Server-side hooks

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
