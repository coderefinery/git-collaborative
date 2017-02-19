---
layout: episode
title: "Working with remotes"
teaching: 30
exercises: 0
questions:
  - "How can we keep repositories in sync?"
  - "How can we share repositories with others?"
objectives:
  - "Understand the difference between local branch, origin/branch, and remote branch."
keypoints:
  - "`git clone` copies everything and sets some pointers to remember where the clone came from."
  - "You communicate commits with `git fetch`/`git pull` and `git push`."
  - "All other Git operations are offline: you can work on a plane while your coworker is on vacation in North Korea."
  - "`origin` refers to where you cloned from (but you can relocate it)."
  - "`origin/foo` is a read-only pointer to branch `foo` on origin."
  - "`origin` pointers only move when you `git fetch`/`git pull` or `git push`."
---

## From local repositories to remote repositories

- In contrast to other version control tools we do not contribute to a repository
  through a lightweight working copy
- In Git we often work within a clone
- Contributing to a repository often starts by cloning the entire repository

---

## Non-bare and bare repositories

### Work: Non-bare repository

- Until now we have met only non-bare repositories

```shell
$ git init  # creates a non-bare repository
```

- A non-bare repository contains `.git` as well as a snapshot of your tracked files that you can directly edit
- We can checkout local branches
- We can and do work inside non-bare repositories

### Archive: Bare repository

- We can create a bare repository

```shell
$ git init --bare  # creates a bare repository
```

- A bare repository contains only the `.git` part
- We never do actual work inside a bare repository

---

## Cloning repositories

```shell
$ git clone https://host.com/user/project.git project
```

- A clone is a full-fledged repository
- Think of `git clone` as a `scp -r` "plus"
- We will see what the "plus" means
- By cloning we clone all commits, all branches and tags, **entire history**

---

## When push comes to pull

- We need a mechanism to communicate changes between the repositories
- We will **pull** or **fetch** updates **from** remote repositories
- There is a difference between pull and fetch and we will soon discuss what the difference is
- We will **push** updates **to** remote repositories

---

## Working with others

- We collaborate with other people through clones by pulling/fetching and pushing changes
- Everybody typically works on own clones
- Sometimes one person works on several clones (typically on different machines)
- We will only push to bare repositories
- Think of Dropbox as a clone which automatically pulls/pushes from/to a bare clone sitting somewhere on
  Dropbox servers

---

## Cloning repositories

This is a representation of what happens when you clone:

*remote*: ![]({{ site.baseurl }}/img/distributed/remote-02-remote.svg)

*local*: ![]({{ site.baseurl }}/img/distributed/remote-03-local.svg)

- We clone the entire history, all branches, all commits (in this example two branches, four commits)
- `git clone` creates pointers `origin/master` and `origin/dev`
- `origin` refers to where we cloned from, try: `git remote -v`
- `origin` is a shortcut for the full URL
- `origin/master` and `origin/dev` are read-only pointers
- They only move during `git pull` or `git fetch` or `git push`
- Only `git pull` or `git fetch` or `git push` require network
- All other operations are local operations

---

## Fetching updates

Let us imagine that the remote repository receives a new commit:

*remote*: ![]({{ site.baseurl }}/img/distributed/remote-06-remote.svg)

*local*: ![]({{ site.baseurl }}/img/distributed/remote-03-local.svg)

Pointer is moved (pushed) by someone else (could be you).

Nothing changes on the local repository until we pull/fetch these changes over the network:

```shell
$ git fetch origin
```

`git fetch origin` updates `origin/master` and `origin/dev`:

*remote*: ![]({{ site.baseurl }}/img/distributed/remote-06-remote.svg)

*local*: ![]({{ site.baseurl }}/img/distributed/remote-04-local.svg)

In a second step we merge `origin/master` (in this case fast-forward; further below we explain what fast-forward means):

```shell
$ git merge origin/master
```
This updates the local branches:

*remote*: ![]({{ site.baseurl }}/img/distributed/remote-06-remote.svg)

*local*: ![]({{ site.baseurl }}/img/distributed/remote-05-local.svg)

---

## Fetch vs. pull

What is the difference between `git fetch` and `git pull`?

So far we have fetched and merged in two steps:

```shell
$ git fetch origin
$ git merge origin/master
```

This is equivalent to:

```shell
$ git pull origin master
```

- `git pull` consists of two operations: a `git fetch` followed by a `git merge`
- Summary: `git pull origin master` fetches `master` from `origin` and merges it
- There is always a `git merge` "hidden" in `git pull`
- Many people will simply `git pull`, very careful people first `git fetch` and inspect the commits before merging them
- With Git you typically merge several times a day without even noticing

---

## Publishing local commits

- We can commit locally
- These commits are not visible to others until we `git push`
- Observe that `master`, `origin/master`, and `master` on remote repository are 3 different pointers:

*remote*: ![]({{ site.baseurl }}/img/distributed/remote-06-remote.svg)

*local*: ![]({{ site.baseurl }}/img/distributed/remote-06-local.svg)

Now let us push the local commits upstream:

```shell
$ git push origin master
```

Only now the remote `master` as well as `origin/master` move:

*remote*: ![]({{ site.baseurl }}/img/distributed/remote-07-remote.svg)

*local*: ![]({{ site.baseurl }}/img/distributed/remote-07-local.svg)

We commit `d8` (the color is to signal that we differ, we are still on
`master`)
and in the meantime remote receives commit `c8` from someone else

*remote*: ![]({{ site.baseurl }}/img/distributed/remote-12-remote.svg)

*local*: ![]({{ site.baseurl }}/img/distributed/remote-08-local.svg)

What happens if we try to `git push origin master`?

`git push` is rejected:

```shell
$ git push
To https://github.com/user/repo.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/user/repo.git'
To prevent you from losing history, non-fast-forward updates were rejected
Merge the remote changes (e.g. 'git pull') before pushing again.  See the
'Note about fast-forwards' section of 'git push --help' for details.
```

The natural reflex is now to `git pull` first but
what happens if we `git pull origin master`?

*remote*: ![]({{ site.baseurl }}/img/distributed/remote-12-remote.svg)

*local*: ![]({{ site.baseurl }}/img/distributed/remote-09-local.svg)

```shell
$ git pull origin master
```

Explanation:

- First we fetched (`origin/master` moved),
  then we merged `origin/master` to `master` (`master` moved)
- Local master and remote master are two different branches
- If they diverge, Git will merge them during `git pull`

You can avoid the merge commits using `--rebase`:

```shell
$ git pull --rebase origin master
```

This will replay your unpublished local master commits at the end of `origin/master`:

*remote*: ![]({{ site.baseurl }}/img/distributed/remote-12-remote.svg)

*local*: ![]({{ site.baseurl }}/img/distributed/remote-10-local.svg)

Note how `d8` changed to `d8*`.

---

## When is a good moment to pull?

- Real example
    - A developer committed big changes to local master
    - But he did not pull or push for several weeks
    - When he tried to push, he could not because origin/master was out of date
    - When he tried to pull in order to update origin/master there were conflicts everywhere
    - After this experience he hated Git

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

## Tracking branches

We want to make changes to `origin/dev`:

*remote*: ![]({{ site.baseurl }}/img/distributed/remote-12-remote.svg)

*local*: ![]({{ site.baseurl }}/img/distributed/remote-10-local.svg)

For this we create and switch to local branch `dev` tracking `origin/dev`:

```shell
$ git checkout -b dev origin/dev
```

*remote*: ![]({{ site.baseurl }}/img/distributed/remote-12-remote.svg)

*local*: ![]({{ site.baseurl }}/img/distributed/remote-11-local.svg)


### Shortcut to checkout tracking branches

If there is no local branch `dev` and there is a remote branch `origin/dev`, then both are equivalent:

```shell
$ git checkout -b dev origin/dev
```

```shell
$ git checkout dev
```

As we commit to `dev` the pointer moves while `origin/dev` does not:

*remote*: ![]({{ site.baseurl }}/img/distributed/remote-12-remote.svg)

*local*: ![]({{ site.baseurl }}/img/distributed/remote-12-local.svg)

We can now push `origin/dev` "forward":

```shell
$ git push origin dev
```

With the result:

*remote*: ![]({{ site.baseurl }}/img/distributed/remote-13-remote.svg)

*local*: ![]({{ site.baseurl }}/img/distributed/remote-13-local.svg)

What if you have created a local branch and want to make it public? Push it upstream:

```shell
$ git checkout -b cool-branch    # create and switch to cool-branch
$ git commit                     # work and commit
$ git push -u origin cool-branch # push to origin and set as upstream
```

We can also delete remote branches:

```shell
$ git push origin --delete cool-branch
```

---

## Fast-forward vs. non-fast-forward merges

It is useful to understand the difference between fast-forward vs. non-fast-forward merges.

To clarify what is meant by "fast-forward" imagine that you are on `master` and want to merge `devel`:

![]({{ site.baseurl }}/img/branches/pre-ff.svg)

What will happen if we `git merge devel`?

If you now type `git merge devel`, Git will recognize that it can simply move
the `master` pointer to `b3` without creating a merge commit

This is a fast-forward merge:

![]({{ site.baseurl }}/img/branches/ff.svg)

The default in Git is to fast-forward merge when possible.

If you do not like this you can tell Git to merge with no fast-forward:

```shell
$ git merge --no-ff devel
```

Both is fine, the resulting code is the same, not the history:

![]({{ site.baseurl }}/img/branches/no-ff.svg)

It is a matter of taste or convention.
