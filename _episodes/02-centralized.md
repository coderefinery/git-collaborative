---
layout: episode
title: Centralized workflow
teaching: 20
exercises: 40
questions:
  - How can we collaborate with others within one repository?
objectives:
  - Understand how to collaborate using a centralized workflow.
  - Understand the difference between local branch, origin/branch, and remote branch.
keypoints:
  - Centralized workflow is often used for remote collaborative work.
  - "`origin` refers to where you cloned from (but you can relocate it)."
  - "`origin/mybranch` is a read-only pointer to branch `mybranch` on `origin`."
  - "These read-only pointers only move when you `git fetch`/`git pull` or `git push`."
---

## Distributed version control

![The GitHub Octocat]({{ site.baseurl }}/img/forking/github_octocat.jpeg)

Git implements a **distributed** version control.
This means that any type of repository links that you can think of can be
implemented - not just "everything connects to one central server.

In this episode, we will explore the usage of a **centralized workflow** for collaborating online on a github project.

### Centralized layout

![]({{ site.baseurl }}/img/forking/centralized.svg)

In Git, all repositories are equivalent but in the typical **centralized** style, we consider one repository
as the main development line and this is marked as "central".
The "central" is a role, not a technical difference.

Features:

- Typically all developers have both read and write permissions (double-headed arrows).
- Suited for cases where all developers are in the same group or organization etc.
- Code review workflow is possible.
- Code review can be coupled with with automated testing.

Advantages:

- More familiar for Subversion or CVS users.
- Easier: for each clone there is only one remote.

Disadvantages:

- Everybody who wants to contribute needs write access.
- Maintainer needs to trust the developers to not break things (but you can protect branches).

Real life examples:

- Within the CodeRefinery team we mostly use this approach: [https://github.com/coderefinery](https://github.com/coderefinery)
- [https://github.com/ropensci/plotly](https://github.com/ropensci/plotly)

---

## Centralized workflow exercise

> Exercise preparation
>
> In this exercise, we practice collaborative centralized workflow in small groups
> (4-5 persons). Each group needs to appoint someone who will host the shared
> github repository: *an administrator*.
> For online teaching, use breakout rooms.
>
{: .callout}

First, **one person** per group (*administrator*) **generate** a new repository from a Coderefinery template. Then group members **clone** it (make a local copy) and create a new branch to add changes. Finally each member makes a **pull request** (sending code so that
others can review and accept later).

We'll discuss how this leads to code review
and discuss a number of typical pitfalls.


### Before we start

<font color="red">One person per group (administrator):</font>

1. Each group administrator generate a new repository from [template-centralized-workflow-exercise](https://github.com/coderefinery/template-centralized-workflow-exercise) called `centralized-workflow-exercise`:
<img src="{{ site.baseurl }}/img/centralized/generate_repo.png" width="700"/>

There is no need to tick *"Include all branches"* for this exercise.
2. Everyone in your group needs their GitHub account to be added to your central repository.
    - Participants give their GitHub usernames to their chosen administrator (in their respective group).
    - Administrator gives the other group members the newly created github repository URL - if in not online, try writing it in the shared document if in person.
    - Administrator adds participants as collaborators to their project.  Settings → Manage Access → Invite a collaborator.


### After participants have been added as collaborators


#### 1. Clone your administrator's group repository

```
$ git clone {{ site.centralized_workflow_exercise_url }}.git centralized-workflow-exercise
```

Where you replace `coderefinery` by your repository administrator.

Instead of using https you can also clone using ssh keys:
- [https://help.github.com/articles/connecting-to-github-with-ssh/](https://help.github.com/articles/connecting-to-github-with-ssh/)
- [https://docs.gitlab.com/ee/gitlab-basics/create-your-ssh-keys.html](https://docs.gitlab.com/ee/gitlab-basics/create-your-ssh-keys.html)

This is a representation of what happens when you clone:

*remote*: ![]({{ site.baseurl }}/img/centralized/01-remote.svg)

*local*: ![]({{ site.baseurl }}/img/centralized/01-local.svg)

- We clone the entire history, all branches, all commits. In our case, we have one branch (we did not include *all branches* when creating our repository from template) and we have only one commit (*initial commit*).
- `git clone` creates pointers `origin/master` so you can see the branches of the origin.
- `origin` refers to where we cloned from, try: `git remote -v`.
- `origin` is a shortcut for the full URL.
- `origin/master` is a read-only pointer.
- They only move during `git pull` or `git fetch` or `git push`.
- Only `git pull` or `git fetch` or `git push` require network.
- All other operations are local operations.


#### 2. Step into the newly created directory

```
$ cd centralized-workflow-exercise
```


#### 3. Create a branch `yourname/somefeature` pointing at your commit

Create a branch from the current `master`:

```
$ git branch yourname/somefeature
$ git checkout yourname/somefeature
```

The `yourname/` prefix has no special meaning here (not like `origin/`): it is just part of a
branch name to indicate who made it.


#### 4. Create a file with a unique name, e.g.: `yourusername.txt`

In this file share your favourite cooking recipe or haiku or Git trick or whatever.


#### 5. Stage and commit the change

```
$ git add yourusername.txt
$ git commit
```

*remote*: ![]({{ site.baseurl }}/img/centralized/01-remote.svg)

*local*: ![]({{ site.baseurl }}/img/centralized/04-local.svg)


#### 6. Push your change as a new branch

```
$ git push origin -u yourname/somefeature
```

Can we leave out the `-u`?


#### 7. Submit a pull request

Submit a pull request from your branch towards the `master` branch.
Do this through the web interface.

A pull-request means: "please review my changes and if you agree, merge them with a mouse-click". In a popular project, it means that anyone can
contribute with *almost no work* on the maintainer's side - a big win.

> ## Code Review
> In a centralized workflow, everyone has write access to the "central" repository and you could merge yourself your own pull-request. However, we usually recommend to get your own pull-request to be reviewed and accepted by someone else in your group.
{: .callout}

Once the pull-request is accepted, the change is merged:

*central*: ![]({{ site.baseurl }}/img/centralized/06-remote.svg)

*local*: ![]({{ site.baseurl }}/img/centralized/04-local.svg)

Finally also discuss {{ site.centralized_workflow_exercise_url }}/network.


#### 8. Update your local copy

Your branch `yourname/somefeature` is not needed anymore but more importantly, you need to sync your local copy:

```
$ git checkout master
$ git pull origin master
```
*central*: ![]({{ site.baseurl }}/img/centralized/06-remote.svg)

*local*: ![]({{ site.baseurl }}/img/centralized/07-local.svg)

> ## Why did we create a feature branch `yourname/somefeature`? (optional)
>
> This exercise is done in groups of 4-5 persons and can be done through a discussion only.
> Whenever we make update to our repository, we create a new branch and make pull-request. Let's now imagine that everyone in your group makes a new change (create a new file) but without creating a new branch.
>
> 1. You all create a new file in the master branch, stage and commit your change locally
> 2. Try to push the change to the upstream repository
>
> ```
> git push origin master
> ```
>
> 3. **Stop here** and discuss why push for most participants was rejected
>
> You probably see something like this:
>
> ```shell
> $ git push
> To https://github.com/user/repo.git
>  ! [rejected]        master -> master (non-fast-forward)
> error: failed to push some refs to 'https://github.com/user/repo.git'
> To prevent you from losing history, non-fast-forward updates were rejected
> Merge the remote changes (e.g. 'git pull') before pushing again.  See the
> 'Note about fast-forwards' section of 'git push --help' for details.
> ```
>
> The push only worked for one participant. Why?
>
{: .challenge}

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
  is to use a **protected** (only certain people may directly push to
  it) `master` branch.
- Only designated "code owners" have write access to the protected branch.
- Anyone else may contribute code changes via pull requests from feature branches.
- Pull requests need to be approved by a code owner.
- Discuss the advantages or disadvantages of this workflow.
