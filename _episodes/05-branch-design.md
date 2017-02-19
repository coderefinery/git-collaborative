---
layout: episode
title: "Branch design"
teaching: 20
exercises: 20
questions:
  - "How should we organize branches to avoid conflicts?"
  - "What is a good branch layout to simplify maintenance and release preparation?"
objectives:
  - "Learn how to name branches."
  - "Discuss typical branch layouts."
---

## Branch naming

- Name your local branches such that you will recognize them 3 months later.
- "test", "foo", "debug", "mybranch" are not good branch names.
- Give descriptive names to remote branches.
- For topic branches we recommend to name them "author/topic" (example `joe/new-integrator`).
- Then everybody knows who is to be contacted about this branch (e.g. stale branches).
- Also you can easily find "your" branches:

```shell
$ git branch -r | grep joe
```

- Name bugfix branches after the issue/ticket (e.g. `issue-137`).
- For release branches we recommend e.g. `release-2.x` or `stable-2.x`.

---

## Always have only one main development line

- Document where it is.
- Organize branches according to features, not according to groups of people.
- Good: branches `feature-a`, `feature-b`, `feature-c`.
- Bad: branches `stockholm`, `san_francisco`, `helsinki`.
- Reason: `stockholm`, `san_francisco`, and `helsinki` will either diverge
  (three main development lines) or somebody will spend a heroic effort to keep
  them synchronized.

---

## Every commit on the main development line should compile

- Sometimes you want to find a commit in the past that broke some functionality.
- When using `git bisect` (we will exercise `git bisect` later)
  you will see that it is very helpful if all commits compile.
- On the other hand you will see that it is annoying if you hit a commit that does not compile.
- This is why we insist so much on a compiling main development line with nice history.
- There is no reason to commit broken or unfinished code to the main development line: for this we have branches.

---

## Rebase vs. merge

To illustrate rebasing we consider the following situation - we wish to merge
`master` into `devel`:

![]({{ site.baseurl }}/img/branches/pre-rebase.svg)

Now you know how to do it:

```shell
$ git checkout devel
$ git merge master
```

This creates a merge commit:

![]({{ site.baseurl }}/img/branches/git-branch-08.svg)


But there is an alternative:

```shell
$ git checkout devel
$ git rebase master
```

![]({{ site.baseurl }}/img/branches/rebase.svg)

- `git rebase` replays the branch commits `b1` to `b3` on top of `master`.
- As if they were committed after `c5`.
- It changes history (notice that the commits `b1` to `b3` have been replaced by `b1*` to `b3*`).
- Discuss advantages and disadvantages.

### Advantages and disadvantages

- `git rebase` makes "merges" producing a linear history.
- `git rebase` may invalidate tests.
- When somebody asks you to rebase your work to the work of somebody else you know what this means.
- When working with others **do not rebase commits that you have shared**
  (history has changed).
- Reference: "Treehouse of Horror V: Time and Punishment", The Simpsons (1994).

![]({{ site.baseurl }}/img/branches/simpsons.jpg)

---

## Branch hygiene

Often we have this situation:

```shell
$ git log --oneline

6e129cf documentation for feature C
05344f6 small fix for feature C
bc11c47 save work on feature C
aa25177 feature B
6b58ba4 feature A
```

But we would prefer to have this history:

```shell
$ git log --oneline

81e100c feature C
aa25177 feature B
6b58ba4 feature A
```

- We can use `git reset --soft aa25177`.
- This means that we move our repository back to commit `aa25177`
  **but** we keep the working tree of the last committed state.
- The final state of the actual code is identical.
- Alternative to `git reset --soft` is an interactive rebase.
- We recommend to create commits on the main development line which are nice logical units.
- Commits should be pickable (not too large not too small for a `cherry-pick`).
- Avoid ball-of-mud commits.

---

## Git rebase and commit squashing exercise

### Objective

In this exercise we will practice how to squash incomplete commits into one
nice commit and replay it on top of the master branch.


### Motivation

This technique is useful in situations where you need to make changes to a pull
request before it can be integrated.


### Exercise

Start the exercise by forking and cloning [this repository](https://github.com/bast/git-rebase-squash-exercise).

The `haiku` branch represents a feature branch that is to be rebased (moved) and squashed.

On the `haiku` branch you find a script that prints a haiku:

```shell
$ git checkout haiku
$ python main.py

This is our haiku:

On a branch ...
                  by Kobayashi Issa

              On a branch
              floating downriver
              a cricket, singing.
```

The haiku is great but the
commit history on
the `haiku` branch is not (for the purpose of this exercise):

```shell
$ git log --oneline

65870f9 fix a copy-paste error
47a007d completed the haiku
a3278e3 another incomplete commit
54fba21 startign to work on it (commit with a typo)
3ff39a1 forgot to add a file
7e1f903 starting working on the haiku
c50a463 initial commit
```

Your task is to rebase the `haiku` branch on top
of `master` and squash the several small "incomplete" commits into one single
self-contained cherry-pickable commit.

In other words instead of this history:

![]({{ site.baseurl }}/img/branches/rebase-exercise-1.svg)

We wish to first rebasing the commits:

![]({{ site.baseurl }}/img/branches/rebase-exercise-2.svg)

And in a second step squash the commits into one:

![]({{ site.baseurl }}/img/branches/rebase-exercise-3.svg)

Verify the steps and the result with `git status` and `git log`.
Verify the history and also that the script still works after the operation.

---

## [Vincent Driessen model](http://nvie.com/posts/a-successful-git-branching-model/)


<img src="{{ site.baseurl }}/img/branches/nvie-model.png" style="height: 600px;"/>

(c) Vincent Driessen, licensed under CC BY-SA.

- [Link to original post](http://nvie.com/posts/a-successful-git-branching-model/).
- Very popular.
- Two long-lived branches: `develop` and `master`.
- New features are developed on feature branches.
- Feature branches branch off from `develop`.
- `master` is the latest stable release by definition.
- Everything merged to `develop` is ready to be released.
- Critique (personal opinion):
    - Naming is unfortunate and often confuses coworkers (rename `develop` to `master` and `master` to `stable`).
    - Model is not ideal if you need to support past versions and publish patches for past versions.
- Good if you do not distribute the stable release (e.g. if you run it on your servers).

---

## Alternative: separate branch for each major release

![]({{ site.baseurl }}/img/branches/tree-model.svg)

- We recommend to name release branches e.g. `release-2.x` or `stable-2.x`.
- It is then crystal clear where the main development line is.
- Does not require to create new branches for patches of past versions.
- Good if you distribute code and support past versions.
- Patches need to be applied to the oldest supported release branch and cherry-picked or merged
  "up" to the main line and all supported release branches.
- We never merge `master` to release branches.
- The `master` branch ideally only receives merges and no direct commits.

---

## Alternative: separate branch for each minor release

- [https://github.com/robertodr/branching-model-discussion](https://github.com/robertodr/branching-model-discussion)
- API-preserving changes are submitted towards minor or major release branches
- API-breaking changes are submitted towards `master`

---

## Document and enforce your branch naming and strategies

- Document recommended branch naming.
- Document your branching layout/strategy.
- Use meaningful version numbers: e.g. [semantic versioning](http://semver.org).
- Require your developers to follow it (code review).
- Write-protect your main development line and release branch(es).

---

## Tag your releases

- Tags are also just pointers to commits.
- While branches are mutable, tags are (typically) immutable.
- Tags can carry extra annotation.
- Always tag your releases:

```shell
$ git tag                              # list all tags
$ git tag -a v1.5 -m 'my version 1.4'  # create annotated tag
$ git tag v1.5                         # create lightweight tag
$ git push origin v1.5                 # share tag to upstream (origin)
$ git push origin --tags               # push all tags
```

- Use annotated tags (then it is clear who created the tag).

---

## Avoiding conflicts

- Conflicts can be avoided if you think and talk with your colleagues before committing.
- Think and plan to which branch you will commit to.
- Fortran people: modifying common blocks often causes conflicts.
- Modifying global data often causes conflicts.
- Monolithic entangled spaghetti-code maximizes risk of conflicts.
- Modular programing minimizes risk of conflicts.
- Ball-of-mud branches for "everything" maximize risk of conflicts.
- One branch for one task only.
- Resolve conflicts early.
- If the branch affects code that is likely to be modified by others, the
  branch should:
  - be short-lived and/or merge often to the main development line
  - merge the main development line often to stay up-to-date

---

## Develop separate features on separate branches

- You create a branch for your new feature that you are working on.
- While working on your feature you discover a defect or bug that has nothing to do
  with your new feature.
- Or you see some ugly code and want to clean it up.
- You are a responsible developer and you do not want to leave this defect.
- You decide to fix this defect right on your new branch "while at it".
- This is a **bad idea** - why?

![]({{ site.baseurl }}/img/confict-resolution/git-fix-1.svg)

- Reasoning
    - If you fix it on your branch other people will not see it.
    - You may want to merge it to `master` but you cannot since your new feature is not ready yet.
    - Perhaps somebody else will fix it on master in a different way and then it will conflict
      with your new feature.
    - Before you commit a change, think: "who needs this change?".
    - Based on the answer select the appropriate branch.
    - Develop separate features on separate branches and be very strict and disciplined with this.

- Better solution
    - Fix it on `master`, so other developers can see it.
    - Than merge it to your development/topic branch.

![]({{ site.baseurl }}/img/confict-resolution/git-fix-2.svg)

- Developing separate features on separate branches minimizes conflicts.
- It makes branches shorter-lived.
- This again minimizes conflicts.

---

## Wrong branch - what now?

OK I made a commit to the "wrong" branch and it is a public branch, what now?

`git cherry-pick` the commit to the "right" branch:

![]({{ site.baseurl }}/img/confict-resolution/git-fix-3.svg)

---

## Rewinding the local master branch

You made few commits to the local `master` branch.
You then realize that it broke some tests but you have no time now to fix them.
So you wish you had committed them to an experimental branch instead.

What now?

![]({{ site.baseurl }}/img/confict-resolution/git-split-branch-1.svg)

You want to move last three commits to a separate branch.

First make sure that your working directory and index are empty.

Then create a new branch (e.g. `feature`):

![]({{ site.baseurl }}/img/confict-resolution/git-split-branch-2.svg)

Now reset `master` back three commits:

```shell
$ git checkout master
$ git branch feature   # create feature branch but stay on master
$ git reset --hard c2  # on master
```

![]({{ site.baseurl }}/img/confict-resolution/git-split-branch-3.svg)

Another job well done.
However this should not be done if the commits have already been shared with others.

---

## How do we correct public commits?

- **Not** with `git reset` because we do not want to change the history for commits that others depend on.
- We use `git revert` which creates **new** commits that revert changes.
- `git revert` does not modify past commits.

---

## When is a good moment to merge?

- Feature branch merges to `master` typically once (at the end of its lifetime).
- But there may be good reasons for merging branch to `master` more often (release branch).
- Never merge a feature branch into another feature branch (branch pollution; discuss why).
- For modular projects with write-protected `master` and code review and very high discipline.
    - You typically should not merge `master` except the occasional `git cherry-pick`.
- For entangled projects where most of the development happens directly on `master`.
    - It is good to merge `master` to your topic branch often to stay in sync with main development line.
    - Merge `master` to your branch ideally should never conflict.
    - But it will sometimes, resolve conflicts early.

---

## Develop on feature branches

- Keeps bugs away from the main development line.
- Divide and conquer: do not create a branch for "everything".
- The more you do on one branch the longer it will take until you can reintegrate it.
- The more granular the branches, the shorter lived.
- Talk with your colleagues to avoid conflicts.

### How to test combinations of features?

- I develop `feature-a`.
- My colleague develops `feature-b`.
- Both are not ready yet to go into the main line.
- How can we test them together?
- Do not cross-merge feature branches.
- Reason: if `feature-a` becomes ready, it cannot be integrated to the main line.
  because it is then diluted with `feature-b`.
- It is easy to make soup out of vegetables, it is difficult to separate a vegetable out of a soup.
- Test combinations on integration branches.
- Integration branches only integrate, we do not "work" on them.
- Same holds for testing combinations with the main line.
- The main line should ideally be an integration branch.
