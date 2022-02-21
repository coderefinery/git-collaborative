# Concepts around collaboration

```{objectives}
- Be able to decide whether to divide work at the branch level or at the repository level.
```

```{instructor-note}
- 20 min teaching
```


## Motivation

- Let's say that someone has given you access to a repository online and you want to contribute to it.
- It is quite easy to make a copy and send a change back.
- First, we do this a relatively simple way: get repository, make a change
  locally, and send the change directly back.
- Then, we make a "pull request" that allows a review.
- Once we know how code review works, we will be able to propose changes
  to repositories of others and review changes submitted by external
  contributors.


## Commits, branches, repositories, forks, clones

- **repository**: The project, contains all data and history (commits, branches, tags).
- **commit**: Snapshot of the project, gets a unique identifier (e.g. `c7f0e8bfc718be04525847fc7ac237f470add76e`).
- **branch**: Independent development line, often we call the main development line `master` or `main`.
- **tag**: A pointer to one commit, to be able to refer to it later. Like a sticky note that you attach to a particular commit (e.g. `phd-printed` or `paper-submitted`).
- **cloning**: Copying the whole repository to your laptop - the first time. It is not necessary to download each file one by one.
- **forking**: Taking a copy of a repository (which is typically not yours) - your
  copy (fork) stays on GitHub and you can make changes to your copy.

```{figure} img/overview/fork.png
:alt: Forking and cloning
:width: 100%
:class: with-border

Forking and cloning.
```


## Generating from templates and importing

There are two more ways to create "copies" of repositories into your user space:
- A repository can be marked as **template** and new repositories can be
  **generated** from it, like using a cookie-cutter.
  The newly created repository will start with a new history, only one commit, and not
  inherit the history of the template.

```{figure} img/overview/generate.png
:alt: Generating from a template
:width: 100%
:class: with-border

Generating from a template.
```

- You can **import** a repository from another hosting service or web address.
  This will preserve the history of the imported project.

```{figure} img/overview/import.png
:alt: Importing a repository
:width: 100%
:class: with-border

Importing a repository.
```
---

```{discussion}
- Visit one of the repositories/projects that you have used recently and try to find out
  how many forks exist and where they are.
- In which situations it could be useful to start from a "template" repository by generating?
```


## Synchronizing changes between repositories

- We need a mechanism to communicate changes between the repositories.
- We will **pull** or **fetch** updates **from** remote repositories (we will soon discuss the difference between pull and fetch).
- We will **push** updates **to** remote repositories.
- We will learn how to suggest changes within repositories on GitHub and across repositories.
- We will learn how to update forks by pulling/fetching changes and pushing them to forks.


```{keypoints}
- `git clone` copies everything: all commits and all branches.
- Branches on the remote appear as (read-only) local branches with a prefix, e.g. `origin/master`.
- We synchronize commits between local and remote with `git fetch`/`git pull` and `git push`.
- Repositories that are shared online often synchronize via pull requests or merge requests.
- Repositories that are forked or cloned do not automatically synchronize themselves.
```
