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
