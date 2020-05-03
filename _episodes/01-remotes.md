---
layout: episode
title: Copying, sharing, and synchronizing repositories
teaching: 20
exercises: 0
questions:
  - How can we backup repositories?
  - How can we share repositories with others?
  - How can we keep repositories in sync?
  - What are different ways to make a copy of the entire repository?
objectives:
  - Be able to decide whether to divide work at the branch level or at the repository level.
keypoints:
  - "`git clone` copies everything: all commits and all branches."
  - Branches on the remove appear as (read-only) local branches with a prefix, e.g. `origin/master`.
  - We synchronize commits between local and remote with `git fetch`/`git pull` and `git push`.
  - Repositories that are shared online often synchronize via pull requests or merge requests.
---

# Motivation

- Let's say that someone has given you access to a repository online
- ... and you want to contribute to it.
- It is quite easy to make a copy and send a change back
- First, we do this a relatively simple way: get repository and send
  code directly back.
- Then, we make a "pull request" that allows a review.

# Basics

## Cloning repositories

The `git clone` command make a copy of a repository.  For example,
```shell
$ git clone https://host.com/user/project.git project
```

- Contributing to a repository often starts by cloning the entire repository.
- By cloning we clone all commits, all branches and tags, **entire history**.
- A clone is a full-fledged repository.

---

## Synchronizing changes between repositories

- We need a mechanism to communicate changes between the repositories.
- We will **pull** or **fetch** updates **from** remote repositories (we will soon discuss the difference between pull and fetch).
- We will **push** updates **to** remote repositories.
