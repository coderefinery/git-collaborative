---
layout: episode
title: Working with remotes and centralized workflow
teaching: 40
exercises: 40
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

## Cloning repositories

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

---

# Centralized workflow exercise

Exercise to practice collaborative centralized workflow. On the way to a pull request
and code review we will meet and discuss a number of typical pitfalls.


## Before we start

1. Participants add their usernames to a shared document.
2. Instructor adds participants as collaborators to this project.


## After participants have been added as collaborators


### 1. Clone [this repository]({{ site.centralized_workflow_exercise_url }})

```
$ git clone {{ site.centralized_workflow_exercise_url }}.git centralized-workflow-exercise
```

Instead of using https you can also clone using ssh keys:
- [https://help.github.com/articles/connecting-to-github-with-ssh/](https://help.github.com/articles/connecting-to-github-with-ssh/)
- [https://docs.gitlab.com/ee/gitlab-basics/create-your-ssh-keys.html](https://docs.gitlab.com/ee/gitlab-basics/create-your-ssh-keys.html)

This is a representation of what happens when you clone:

*remote*: ![]({{ site.baseurl }}/img/centralized/01-remote.svg)

*local*: ![]({{ site.baseurl }}/img/centralized/01-local.svg)

- We clone the entire history, all branches, all commits.
- `git clone` creates pointers `origin/master` and `origin/experiment`.
- `origin` refers to where we cloned from, try: `git remote -v`.
- `origin` is a shortcut for the full URL.
- `origin/master` and `origin/experiment` are read-only pointers.
- They only move during `git pull` or `git fetch` or `git push`.
- Only `git pull` or `git fetch` or `git push` require network.
- All other operations are local operations.


### 2. Step into the newly created directory

```
$ cd centralized-workflow-exercise
```


### 3. Create a file with a unique name, e.g.: `yourusername.txt`

In this file share your favourite cooking recipe or haiku or Git trick or whatever.


### 4. Stage and commit the change

```
$ git add yourusername.txt
$ git commit
```

*remote*: ![]({{ site.baseurl }}/img/centralized/01-remote.svg)

*local*: ![]({{ site.baseurl }}/img/centralized/04-local.svg)


### 5. Try to push the change to the upstream repository

```
$ git push origin master
```

By "upstream" we mean here the repository which we have cloned.
Imagine "upstream" being closer to the main development and your local
clone to be "downstream".


### 6. **Stop here** and discuss why push for most participants was rejected

You probably see something like this:

```shell
$ git push
To https://github.com/user/repo.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/user/repo.git'
To prevent you from losing history, non-fast-forward updates were rejected
Merge the remote changes (e.g. 'git pull') before pushing again.  See the
'Note about fast-forwards' section of 'git push --help' for details.
```

It will work only for one participant. Why?

*remote*: ![]({{ site.baseurl }}/img/centralized/06-remote.svg)

*local*: ![]({{ site.baseurl }}/img/centralized/04-local.svg)

The natural reflex is now to `git pull` first but
what happens if we `git pull origin master`?


### 7. Pull updates from the upstream repository

```
$ git pull origin master
```

*remote*: ![]({{ site.baseurl }}/img/centralized/06-remote.svg)

*local*: ![]({{ site.baseurl }}/img/centralized/07-local.svg)


### 8. **Stop here** and discuss why we obtained a merge commit locally

Ideas? What happened under the hood? Discuss `git fetch` as an alternative to `git pull`.
Discuss `git pull --rebase` as an alternative to avoid merge commits.

What is the difference between `git fetch` and `git pull`?

This is equivalent to:

```shell
$ git pull origin master
```

is equivalent to:

```shell
$ git fetch origin
$ git merge origin/master
```

- `git pull` consists of two operations: a `git fetch` followed by a `git merge`.
- Summary: `git pull origin master` fetches `master` from `origin` and merges it.
- There is always a `git merge` "hidden" in `git pull`.
- Many people will simply `git pull`, very careful people first `git fetch` and inspect the commits before merging them.
- With Git you typically merge several times a day without even noticing.

```shell
$ git pull --rebase origin master
```

would have produced:

*remote*: ![]({{ site.baseurl }}/img/centralized/06-remote.svg)

*local*: ![]({{ site.baseurl }}/img/centralized/08-local.svg)


### 9. Try to push again

It will work for one more person.


### 10. Create a branch `yourname/somefeature` pointing at your commit

First find out the hash of your commit, then create a branch "in the past" pointing to that
hash:

```
$ git branch yourname/somefeature [hash]
```


### 11. Push your change as a new branch

```
$ git push origin -u yourname/somefeature
```

Can we leave out the `-u`?


### 12. Submit a pull request

Submit a pull request from your branch towards the `master` branch.
Do this through the web interface.

Finally also discuss {{ site.centralized_workflow_exercise_url }}/network.

---

## How to make changes to remote branches

Create a local branch `somefeature` tracking `origin/somefeature`:

```shell
$ git checkout -b somefeature origin/somefeature
```

If there is no local branch `somefeature` and there is a remote branch `origin/somefeature`, then this is enough:

```shell
$ git checkout somefeature
```

Once we track a remote branch, we can pull from it and push to it:

```shell
$ git pull origin somefeature
$ git push origin somefeature
```

We can also delete remote branches:

```shell
$ git push origin --delete somefeature
```

---

## Centralized workflow with protected branches

- Forking workflow may be overkill for small closed-source projects.
- A good alternative to the forking workflow for a group of collaborators
  is to use a protected (`master`) branch.
- Only designated "code owners" have write access to the protected branch.
- All project members contribute code changes via pull requests from feature branches.
- Pull requests need to be approved by a code owner.
- Discuss the advantages or disadvantages of this workflow.
