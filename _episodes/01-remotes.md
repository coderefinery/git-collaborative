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

## Motivation

- Let's say that someone has given you access to a repository online
- ... and you want to contribute to it.
- It is quite easy to make a copy and send a change back.
- First, we do this a relatively simple way: get repository, make a change
  locally, and send the change directly back.
- Then, we make a "pull request" that allows a review.
- Once we know how code review works, we will be able to propose changes
  to repositories of others and review changes submitted by external
  contributors.

---

## Commits, branches, repositories, forks, clones

- **repository**: The project, contains all data and history (commits, branches, tags).
- **commit**: Snapshot of the project, gets a unique identifier (e.g. `c7f0e8bfc718be04525847fc7ac237f470add76e`).
- **branch**: Independent development line, often we call the main development line `master`.
- **tag**: A pointer to one commit, to be able to refer to it later. Like a sticky note that you attach to a particular commit (e.g. `phd-printed` or `paper-submitted`).
- **cloning**: Copying the whole repository to your laptop - the first time. It is not necessary to download each file one by one.
- **forking**: Taking a copy of a repository (which is typically not yours) - your
  copy (fork) stays on GitHub and you can make changes to your copy.

---

## Synchronizing changes between repositories

- We need a mechanism to communicate changes between the repositories.
- We will **pull** or **fetch** updates **from** remote repositories (we will soon discuss the difference between pull and fetch).
- We will **push** updates **to** remote repositories.
