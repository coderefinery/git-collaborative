---
layout: episode
title: "Working with remotes"
teaching: 15
exercises: 15
questions:
  - "How can we keep repositories in sync?"
  - "How can we share repositories with others?"
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

## Collaboration via distributed version control

- Distributed version control
- Non-bare and bare repositories
- Cloning repositories
- Collaboration with others
- Fetching changes from remote repositories
- Pushing changes to remote repositories

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

---

## Cloning repositories

- Think of `git clone` as a `scp -r` "plus"
- We will see what the "plus" means
- By cloning we clone all commits, all branches, entire history

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

![]({{ site.baseurl }}/img/distributed/remote-02-remote.svg)

- Imagine there is a remote repository on host1
- We are ready to clone the repository

---

## Cloning repositories

![]({{ site.baseurl }}/img/distributed/remote-02-remote.svg)
![]({{ site.baseurl }}/img/distributed/remote-03-local.svg)

```shell
host2$ git clone ssh://user@host1/path/to/repo [/path/to/clone]
```

- We clone the entire history, all branches, all commits
- `git clone` creates pointers `origin/master` and `origin/dev`
- `origin` refers to where we cloned from
- It is a shortcut for `ssh://user@host1/path/to/repo`

---

## Cloning repositories

![]({{ site.baseurl }}/img/distributed/remote-02-remote.svg)
![]({{ site.baseurl }}/img/distributed/remote-03-local.svg)

- `origin/master` and `origin/dev` are read-only pointers
- They only move during `git pull` or `git fetch` or `git push`
- Only `git pull` or `git fetch` or `git push` require network
- All other operations are local operations

---

## Working with remote repositories

![]({{ site.baseurl }}/img/distributed/remote-06-remote.svg)
![]({{ site.baseurl }}/img/distributed/remote-03-local.svg)

- Remote repository receives a new commit
- Pointer is moved (pushed) by someone else (could be you)
- Nothing changes on the local repository until we pull/fetch these changes over the network

---

## Fetching updates

![]({{ site.baseurl }}/img/distributed/remote-06-remote.svg)
![]({{ site.baseurl }}/img/distributed/remote-04-local.svg)

```shell
$ git fetch origin
```

- `git fetch origin` updates `origin/master` and `origin/dev`

---

## Fetching updates

![]({{ site.baseurl }}/img/distributed/remote-06-remote.svg)
![]({{ site.baseurl }}/img/distributed/remote-05-local.svg)

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

![]({{ site.baseurl }}/img/distributed/remote-06-remote.svg)
![]({{ site.baseurl }}/img/distributed/remote-06-local.svg)

- We can commit locally
- These commits are not visible to others until we `git push`
- Observe that `master`, `origin/master`, and `master` on remote repository are 3 different pointers

---

![]({{ site.baseurl }}/img/distributed/remote-07-remote.svg)
![]({{ site.baseurl }}/img/distributed/remote-07-local.svg)

```shell
$ git push origin master
```

- Only now the remote `master` as well as `origin/master` move

---

![]({{ site.baseurl }}/img/distributed/remote-12-remote.svg)
![]({{ site.baseurl }}/img/distributed/remote-08-local.svg)

- We commit `d7` and in the meantime remote receives commit `c7` from someone else
- What happens if we `git pull origin master`?

---

![]({{ site.baseurl }}/img/distributed/remote-12-remote.svg)
![]({{ site.baseurl }}/img/distributed/remote-09-local.svg)

```shell
$ git pull origin master
```

- First we fetched (`origin/master` moved),
  then we merged `origin/master` to `master` (`master` moved)
- Local master and remote master are two different branches
- If they diverge, Git will merge them during `git pull`

---

![]({{ site.baseurl }}/img/distributed/remote-12-remote.svg)
![]({{ site.baseurl }}/img/distributed/remote-10-local.svg)

```shell
$ git pull --rebase origin master
```

- You can avoid this using `--rebase`
- This will replay your unpublished local master commits at the end of `origin/master`
- Note how `d8` changed to `d8*`

---

![]({{ site.baseurl }}/img/distributed/remote-12-remote.svg)
![]({{ site.baseurl }}/img/distributed/remote-11-local.svg)

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

![]({{ site.baseurl }}/img/distributed/remote-12-remote.svg)
![]({{ site.baseurl }}/img/distributed/remote-12-local.svg)

- As we commit to `dev` the pointer moves while `origin/dev` does not

---

![]({{ site.baseurl }}/img/distributed/remote-13-remote.svg)
![]({{ site.baseurl }}/img/distributed/remote-13-local.svg)

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

![]({{ site.baseurl }}/img/distributed/git-pull-rebase-1.svg)

- Branches are just pointers to commits
- `master` and `origin/master` are two different branches
- `HEAD` points to where we currently are

---

## Recap about pull merges

![]({{ site.baseurl }}/img/distributed/git-pull-rebase-2.svg)

- We do some work on the local `master` and create two commits
- Time arrow goes from left to right (commit arrows point to their parents)
- What happens if we try to `git push`?

---

## Recap about pull merges

![]({{ site.baseurl }}/img/distributed/git-pull-rebase-3a.svg)

- In this case `origin/master` received no other commits
- First we see a fast-forward merge (pointer `origin/master` simply moves)
- This is followed by a successful push

---

## Recap about pull merges

![]({{ site.baseurl }}/img/distributed/git-pull-rebase-3b.svg)

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

![]({{ site.baseurl }}/img/distributed/git-pull-rebase-3b-merge.svg)

- We now have two options to integrate the commits on `origin/master`
- First option: `git pull`
- A `git pull` always consists of `git fetch` and `git merge`
- In this case a fast-forward merge was not possible and a **merge commit is automatically created**

---

## Recap about pull merges

![]({{ site.baseurl }}/img/distributed/git-pull-rebase-3b-rebase.svg)

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
