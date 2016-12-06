---
layout: episode
title: "Distributed version control"
teaching: 30
exercises: 30
questions:
  - "How can we collaborate with people who we might not know yet?"
  - "What is a fork?"
  - "What is a pull request or merge request?"
  - "How do teams collaborate on GitHub or GitLab or Bitbucket?"
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

## Distributed version control

- Git implements a distributed version control
- All these topologies are possible

![]({{ site.baseurl }}/img/intro/topo.jpg)

- Typically we create a star-topology or tree-topologies or triangular topologies

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
![]({{ site.baseurl }}/img/github/github-remote-01.svg)

**https://github.com/user/foo.git**
![]({{ site.baseurl }}/img/github/github-remote-01.svg)

---

## Cloning a fork to work on it

```shell
$ git clone https://github.com/user/foo.git
```

**https://github.com/foo/foo.git**
![]({{ site.baseurl }}/img/github/github-remote-01.svg)

**https://github.com/user/foo.git**
![]({{ site.baseurl }}/img/github/github-remote-01.svg)

**local repo**
![]({{ site.baseurl }}/img/github/github-local-01.svg)

---

## Working with the local repo

- We do some work and make a commit

**https://github.com/foo/foo.git**
![]({{ site.baseurl }}/img/github/github-remote-01.svg)

**https://github.com/user/foo.git**
![]({{ site.baseurl }}/img/github/github-remote-01.svg)

**local repo**
![]({{ site.baseurl }}/img/github/github-local-02.svg)

---

## Pushing the change to origin

```shell
$ git push origin master
```

**https://github.com/foo/foo.git**
![]({{ site.baseurl }}/img/github/github-remote-01.svg)

**https://github.com/user/foo.git**
![]({{ site.baseurl }}/img/github/github-remote-02.svg)

**local repo**
![]({{ site.baseurl }}/img/github/github-local-03.svg)

---

## Pull-request

- We can file a pull-request
- A pull-request means: "please review my changes and if you agree, merge them with a mouseclick"

**https://github.com/foo/foo.git**
![]({{ site.baseurl }}/img/github/github-remote-01.svg)

**https://github.com/user/foo.git**
![]({{ site.baseurl }}/img/github/github-remote-02.svg)

**local repo**
![]({{ site.baseurl }}/img/github/github-local-03.svg)

---

## Pull-request

- If the pull-request is accepted, the change is incorporated

**https://github.com/foo/foo.git**
![]({{ site.baseurl }}/img/github/github-remote-02.svg)

**https://github.com/user/foo.git**
![]({{ site.baseurl }}/img/github/github-remote-02.svg)

**local repo**
![]({{ site.baseurl }}/img/github/github-local-03.svg)

---

## Updating the fork with upstream changes

- Upstream repo receives other changes (other merged pull-requests)
- How do we get these changes to the forked repo?

**https://github.com/foo/foo.git**
![]({{ site.baseurl }}/img/github/github-remote-03.svg)

**https://github.com/user/foo.git**
![]({{ site.baseurl }}/img/github/github-remote-02.svg)

**local repo**
![]({{ site.baseurl }}/img/github/github-local-03.svg)

---

## Updating the fork with upstream changes

```shell
$ git remote add upstream https://github.com/foo/foo.git
$ git fetch upstream
```

**https://github.com/foo/foo.git**
![]({{ site.baseurl }}/img/github/github-remote-03.svg)

**https://github.com/user/foo.git**
![]({{ site.baseurl }}/img/github/github-remote-02.svg)

**local repo**
![]({{ site.baseurl }}/img/github/github-local-04.svg)

---

## Updating the fork with upstream changes

```shell
$ git checkout master
$ git merge upstream/master
```

**https://github.com/foo/foo.git**
![]({{ site.baseurl }}/img/github/github-remote-03.svg)

**https://github.com/user/foo.git**
![]({{ site.baseurl }}/img/github/github-remote-02.svg)

**local repo**
![]({{ site.baseurl }}/img/github/github-local-05.svg)

---

## Updating the fork with upstream changes

```shell
$ git push origin master
```

**https://github.com/foo/foo.git**
![]({{ site.baseurl }}/img/github/github-remote-03.svg)

**https://github.com/user/foo.git**
![]({{ site.baseurl }}/img/github/github-remote-03.svg)

**local repo**
![]({{ site.baseurl }}/img/github/github-local-06.svg)

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

![]({{ site.baseurl }}/img/branches/pre-ff.svg)

---

## Fast-forward vs. non-fast-forward merges

- If you now type `git merge devel`,
  Git will recognize that it can simply move the `master` pointer to `b3`
  without creating a merge commit
- This is a fast-forward merge

![]({{ site.baseurl }}/img/branches/ff.svg)

- The default in Git is to fast-forward merge when possible

---

## Fast-forward vs. non-fast-forward merges

- If you do not like this you can tell Git to merge with no fast-forward

```shell
$ git merge --no-ff devel
```

![]({{ site.baseurl }}/img/branches/no-ff.svg)

- Both is fine, the resulting code is the same, not the history
- It is a matter of taste or convention

---

Here also explain pull merge commits
