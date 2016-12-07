---
layout: episode
title: "Bonus: Interrupted work"
teaching: 20
exercises: 0
questions:
  - "How can Git help us to deal with interrupted work and context switching?"
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

## Frequent situation: interrupted work

- Your supervisor comes in and wants you to fix/commit something right now
- You are in the middle of a Jackson-Pollock-style debugging spree with 27 modified files
  and debugging prints everywhere
- What to do?
- What to do with uncommitted code?

---

## What to do with uncommitted code?

- Commit it
- But sometimes you do not want to, sometimes you want to hide your changes for 5 minutes,
  do something else, then bring them back and continue
- You can do this with `git stash`

```shell
$ git stash        # your modifications are stashed away
$ git stash pop    # your modifications are back
```

- It is a stack, you can stash several batches of modifications

```shell
$ git stash        # stash your debug code away
$ git commit       # fix something for the boss, commit it
$ git stash pop    # now you can continue
```
