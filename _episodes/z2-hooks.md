---
layout: episode
title: "Hooks"
teaching: 0
exercises: 0
questions:
  - "How can we automate tasks depending on events in the Git repository?"
objectives:
  - "This is one objective of this episode."
  - "This is another objective of this episode."
  - "Yet another objective."
  - "And not to forget this objective."
keypoints:
  - "This is an important key point."
  - "Another important key point."
  - "One more key point."
---

## Hooks

```shell
$ ls -l .git/hooks/
```

- Hooks are scripts that are executed before/after certain events
- They can be used to enforce nearly any kind of policy for your project
- There are client-side and server-side hooks

---

### Client-side hooks

- `pre-commit`: before commit message editor (example: make sure tests run)
- `prepare-commit-msg`: before commit message editor (example: modify default messages)
- `commit-msg`: after commit message editor (example: validate commit message pattern)
- `post-commit`: after commit process (example: notification)
- `pre-rebase`: before rebase anything (example: disallow rebasing published commits)
- `post-rewrite`: run by commands that rewrite commits
- `post-checkout`: after successful `git checkout` (example: generating documentation)
- `post-merge`: after successful merge
- `pre-push`: runs during `git push` before any objects have been transferred
- `pre-auto-gc`: invoked just before the garbage collection takes place

---

### Server-side hooks

- `pre-receive`: before accepting any references
- `update`: like `pre-receive` but runs once per pushed branch
- `post-receive`: after entire process is completed

- Typical use:
    - Maintenance work
    - Refreshing of documentation/website
    - Sanity checks
    - Code style checks
    - Email notification
    - Rebuilding software packages
name: inverse
layout: true
class: center, middle, inverse
