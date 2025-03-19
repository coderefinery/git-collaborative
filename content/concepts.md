# Concepts around collaboration

:::{objectives}
- Be able to decide whether to divide work at the branch level or at the repository level.
:::


## Commits, branches, repositories, forks, clones

- {term}`repository`: The project, contains all data and history (commits, branches, tags).
- {term}`commit`: Snapshot of the project, gets a unique identifier (e.g. `c7f0e8bfc718be04525847fc7ac237f470add76e`).
- {term}`branch`: Independent development line. The main development line is often called `main`.
- {term}`tag`: A pointer to one commit, to be able to refer to it later. Like a [commemorative plaque](https://en.wikipedia.org/wiki/Commemorative_plaque)
  that you attach to a particular commit (e.g. `phd-printed` or `paper-submitted`).
- {term}`cloning <clone>`: Copying the whole repository to your laptop - the first time. It is not necessary to download each file one by one.
- {term}`forking <fork>`: Taking a copy of a repository (which is typically not yours) - your
  copy (fork) stays on GitHub/GitLab and you can make changes to your copy.


## Cloning a repository

In order to make a complete copy a whole repository, the `git clone` command
can be used. When cloning, all the files, of all or selected branches, of a
repository are copied in one operation. Cloning of a repository is of relevance
in a few different situations:
* Working on your own, cloning is the operation that you can use to create
  multiple instances of a repository on, for instance, a personal computer, a
  server, and a supercomputer.
* The parent repository could be a repository that you or your colleague own. A
  common use case for cloning is when working together within a smaller team
  where everyone has read and write access to the same git repository.
* Alternatively, cloning can be made from a public repository of a code that
  you would like to use. Perhaps you have no intention to work on the code, but
  would like to stay in tune with the latest developments, also in-between
  releases of new versions of the code.


:::{figure} img/overview/forkandclone.png
:alt: Forking and cloning
:width: 100%
:class: with-border

Forking and cloning
:::


## Forking a repository

When a fork is made on GitHub/GitLab a complete copy, of all or selected
branches, of the repository is made. The copy will reside under a different
account on GitHub/GitLab. Forking of a repository is of high relevance when
working with a git repository to which you do not have write access.
- In the fork repository commits can be made to the base branch (`main` or
  `master`), and to other branches.
- The commits that are made within the branches of the fork repository can be
  contributed back to the parent repository by means of pull or merge requests.


## Synchronizing changes between repositories

- We need a mechanism to communicate changes between the repositories.
- We will **pull** or **fetch** updates **from** remote repositories (we will soon discuss the difference between pull and fetch).
- We will **push** updates **to** remote repositories.
- We will learn how to suggest changes within repositories on GitHub and across repositories (**pull request**).
- Repositories that are forked or cloned do not automatically synchronize themselves:
  We will learn how to update forks (by pulling from the "central" repository).
- A main difference between cloning a repository and forking a repository is that the former
  is a general operation for generating copies of a repository to different computers,
  whereas forking is a particular operation implemented on GitHub/GitLab.


## Generating from templates

A repository can be marked as **template** and new repositories can be
**generated** from it, like using a cookie-cutter.

The newly created repository will start with a new ("flattened") history, only one commit, and not
inherit the history of the template.

:::{figure} img/overview/generate.png
:alt: Generating from a template
:width: 100%
:class: with-border

Generating from a template.
:::
