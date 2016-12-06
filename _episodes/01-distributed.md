---
layout: episode
title: "Collaboration via distributed version control"
teaching: 70
exercises: 20
questions:
  - "A question that this episode will answer?"
  - "Another question?"
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

name: inverse
layout: true
class: center, middle, inverse

---

## Collaboration via distributed version control

- Distributed version control
- Non-bare and bare repositories
- Cloning repositories
- Collaboration with others
- Fetching changes from remote repositories
- Pushing changes to remote repositories

---

## Distributed version control

- Git implements a distributed version control
- All these topologies are possible

![]({{ site.baseurl }}/img/intro/topo.jpg)

- In contrast to other version control tools we do not contribute to a repository
  through a lightweight working copy but rather by cloning the entire repository

---

## Non-bare and bare repositories

### Work: Non-bare repository

- Until now we have met only non-bare repositories

```shell
$ git init # creates a non-bare repository
```

- A non-bare repository contains `.git` and "the normal files"
- We can checkout local branches
- We can and do work inside non-bare repositories

### Archive: Bare repository

- We can create a bare repository

```shell
$ git init --bare # creates a bare repository
```

- A bare repository contains only the `.git` part
- We never work inside a bare repository

---

## Cloning repositories

- We can clone repositories
- We can clone on the same host

```shell
host1$ cd /path/to/repo
host1$ git init                                           # creates non-bare
host1$ git clone /path/to/repo /path/to/clone             # creates non-bare
host1$ git clone --bare /path/to/repo /path/to/clone-bare # creates bare
```

- Or you clone from another machine via ssh (or via other protocols)

```shell
host2$ git clone ssh://user@host1/path/to/repo [/path/to/clone] # non-bare
```

- A clone is a full-fledged repository
- We can clone again and again
- Typically we create a star-topology or tree-topologies or triangular topologies

---

## Cloning repositories

- Think of `git clone` as a `scp -r` "plus"
- We will see what the "plus" means
- By cloning we clone all commits, all branches, entire history

![](/img/intro/topo.jpg)

---

## When push comes to pull

- We need a mechanism to communicate changes between the repositories
- We will **pull** or **fetch** updates **from** remote repositories
- There is a difference between pull and fetch and we will see what the difference is
- We will **push** updates **to** remote repositories

## Working with others

- We collaborate with other people through clones by pulling/fetching and pushing changes
- Everybody typically works on own clones
- Sometimes one person works on several clones (typically on different machines)
- We will only push to bare repositories
- Think of Dropbox as a clone which automatically pulls/pushes from/to a bare clone sitting somewhere on
  Dropbox servers

---

## Cloning repositories

![](/img/distributed/remote-02-remote.svg)

- Imagine there is a remote repository on host1
- We are ready to clone the repository

---

## Cloning repositories

![](/img/distributed/remote-02-remote.svg)
![](/img/distributed/remote-03-local.svg)

```shell
host2$ git clone ssh://user@host1/path/to/repo [/path/to/clone]
```

- We clone the entire history, all branches, all commits
- `git clone` creates pointers `origin/master` and `origin/dev`
- `origin` refers to where we cloned from
- It is a shortcut for `ssh://user@host1/path/to/repo`

---

## Cloning repositories

![](/img/distributed/remote-02-remote.svg)
![](/img/distributed/remote-03-local.svg)

- `origin/master` and `origin/dev` are read-only pointers
- They only move during `git pull` or `git fetch` or `git push`
- Only `git pull` or `git fetch` or `git push` require network
- All other operations are local operations

---

## Working with remote repositories

![](/img/distributed/remote-06-remote.svg)
![](/img/distributed/remote-03-local.svg)

- Remote repository receives a new commit
- Pointer is moved (pushed) by someone else (could be you)
- Nothing changes on the local repository until we pull/fetch these changes over the network

---

## Fetching updates

![](/img/distributed/remote-06-remote.svg)
![](/img/distributed/remote-04-local.svg)

```shell
$ git fetch origin
```

- `git fetch origin` updates `origin/master` and `origin/dev`

---

## Fetching updates

![](/img/distributed/remote-06-remote.svg)
![](/img/distributed/remote-05-local.svg)

```shell
$ git merge origin/master
```

- In a second step we merge `origin/master` (in this case fast-forward)

---

## Fetch vs. pull

```shell
$ git fetch origin
$ git merge origin/master
```

- This is equivalent to

```shell
$ git pull origin master
```

- `git pull` consists of two operations: a `git fetch` followed by a `git merge`
- Summary: `git pull origin master` fetches `master` from `origin` and merges it
- There is always a `git merge` "hidden" in `git pull`
- Many people will simply `git pull`, very careful people first `git fetch` and inspect the commits before merging them
- With Git you typically merge several times a day without even noticing

---

![](/img/distributed/remote-06-remote.svg)
![](/img/distributed/remote-06-local.svg)

- We can commit locally
- These commits are not visible to others until we `git push`
- Observe that `master`, `origin/master`, and `master` on remote repository are 3 different pointers

---

![](/img/distributed/remote-07-remote.svg)
![](/img/distributed/remote-07-local.svg)

```shell
$ git push origin master
```

- Only now the remote `master` as well as `origin/master` move

---

![](/img/distributed/remote-12-remote.svg)
![](/img/distributed/remote-08-local.svg)

- We commit `d7` and in the meantime remote receives commit `c7` from someone else
- What happens if we `git pull origin master`?

---

![](/img/distributed/remote-12-remote.svg)
![](/img/distributed/remote-09-local.svg)

```shell
$ git pull origin master
```

- First we fetched (`origin/master` moved),
  then we merged `origin/master` to `master` (`master` moved)
- Local master and remote master are two different branches
- If they diverge, Git will merge them during `git pull`

---

![](/img/distributed/remote-12-remote.svg)
![](/img/distributed/remote-10-local.svg)

```shell
$ git pull --rebase origin master
```

- You can avoid this using `--rebase`
- This will replay your unpublished local master commits at the end of `origin/master`
- Note how `d8` changed to `d8*`

---

![](/img/distributed/remote-12-remote.svg)
![](/img/distributed/remote-11-local.svg)

```shell
$ git checkout -b dev origin/dev
```

- We create and switch to local branch `dev` tracking `origin/dev`

---

## Shortcut to checkout tracking branches

- If there is no local branch `dev` and there is a remote branch `origin/dev`,
  then both are equivalent

```shell
$ git checkout -b dev origin/dev
```

```shell
$ git checkout dev
```

---

![](/img/distributed/remote-12-remote.svg)
![](/img/distributed/remote-12-local.svg)

- As we commit to `dev` the pointer moves while `origin/dev` does not

---

![](/img/distributed/remote-13-remote.svg)
![](/img/distributed/remote-13-local.svg)

```shell
$ git push origin dev
```

- We have pushed `origin/dev` forward

---

- What if you have created a local branch and want to make it public?
- Simply push it upstream

```shell
$ git checkout -b cool-branch    # create and switch to cool-branch
$ git commit                     # work and commit
$ git push -u origin cool-branch # push to origin and set as upstream
```

- We can also delete remote branches

```shell
$ git push origin --delete cool-branch
```

---

## Recap

- `git clone` copies everything and sets some pointers to remember where the clone came from

```shell
$ git remote -v

origin	user@somehost:somerepo (fetch)
origin	user@somehost:somerepo (push)
```

- You communicate commits with `git fetch`/`git pull` and `git push`
- All other Git operations are offline: you can work on a plane while your coworker
  is on vacation in North Korea
- `origin` refers to where you cloned from (but you can relocate it)
- `origin/foo` is a read-only pointer to branch `foo` on origin
- `origin` pointers only move when you `git fetch`/`git pull` or `git push`

---

## Recap about pull merges

![](/img/distributed/git-pull-rebase-1.svg)

- Branches are just pointers to commits
- `master` and `origin/master` are two different branches
- `HEAD` points to where we currently are

---

## Recap about pull merges

![](/img/distributed/git-pull-rebase-2.svg)

- We do some work on the local `master` and create two commits
- Time arrow goes from left to right (commit arrows point to their parents)
- What happens if we try to `git push`?

---

## Recap about pull merges

![](/img/distributed/git-pull-rebase-3a.svg)

- In this case `origin/master` received no other commits
- First we see a fast-forward merge (pointer `origin/master` simply moves)
- This is followed by a successful push

---

## Recap about pull merges

![](/img/distributed/git-pull-rebase-3b.svg)

- However, what if `origin/master` receives other commits in the meantime?
- `git push` is rejected:

```shell
$ git push
To https://github.com/user/repo.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/user/repo.git'
To prevent you from losing history, non-fast-forward updates were rejected
Merge the remote changes (e.g. 'git pull') before pushing again.  See the
'Note about fast-forwards' section of 'git push --help' for details.
```

---

## Recap about pull merges

![](/img/distributed/git-pull-rebase-3b-merge.svg)

- We now have two options to integrate the commits on `origin/master`
- First option: `git pull`
- A `git pull` always consists of `git fetch` and `git merge`
- In this case a fast-forward merge was not possible and a **merge commit is automatically created**

---

## Recap about pull merges

![](/img/distributed/git-pull-rebase-3b-rebase.svg)

- Second option: `git pull --rebase`
- This moves our local commits after the commits on `origin/master`
- This operation creates **new** commits (marked asterisk)
- The new commits are **rebased**
- The source code after `git pull` and `git pull --rebase` is the **same**
- The history is **different** (no merge commit for `git pull --rebase`)
- It is possible to make `git pull --rebase` default with `git config`

---

## When is a good moment to pull?

- Real example
    - A developer committed big changes to local master
    - But he did not pull or push for several weeks
    - When he tried to push, he could not because origin/master was out of date
    - When he tried to pull in order to update origin/master there were conflicts everywhere
    - After this experience he hated Git

---

## When is a good moment to pull?

- Explanation
    - Local master and remote master are two different branches
    - Local feature branch and remote feature branch are two different branches
    - `git pull` fetches and merges
    - If you never pull then the branches may diverge
    - `git pull` often to stay in sync with upstream development
    - `git push` whenever you want other people to know about your changes
    - If you never `git push` others will not see your changes
    - Nontrivial changes should not be done on master

---

## Working with multiple remotes

- There is nothing special about the name `origin`
- `origin` is just an alias
- Working with multiple remotes is not scary
- We can call these aliases as we like
- We can add and remove remotes

```shell
$ git remote add upstream https://github.com/foo/foo.git
$ git remote rm upstream
$ git remote add group-repo https://example.com/exciting-project.git
$ git remote rm group-repo
```

- We synchronize remotes via the local clone
- To see all remotes

```shell
$ git remote -v
```

---

## Repository layouts

- Centralized layout
- Decentralized layout
- Fork/pull-request layout

---

## Tags

- Tags are also just pointers to commits
- While branches are mutable, tags are (typically) immutable
- Tags can carry extra annotation
- Always tag your releases

```shell
$ git tag                             # list all tags
$ git tag -a v1.4 -m 'my version 1.4' # create annotated tag
$ git tag v1.4                        # create lightweight tag
$ git push origin v1.5                # share tag to upstream (origin)
$ git push origin --tags              # push all tags
```

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

---

# Working with GitHub

This talk is a live demo, list below serves as memory help

- Over 3 million users
- Over 10 million repositories
- Largest code host in the world
- Today the de facto standard
- GitHub activity good for your CV
- Overview
- Creating and deleting projects
- Accessing projects (https or ssh)
- README.md
- Issues (tickets)
- Wiki
- Fork/pull-request mechanism: like peer review
- Autoclosing issues
- Discussing with mentions
- GitHub Pages
- Hooks
- Gist
- KTH has GitHub Enterprise

---

## Forking a repository

- A fork is basically a (bare) clone
- The upstream repo and the fork are in principle independent repositories
- We copy all commits, all branches

**https://github.com/foo/foo.git**
![](/img/github/github-remote-01.svg)

**https://github.com/user/foo.git**
![](/img/github/github-remote-01.svg)

---

## Cloning a fork to work on it

```shell
$ git clone https://github.com/user/foo.git
```

**https://github.com/foo/foo.git**
![](/img/github/github-remote-01.svg)

**https://github.com/user/foo.git**
![](/img/github/github-remote-01.svg)

**local repo**
![](/img/github/github-local-01.svg)

---

## Working with the local repo

- We do some work and make a commit

**https://github.com/foo/foo.git**
![](/img/github/github-remote-01.svg)

**https://github.com/user/foo.git**
![](/img/github/github-remote-01.svg)

**local repo**
![](/img/github/github-local-02.svg)

---

## Pushing the change to origin

```shell
$ git push origin master
```

**https://github.com/foo/foo.git**
![](/img/github/github-remote-01.svg)

**https://github.com/user/foo.git**
![](/img/github/github-remote-02.svg)

**local repo**
![](/img/github/github-local-03.svg)

---

## Pull-request

- We can file a pull-request
- A pull-request means: "please review my changes and if you agree, merge them with a mouseclick"

**https://github.com/foo/foo.git**
![](/img/github/github-remote-01.svg)

**https://github.com/user/foo.git**
![](/img/github/github-remote-02.svg)

**local repo**
![](/img/github/github-local-03.svg)

---

## Pull-request

- If the pull-request is accepted, the change is incorporated

**https://github.com/foo/foo.git**
![](/img/github/github-remote-02.svg)

**https://github.com/user/foo.git**
![](/img/github/github-remote-02.svg)

**local repo**
![](/img/github/github-local-03.svg)

---

## Updating the fork with upstream changes

- Upstream repo receives other changes (other merged pull-requests)
- How do we get these changes to the forked repo?

**https://github.com/foo/foo.git**
![](/img/github/github-remote-03.svg)

**https://github.com/user/foo.git**
![](/img/github/github-remote-02.svg)

**local repo**
![](/img/github/github-local-03.svg)

---

## Updating the fork with upstream changes

```shell
$ git remote add upstream https://github.com/foo/foo.git
$ git fetch upstream
```

**https://github.com/foo/foo.git**
![](/img/github/github-remote-03.svg)

**https://github.com/user/foo.git**
![](/img/github/github-remote-02.svg)

**local repo**
![](/img/github/github-local-04.svg)

---

## Updating the fork with upstream changes

```shell
$ git checkout master
$ git merge upstream/master
```

**https://github.com/foo/foo.git**
![](/img/github/github-remote-03.svg)

**https://github.com/user/foo.git**
![](/img/github/github-remote-02.svg)

**local repo**
![](/img/github/github-local-05.svg)

---

## Updating the fork with upstream changes

```shell
$ git push origin master
```

**https://github.com/foo/foo.git**
![](/img/github/github-remote-03.svg)

**https://github.com/user/foo.git**
![](/img/github/github-remote-03.svg)

**local repo**
![](/img/github/github-local-06.svg)

---

## Pro-tip

- Different URLs for fetch and push

```shell
$ git remote add origin https://github.com/foo/foo.git
$ git remote set-url --push origin https://github.com/user/foo.git
```

- Now we always fetch from the central repo and push to forked repo

```shell
$ git remote -v

origin	https://github.com/foo/foo.git (fetch)
origin	https://github.com/user/foo.git (push)
```

---

## Summary

- Working with multiple remotes is not scary
- `origin` and `upstream` are just aliases
- We can call these aliases as we like
- We can add and remove remotes

```shell
$ git remote add upstream https://github.com/foo/foo.git
$ git remote rm upstream
```

- We synchronize remotes via the local clone
- To see all remotes

```shell
$ git remote -v
```

---

Collaborative GitHub workflow exercise

https://github.com/bast/forking-workflow-exercise

---

## Fast-forward vs. non-fast-forward merges

- To clarify what is meant by "fast-forward" imagine that you are on `master` and want to merge `devel`
- What will happen if we `git merge devel`?

![](/img/branches/pre-ff.svg)

---

## Fast-forward vs. non-fast-forward merges

- If you now type `git merge devel`,
  Git will recognize that it can simply move the `master` pointer to `b3`
  without creating a merge commit
- This is a fast-forward merge

![](/img/branches/ff.svg)

- The default in Git is to fast-forward merge when possible

---

## Fast-forward vs. non-fast-forward merges

- If you do not like this you can tell Git to merge with no fast-forward

```shell
$ git merge --no-ff devel
```

![](/img/branches/no-ff.svg)

- Both is fine, the resulting code is the same, not the history
- It is a matter of taste or convention

---

Here also explain pull merge commits
