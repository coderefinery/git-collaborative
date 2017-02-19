---
layout: episode
title: "Distributed version control"
teaching: 20
exercises: 35
questions:
  - "How can we collaborate with people who we might not know yet?"
  - "What is a fork?"
  - "What is a pull request or merge request?"
  - "What is code review?"
  - "How do teams collaborate on GitHub or GitLab or Bitbucket?"
objectives:
  - "Get a mental representation of what is happening on GitHub."
  - "Get comfortable with the forking workflow."
keypoints:
  - "Working with multiple remotes is not as scary as it looks."
  - "`origin` is just an alias."
  - "We can add and remove remotes."
  - "We can call these aliases as we like."
  - "We synchronize remotes via the local clone."
  - "To see all remotes use `git remote -v`."
  - "If you are more than one person contributing to a project, implement code review."
---

## Distributed version control

Git implements a distributed version control.
Basically any repository topology that you can think of can be implemented.

Two topologies are very frequent: centralized and forking layout.


### Centralized layout

![]({{ site.baseurl }}/img/distributed/centralized.svg)

In Git all repositories are in principle equivalent but typically we consider one repository
as the main development line and this is marked as "central".
The "central" is a role, not a technical difference.

Features:

- Typically all developers have both read and write permissions (double-headed arrows).

Advantages:

- More familiar for Subversion or CVS users.
- Easier: for each clone there is only one remote.

Disadvantages:

- No code review.
- Maintainer needs to trust the developers to not break things.


### Forking layout

![]({{ site.baseurl }}/img/distributed/forking-overview.svg)

Again we call one repository the "central" repository.

Features:

- Most developers have only read access.
- For a public repository everybody has read access.
- Only very few people (the maintainers) have write access.
- Typically nobody pushes directly to the central repo.
- Central repo and the forks typically reside in the "cloud".

Advantages:

- Code is integrated via code review (during pull/merge request).
- Maintainer has full control over what goes in.
- Allows contributions from people you don't know yet (in practice not possible in centralized layout).
- Allows to implement peer review in coding (code review).
- Allows to couple code review with automated testing.

Disadvantages:

- Learning curve: we need to deal at least with two remotes (fork and central repo).

---

## Working with multiple remotes

- There is nothing special about the name `origin`. The `origin` is just an alias.
- We can call these aliases as we like.
- We can add and remove remotes.

```shell
$ git remote add upstream https://github.com/project/project.git
$ git remote rm upstream
$ git remote add group-repo https://example.com/exciting-project.git
$ git remote rm group-repo
```

We synchronize remotes via the local clone.

To see all remotes:

```shell
$ git remote -v
```

---

## Exercise to practice collaborative forking workflow

We will run this exercise in groups and we number the groups
1, 2, ..., etc.

Objectives:

- Learn how to fork, modify the fork, and file a pull request towards forked repo.
- Learn how to update your fork with upstream changes.

We will do this exercise on [GitHub](https://github.com) but also
[GitLab](https://gitlab.com) and [Bitbucket](https://bitbucket.org) allow
similar workflows and basically everything that we will discuss is transferable.


### Part A: Fork and clone

First fork [this repository](https://github.com/coderefinery/forking-workflow-exercise)
on GitHub into your namespace and then clone the fork to your computer.

Here is a pictorial representation of this part:

![]({{ site.baseurl }}/img/distributed/forking-1.svg)

This is how it looks after we fork:

*central*: ![]({{ site.baseurl }}/img/github/github-remote-01.svg)

*fork*: ![]({{ site.baseurl }}/img/github/github-remote-01.svg)

- A fork is basically a (bare) clone.
- The upstream repo and the fork are in principle independent repositories.
- When forking we copy all commits, all branches.

After we clone the fork we have three in principle independent repositories:

*central*: ![]({{ site.baseurl }}/img/github/github-remote-01.svg)

*fork*: ![]({{ site.baseurl }}/img/github/github-remote-01.svg)

*local*: ![]({{ site.baseurl }}/img/github/github-local-01.svg)


### Part B: Modify and commit

Then add a file `groupN.py` where N is your group number, e.g. `group17.py`.
**Add only one file per group**. (Why?)

This file should contain a function called `tweet()` which returns
a string of maximum 140 characters, for instance:

```python
def tweet():
    return "please replace this boring sentence with something more fun"
```

The file `main.py` automatically calls all `tweet()` functions defined in files
`groupN.py` (1 <= N <= 50). You do not need to edit `main.py`.

Test it before you commit your change:

```shell
$ python main.py

group 17 says: please replace this boring sentence with something more fun
```

If it works, commit the change. And here is a picture of what just happened:

*central*: ![]({{ site.baseurl }}/img/github/github-remote-01.svg)

*fork*: ![]({{ site.baseurl }}/img/github/github-remote-01.svg)

*local*: ![]({{ site.baseurl }}/img/github/github-local-02.svg)


### Part C: Push your changes to the fork

Once you see your sentence correctly printed, commit and push to your fork. Don't worry
nothing gets out to Twitter but please mind that your changes will be public on
GitHub (but you can delete them later).

```shell
$ git push origin master
```

*central*: ![]({{ site.baseurl }}/img/github/github-remote-01.svg)

*fork*: ![]({{ site.baseurl }}/img/github/github-remote-02.svg)

*local*: ![]({{ site.baseurl }}/img/github/github-local-03.svg)


### Part D: File a pull request

Then file a pull request towards the repository where you forked from.

Here is a pictorial representation for parts C and D:

![]({{ site.baseurl }}/img/distributed/forking-2.svg)

A pull-request means: "please review my changes and if you agree, merge them with a mouse-click".

Once the pull-request is accepted, the change is incorporated:

*central*: ![]({{ site.baseurl }}/img/github/github-remote-02.svg)

*fork*: ![]({{ site.baseurl }}/img/github/github-remote-02.svg)

*local*: ![]({{ site.baseurl }}/img/github/github-local-03.svg)

Wait here until we integrate all pull requests into the central repo
together on the big screen.


### Part E: Update your fork

We do this part **after the contributions from all groups have been integrated**.

Once this is done, practice to update your forked repo with the upstream
changes and verify that you got the files created by other groups:

```shell
$ python main.py
```

Make sure that the contributions from other groups are not only on your local repository
but really also end up in your fork.

Here is a pictorial representation of this part:

![]({{ site.baseurl }}/img/distributed/forking-3.svg)

We will discuss two solutions:

#### Longer route

- Upstream repo receives other changes (other merged pull-requests)
- How do we get these changes to the forked repo?

*central*: ![]({{ site.baseurl }}/img/github/github-remote-03.svg)

*fork*: ![]({{ site.baseurl }}/img/github/github-remote-02.svg)

*local*: ![]({{ site.baseurl }}/img/github/github-local-03.svg)

```shell
$ git remote add upstream https://github.com/coderefinery/forking-workflow-exercise.git
$ git fetch upstream
```

*central*: ![]({{ site.baseurl }}/img/github/github-remote-03.svg)

*fork*: ![]({{ site.baseurl }}/img/github/github-remote-02.svg)

*local*: ![]({{ site.baseurl }}/img/github/github-local-04.svg)

```shell
$ git checkout master
$ git merge upstream/master
```

*central*: ![]({{ site.baseurl }}/img/github/github-remote-03.svg)

*fork*: ![]({{ site.baseurl }}/img/github/github-remote-02.svg)

*local*: ![]({{ site.baseurl }}/img/github/github-local-05.svg)

```shell
$ git push origin master
```

*central*: ![]({{ site.baseurl }}/img/github/github-remote-03.svg)

*fork*: ![]({{ site.baseurl }}/img/github/github-remote-03.svg)

*local*: ![]({{ site.baseurl }}/img/github/github-local-06.svg)


#### Shorter route

Remotes are aliases. We can use remote URLs directly.

Here we pull from the central repo and push to our fork:

```shell
$ git checkout master
$ git pull https://github.com/coderefinery/forking-workflow-exercise.git master
$ git push https://github.com/user/forking-workflow-exercise.git master
```

---

## Pro-tip

Use Different URLs for fetch and push. Makes sense if you are the only person pushing to the fork:

```shell
$ git remote add origin https://github.com/project/project.git
$ git remote set-url --push origin https://github.com/user/project.git
```

Now we always fetch from the central repo and push to forked repo.

```shell
$ git remote -v

origin	https://github.com/project/project.git (fetch)
origin	https://github.com/user/project.git (push)
```
