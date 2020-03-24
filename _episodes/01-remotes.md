---
layout: episode
title: Working with remotes
teaching: 20
exercises: 0
questions:
  - How can we share repositories with others?
  - How can we keep repositories in sync?
objectives:
  - Understand the difference between local branch, origin/branch, and remote branch.
keypoints:
  - "`git clone` copies everything and sets some pointers to remember where the clone came from."
  - You communicate commits with `git fetch`/`git pull` and `git push`.
  - All other Git operations are offline - you can work on a plane while your coworker is on vacation in North Korea.
  - "`origin` refers to where you cloned from (but you can relocate it)."
  - "`origin/foo` is a read-only pointer to branch `foo` on origin."
  - "`origin` pointers only move when you `git fetch`/`git pull` or `git push`."
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
