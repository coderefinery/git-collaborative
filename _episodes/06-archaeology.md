---
layout: episode
title: "Archaeology with Git"
teaching: 15
exercises: 20
questions:
  - "How can we find out who introduced a line of code and when exactly?"
  - "How can we find out which commit broke a functionality?"
objectives:
  - "Quickly find a line of code, find out who introduced it, when, and why."
  - "Quickly find the commit that changed a behavior."
keypoints:
  - "`git bisect`, `git grep`, `git blame`, `git show` are a powerful combination when doing archaeology in a project."
---

## Inspecting commits

At any moment we can inspect individual commits with `git show`:

```shell
$ git show 47a00

commit 47a007d563adb03aeedbddeb483d3c6c0301c10a
Author: Radovan Bast <bast@users.noreply.github.com>
Date:   Wed Dec 7 17:27:04 2016 +0100

    completed the haiku

diff --git a/haiku.py b/haiku.py
index dd98a4c..a2f8de8 100644
--- a/haiku.py
+++ b/haiku.py
@@ -1,4 +1,9 @@
 def get_haiku():

     return '''On a branch ...
-                  by Kobayashi Issa'''
+                  by Kobayashi Issa
+
+              On a branch
+              floating downriver
+              floating downriver
+              a cricket, singing.'''
```

We see that the start of the hash is enough if it is unique.

Compare this with: [https://github.com/bast/git-rebase-squash-exercise/commit/47a007d563adb03aeedbddeb483d3c6c0301c10a](https://github.com/bast/git-rebase-squash-exercise/commit/47a007d563adb03aeedbddeb483d3c6c0301c10a)

---

## Grepping code

```shell
$ git grep -i fixme

densfit/df_vxc.F:!fixme call XC integrator
dirac/dirgrd.F:!FIXME: there is some issue with one-step - investigate later
dirac/dirrdn.F:!       fixme num grid report should be independent of DFT
dirac/dirscf.F:        !fixme: michal for InteRest
dirac/dirscf.F:          !fixme: michal for InteRest
dirac/dirscf.F:          !fixme: michal for InteRest
embedding/get_vemb_mat.F:!fixme irep can be < 0 in NONREL runs
eri/eri2out.F:!fixme
eri/eri2out.F:!fixme
eri/eri2out.F:!fixme
gp/gpkrmc.F:C     FIXME: dette ser ikke ud til at virke for complex groups.
interest/module_interest_hrr.f90:  !-- fixme --!
interest/module_interest_interface.F90:    !> fixme: contracted basis sets
```

- Greps entire repository below current directory
- Super fast

---

## Finding out who introduced a modification and when

- `git blame` is a fun and useful command to find out when a specific line got introduced and by whom
- This is important to judge the impact of a bug:
  - When was it introduced?
  - For how long has this bug been around?
  - Has this bug been released?
  - Has this buggy code been used by others?

```shell
$ git blame <filename>

faa4617a (Radovan Bast      2012-07-02 11:04:45 +0200) ! get the one electron Hamiltonian
e564cfe8 (A. J. Thorvaldsen 2012-12-25 00:59:21 +0100) H1 = 0*S
e564cfe8 (A. J. Thorvaldsen 2012-12-25 00:59:21 +0100) call mat_ensure_alloc(H1, only_alloc=.true.)
faa4617a (Radovan Bast      2012-07-02 11:04:45 +0200) call interface_scf_get_h1(H1)
faa4617a (Radovan Bast      2012-07-02 11:04:45 +0200)
e6cfa2cf (Radovan Bast      2012-03-01 10:06:39 +0100) ! get the two electron contribution (G) to Fock matrix
e564cfe8 (A. J. Thorvaldsen 2012-12-25 00:59:21 +0100) G = 0*S
e564cfe8 (A. J. Thorvaldsen 2012-12-25 00:59:21 +0100) call mat_ensure_alloc(G, only_alloc=.true.)
810e14d8 (Radovan Bast      2012-07-01 17:19:56 +0200) call interface_scf_get_g(D, G)
761d5c27 (Radovan Bast      2012-05-18 16:28:34 +0200)
e6cfa2cf (Radovan Bast      2012-03-01 10:06:39 +0100) ! Fock matrix F = H1 + G
761d5c27 (Radovan Bast      2012-05-18 16:28:34 +0200) F = H1 + G
```

- "Who the %&!@!!! wrote this crap?!?"
- "Oh, it was me. Nevermind :-)"

Who edited the source file for `git grep` and when and why?

- [https://github.com/git/git/blame/master/grep.c](https://github.com/git/git/blame/master/grep.c)

---

## Finding removed code

I remember there used to be a line containing the word "great idea".
Now it is gone:

```shell
$ git grep 'great idea'

[no output]
```

Sometimes also the log does not help because the commit messages are not helpful:

```shell
$ git log --oneline

2bc6228 even more ideas
bad55db more ideas
81191b5 this is not a useful commit message
baae463 initial layout
```

We can figure out when it disappeared:

```shell
$ git log -S 'great idea'

commit 81191b5407687745e7f36b8ae4d78b7ea2377ff0
Author: Radovan Bast <bast@users.noreply.github.com>
Date:   Tue Dec 13 22:27:06 2016 +0200

    this is not a useful commit message

commit baae463ee30ff07a2e346852817cbd2038bd05df
Author: Radovan Bast <bast@users.noreply.github.com>
Date:   Tue Dec 13 22:26:48 2016 +0200

    initial layout
```

Now let us have a look at that commit:

```shell
$ git show 81191b5

commit 81191b5407687745e7f36b8ae4d78b7ea2377ff0
Author: Radovan Bast <bast@users.noreply.github.com>
Date:   Tue Dec 13 22:27:06 2016 +0200

    this is not a useful commit message

diff --git a/ideas.txt b/ideas.txt
index a09af89..a657b2b 100644
--- a/ideas.txt
+++ b/ideas.txt
@@ -1,3 +1,2 @@
-great idea
 bad idea
 mediocre idea
```

Indeed!

---

## Finding a developer to talk to (large projects)

- Example: you want to know who implemented a specific keyword/functionality
- `git grep` for the keyword or screen message
- Then with `git blame` find the person who introduced it
- With `git show` check the commit that introduced the change (it could be a file rename done by someone else)
- In the latter case check out a version prior to the move or rename and `git grep` and `git blame` there

---

## Going back in time

We do not have to branch from the tip of the branch (HEAD).
We can branch from arbitrary (earlier) hash:

```shell
$ git checkout -b <name> <hash>
```

This is the recommended mechanism to inspect old code (hash abc123):

```shell
$ git checkout -b museum abc123  # create branch called "museum" from hash abc123
  # do some archaeology ...
  # "What was I thinking back then!?"
  # "Aha!"
$ git checkout master            # after you are done switch back to "master"
$ git branch -d museum
```

Branches help us to keep the repository organized.

---

## Finding commits not merged upstream

So you would like to know which commits from current branch have not been
merged to `<branch>`. No problem with `git cherry`:

Here is an example:

```shell
$ git clone https://github.com/bast/git-rebase-squash-exercise.git
$ cd git-rebase-squash-exercise
$ git checkout haiku
$ git cherry master

+ 7e1f903f77d2b6d8ac2b9a403e30367b5b7eeb4a
+ 3ff39a18a24074e83ee30e4e959d3863ae05ed82
+ 54fba2116e74af3170314d0e2be85b34c6f27490
+ a3278e36ddbbd8b1feff38ba973ede4b3d9323c9
+ 47a007d563adb03aeedbddeb483d3c6c0301c10a
+ 65870f9c4147bace639a92b08250911b541364fe
```

These six commits are on `haiku` but are not on `master`.

Sometimes branches received different commits, then you will see hashes with "+" and "-" in front of them.

---

## Finding out when something broke

- Sometimes you realize that something broke.
- You know that it used to work.
- You do not know when it broke.
- First find out a commit in past when it worked.
- Then bisect your way until you find the commit that broke it.

```shell
$ git bisect start
$ git bisect good 75c737cf5c9  # this is a commit that worked
$ git bisect bad HEAD          # last commit is broken
  # now compile and test
  # after that decide whether
$ git bisect good
  # or
$ git bisect bad
  # now compile and test
  # after that decide whether
$ git bisect good
  # or
$ git bisect bad
  # iterate until commit is found
```

- This can even be automatized with `git bisect run <script>`.
- For this you write the script that returns zero/non-zero (success/failure).

---

## Git bisect exercise

Clone or fork it from [here](https://github.com/bast/git-bisect-exercise).


### Motivation

The motivation for this exercise is to be able to do archaeology with Git on a
source code where the bug is difficult to see visually. Finding the offending
commit is often more than half the debugging.


### Background

The script `get_pi.py` approximates pi using terms of the Nilakantha series. It
should produce 3.141519 but it does not. The script broke at some point and
produces 3.57361 using the last commit:

```
$ python get_pi.py

3.573618985595276
```

At some point within the 500 first commits, an error was introduced. The only
thing we know is that the first commit worked correctly.


### Your task

Use `git bisect` to find the commit which broke the computation.


### Bonus exercise

Write a script that checks for a correct result and use `git bisect run` to
find the offending commit automatically.
