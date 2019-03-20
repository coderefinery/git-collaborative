---
layout: episode
title: Distributed version control and forking workflow
teaching: 20
exercises: 40
questions:
  - How can we collaborate with people who we might not know yet?
  - What is a fork?
  - What is a pull request or merge request?
  - What is code review?
  - How do teams collaborate on GitHub or GitLab or Bitbucket?
objectives:
  - Get a mental representation of what is happening on GitHub.
  - Get comfortable with the forking workflow.
keypoints:
  - Working with multiple remotes is not as scary as it looks.
  - "`origin` is just an alias."
  - We can add and remove remotes.
  - We can call these aliases as we like.
  - We synchronize remotes via the local clone.
  - "To see all remotes use `git remote -v`."
  - If you are more than one person contributing to a project, implement code review.
---

## Distributed version control

![The GitHub Octocat]({{ site.baseurl }}/img/forking/github_octocat.jpeg)


Git implements a distributed version control.
Basically any repository topology that you can think of can be implemented.

Two topologies are very frequent: centralized and forking layout.


### Centralized layout

![]({{ site.baseurl }}/img/forking/centralized.svg)

In Git all repositories are in principle equivalent but typically we consider one repository
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


### Forking layout

![]({{ site.baseurl }}/img/forking/forking-overview.svg)

Again we call one repository the "central" repository.

Features:

- Most developers have only read access to the main project.
- For a public repository everybody has read access.
- Only very few people (the maintainers) have write access.
- Typically nobody pushes directly to the central repo.
- Code review can be coupled with with automated testing.
- Central repo and the forks typically reside in the "cloud".

Advantages:

- Code is integrated via code review (during pull/merge request).
- Maintainer has full control over what goes in.
- Allows contributions from people you don't know yet (in practice not possible in centralized layout).
- Structurally helps to implement peer review in coding (code review).

Disadvantages:

- Learning curve: we need to deal at least with two remotes (fork and central repo).
- Introduces additional steps (to e.g. update the fork).

---

## Working with multiple remotes

- There is nothing special about the name `origin`. The `origin` is just an alias.
- We can call these aliases as we like.
- We can add and remove remotes:

```shell
$ git remote add upstream https://github.com/project/project.git
$ git remote rm upstream
$ git remote add group-repo https://example.com/exciting-project.git
$ git remote rm group-repo
```

We synchronize remotes via the local clone.

To see all remotes:

```shell
$ git remote --verbose
```

---

## Exercise 1: practice collaborative forking workflow

We will run this exercise in groups. Groups can choose a number or a name.

Objectives:

- Learn how to fork, modify the fork, and file a pull request towards the forked repo.
- Learn how to update your fork with upstream changes.

We will do this exercise on [GitHub](https://github.com) but also
[GitLab](https://gitlab.com) and [Bitbucket](https://bitbucket.org) allow
similar workflows and basically everything that we will discuss is transferable.


### Part A: Fork and clone

First fork [this repository]({{ site.forking_workflow_exercise_url }})
into your namespace and then clone the fork to your computer.

Here is a pictorial representation of this part:

![]({{ site.baseurl }}/img/forking/forking-1.svg)

This is how it looks after we fork:

*central*: ![]({{ site.baseurl }}/img/forking/github-remote-01.svg)

*fork*: ![]({{ site.baseurl }}/img/forking/github-remote-01.svg)

- A fork is basically a (bare) clone.
- The upstream repo and the fork are in principle independent repositories.
- When forking we copy all commits, all branches.

After we clone the fork we have three in principle independent repositories:

*central*: ![]({{ site.baseurl }}/img/forking/github-remote-01.svg)

*fork*: ![]({{ site.baseurl }}/img/forking/github-remote-01.svg)

*local*: ![]({{ site.baseurl }}/img/forking/github-local-01.svg)


### Part B: Modify and commit

Before we do any modification, we create a new branch and switch to it - this is a good reflex and a good practice.
On the new branch add a file `group-X.py` where X is your group number or group name, e.g. `group-17.py`.
**Add only one file per group**.
(Why? - if you are adventurous, add both a file with the same name to see what happens)

This file should contain a function called `tweet()` which returns
a string of maximum 280 characters, for instance (don't worry, nothing gets out to Twitter):

```python
def tweet():
    return "please replace this boring sentence with something more fun"
```

The file `main.py` automatically calls all `tweet()` functions defined in files
`group*.py`. You do not need to edit `main.py`.

Test it before you commit your change:

```shell
$ python main.py

group 17 says: please replace this boring sentence with something more fun
```

If it works, commit the change. And here is a picture of what just happened:

*central*: ![]({{ site.baseurl }}/img/forking/github-remote-01.svg)

*fork*: ![]({{ site.baseurl }}/img/forking/github-remote-01.svg)

*local*: ![]({{ site.baseurl }}/img/forking/github-local-02.svg)


### Part C: Push your changes to the fork

Once you see your sentence correctly printed, commit and push the branch to your fork.

Don't worry
nothing gets out to Twitter but please mind that your changes will be public on
GitHub (but you can delete them later).

```shell
$ git push origin feature
```

*central*: ![]({{ site.baseurl }}/img/forking/github-remote-01.svg)

*fork*: ![]({{ site.baseurl }}/img/forking/github-remote-02.svg)

*local*: ![]({{ site.baseurl }}/img/forking/github-local-03.svg)


### Part D: File a pull request

Then file a pull request from the branch on your fork towards the master branch on the repository where you forked from.

Here is a pictorial representation for parts C and D:

![]({{ site.baseurl }}/img/forking/forking-2.svg)

A pull-request means: "please review my changes and if you agree, merge them with a mouse-click".

Once the pull-request is accepted, the change is merged:

*central*: ![]({{ site.baseurl }}/img/forking/github-remote-03.svg)

*fork*: ![]({{ site.baseurl }}/img/forking/github-remote-02.svg)

*local*: ![]({{ site.baseurl }}/img/forking/github-local-03.svg)

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

![]({{ site.baseurl }}/img/forking/forking-3.svg)

We will discuss two solutions:

#### Longer route

- Upstream repo receives other changes (other merged pull-requests)
- How do we get these changes to the forked repo?

```shell
$ git remote add upstream {{ site.forking_workflow_exercise_url }}.git
$ git fetch upstream
```

*central*: ![]({{ site.baseurl }}/img/forking/github-remote-03.svg)

*fork*: ![]({{ site.baseurl }}/img/forking/github-remote-02.svg)

*local*: ![]({{ site.baseurl }}/img/forking/github-local-04.svg)

```shell
$ git checkout master
$ git merge upstream/master
```

*central*: ![]({{ site.baseurl }}/img/forking/github-remote-03.svg)

*fork*: ![]({{ site.baseurl }}/img/forking/github-remote-02.svg)

*local*: ![]({{ site.baseurl }}/img/forking/github-local-05.svg)

```shell
$ git push origin master
```

*central*: ![]({{ site.baseurl }}/img/forking/github-remote-03.svg)

*fork*: ![]({{ site.baseurl }}/img/forking/github-remote-04.svg)

*local*: ![]({{ site.baseurl }}/img/forking/github-local-06.svg)


#### Shorter route

Remotes are aliases. We can use remote URLs directly.

Here we pull from the central repo and push to our fork:

```shell
$ git checkout master
$ git pull {{ site.forking_workflow_exercise_url }}.git master
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

---

<br>
<br>
<br>
![]({{ site.baseurl }}/img/forking/remote.jpg)
## Luke Skywalker: *You know, I did feel something. I could almost see the remote.*

## Ben Kenobi: *That's good. You've taken your first step into a larger world.*

(from Star Wars Episode IV - A New Hope)

<br>
<br>
<br>

---

## Discussion point: naming

In GitHub or BitBucket asking someone to bring code from a forked repo or
branch to the main repo is called a **pull request**. In GitLab it is called a
**merge request**. Which one do you feel is more appropriate and in which
context?

---

## Always create a feature branch

- Never commit to the branch you wish to submit the pull request towards.
- For each pull request create a new branch.

Motivation:

- Limits the risk that commits get accidentally appended to an open pull request.
- History-rewrite (rebased and/or squashed commits) on the central repository does not lead to a diverging local default branch.

---

## Code review

- You see what others are working on
- Collaborative learning
- OK if students and junior researchers review senior researchers
- Improves quality of the code
