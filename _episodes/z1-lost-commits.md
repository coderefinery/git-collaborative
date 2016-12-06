---
layout: episode
title: "Unsorted: Lost commits"
teaching: 0
exercises: 0
questions:
  - "Sure we need this here?"
objectives:
  - "This is one objective of this episode."
---

## Detached head

- Typically `HEAD` points to a branch
- But you can make it point directly to a commit
- This is the detached `HEAD`

```shell
$ git checkout <hash>  # switch directly to a commit
```

- You can commit from there but what happens when you switch back to some branch?
- What happens to the commits?

---

## Lost commits

- You can recover lost commits with `git reflog`
- `git reflog` keeps a log with references (hashes)
- Try it, one day you will need it

---

## "Deleted" commits

- `git reset --hard` does not by itself delete commits
- It only moves the branch pointer back
- Commits move branch pointers forward, reset moves it back
- You can recover "deleted" commits with `git reflog`
- Unless the garbage collector has removed them already (more about it next slide)

---

## Orphaned commits

- Sometimes you want to get rid of orphaned/stale commits

```shell
$ git gc # run the garbage collector
```

- But be careful: today's garbage might be tomorrow's gold
- GitHub runs `git gc` on a periodic basis
