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



### Forking layout

![]({{ site.baseurl }}/img/forking/forking-overview.svg)

In the **forking layout**, again we call one repository the "central"
repository but people push to **forks** (their own copies of the
repository on GitHub).

Features:

- Most developers have only read access to the main project.
- For a public repository everybody has read access.
- Only very few people (the maintainers) have write access.
- Typically nobody pushes directly to the central repo.
- Code review can be coupled with automated testing.
- Central repo and the forks typically reside in the "cloud".
- Naturally grows out the centralized model once more people begin
  contributing.

Advantages:

- Code is integrated via code review (during pull/merge request).
- Maintainer has full control over what goes in.
- Allows contributions from people you don't know yet (in practice not possible in centralized layout).
- Structurally helps to implement peer review in coding (code review).

Disadvantages:

- Learning curve: we need to deal at least with two remotes (fork and central repo).
- Introduces additional steps (to e.g. update the fork).

Real life examples:

- NumPy: [https://numpy.org/devdocs/dev/index.html](https://numpy.org/devdocs/dev/index.html)
- [https://github.com/jupyterlab/jupyterlab](https://github.com/jupyterlab/jupyterlab)

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
$ git remote add upstream https://github.com/project/project.git
$ git remote add downstream https://github.com/userX/project.git
```

We synchronize remotes via the local clone.

To see all remotes:

```shell
$ git remote --verbose
```

---

## Exercise: practice collaborative forking workflow

In this exercise, we make a fork, push to that fork, and make a pull
request to the "central" repository. Later we will exercise updating the individual forks
after changes from all participants have been merged.

As an example we will collaboratively develop a cookbook for taco recipes,
inspired by [tacofancy](https://github.com/sinker/tacofancy).

We recommend that you discuss with your neighbor/group throughout the exercise.

Objectives:

- Learn how to fork, modify the fork, and file a pull request towards the forked repo.
- Learn how to update your fork with upstream changes.

We will do this exercise on [GitHub](https://github.com) but also
[GitLab](https://gitlab.com) and [Bitbucket](https://bitbucket.org) allow
similar workflows and basically everything that we will discuss is transferable.

<div class="alert alert-dismissible alert-warning">
  <button type="button" class="close" data-dismiss="alert">&times;</button>
  <h4 class="alert-heading">We will work with a new repository for this exercise!</h4>
  <p>
    For this exercise we will fork a different repository compared to earlier today.
    Please step out of the repository and check that you fork the <b>forking</b>-workflow-exercise.
  </p>
</div>


### Part A: Fork and clone

In the **groups/breakout-rooms**, one person like the helper, do a necessary preparatory step. The person creates a repository
from a template in their GitHub user space. We do not use the templates directly but
[generate exercises from them](https://help.github.com/en/articles/creating-a-repository-from-a-template).
Here is the template for forking workflow exercise:
[https://github.com/coderefinery/template-forking-workflow-exercise](https://github.com/coderefinery/template-forking-workflow-exercise)

Write the link to the newly created repository in the shared document (hackmd)
under a subsection with your group number as heading.

The others in **the group** fork the helper's newly created repository. The group members then clone the fork ---
the repository which is created their GitHub user space --- to their own computer.

For the ones of you who follow the **main** room, you first fork [this repository]({{ site.forking_workflow_exercise_url }})
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


### Part B: Open an "issue" as a change proposal

Before we start any coding, open a new "Issue" on the central repository as a
"proposal" where you describe your idea for a recipe with the possibility to
collect feedback from others. After creating this issue note the issue number.
We will later refer to this issue number.

Discuss with your neighbor why it can be useful to open an issue before
starting the actual coding.


### Part C: Modify and commit

Before we do any modification, we create a new branch and switch to it: this is
a good reflex and a good practice. Choose a branch name which is descriptive of
its content.

On the new branch create a new file which will hold your recipe,
for instance `traditional_coderefinery_tacos.md` (but change the name). You can get inspired
[here](https://github.com/sinker/tacofancy/tree/master/full_tacos). Hopefully we all use different
file names, otherwise we will experience conflicts later (which is also interesting!).

There is also a file called `test.py` which will automatically verify whether your recipe contains the string
"taco" (case insensitive). This is there to slowly introduce us to automated testing.

Once you are happy with your recipe, commit the change and in your commit
message reference the issue which you have opened earlier with "this is my
commit message; closes #N" (use a more descriptive message and replace N by the
actual issue number).

And here is a picture of what just happened:

*central*: ![]({{ site.baseurl }}/img/forking/github-remote-01.svg)

*fork*: ![]({{ site.baseurl }}/img/forking/github-remote-01.svg)

*local*: ![]({{ site.baseurl }}/img/forking/github-local-02.svg)


### Part D: Push your changes to the fork

Now push your new branch to your fork. Your branch is probably called something else than "feature". Also verify where
"origin" points to.

```shell
$ git push origin feature
```

*central*: ![]({{ site.baseurl }}/img/forking/github-remote-01.svg)

*fork*: ![]({{ site.baseurl }}/img/forking/github-remote-02.svg)

*local*: ![]({{ site.baseurl }}/img/forking/github-local-03.svg)


### Part E: File a pull request

Then file a pull request from the branch on your fork towards the master branch on the repository where you forked from.

Here is a pictorial representation for parts D and E:

![]({{ site.baseurl }}/img/forking/forking-2.svg)

A pull-request means: "please review my changes and if you agree, merge them with a mouse-click".

Once the pull-request is accepted, the change is merged:

*central*: ![]({{ site.baseurl }}/img/forking/github-remote-03.svg)

*fork*: ![]({{ site.baseurl }}/img/forking/github-remote-02.svg)

*local*: ![]({{ site.baseurl }}/img/forking/github-local-03.svg)

Wait here until we integrate all pull requests into the central repo
together on the big screen.

Observe how the issues automatically close after the pull requests are merged
(provided the commit messages contain [the right keywords](https://help.github.com/en/articles/closing-issues-using-keywords)).


> ## (Optional) Exercise: try to send a conflicting pull request
>
> If you complete parts A-E much earlier than others, try to send another pull request
> where you anticipate a conflict with your first pull request.
{: .challenge}

> ## (Optional) Exercise: practice making changes to your pull request
>
> You can do that by pushing new commits to the branch where you sent the pull
> request from. Observe how they end up added to your pull request.
{: .challenge}


### Part F: Update your fork

We do this part **after the contributions from all participants have been integrated**.

Once this is done, practice to update your forked repo with the upstream
changes and verify that you got the files created by other participants.

Make sure that the contributions from other participants are not only on your local repository
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

> ## (Optional) Exercise: squash merge a pull request
>
> If you complete this exercise much earlier than others, pair up with somebody,
> create a new repository, fork it, and send a pull request with several
> small commits. On the other computer accept these with "Squash and merge" and later compare the source
> and target repositories/branches how they differ after the small commits got squashed into one.
{: .challenge}

---

<br>
<br>
<br>
![]({{ site.baseurl }}/img/forking/remote.jpg)
## Luke Skywalker: *You know, I did feel something. I could almost see the remote.*

## Ben Kenobi: *That's good. You've taken your first step into a larger world.*

(from Star Wars Episode IV - A New Hope)

---

> ## Discussion
>
> ### Naming
>
> In GitHub or BitBucket asking someone to bring code from a forked repo or
> branch to the main repo is called a **pull request**. In GitLab it is called a
> **merge request**. Which one do you feel is more appropriate and in which
> context?
>
> ### Always create a feature branch
>
> - Never commit to the branch you wish to submit the pull request towards.
> - For each pull request create a new branch.
>
> Motivation:
> - Limits the risk that commits get accidentally appended to an open pull request.
> - History-rewrite (rebased and/or squashed commits) on the central repository does not lead to a diverging local default branch.
>
> See also [this
> blogpost](https://blog.jasonmeridth.com/posts/do-not-issue-pull-requests-from-your-master-branch/)
> for an explanation.
>
> ### Why code review
>
> - You see what others are working on
> - Collaborative learning
> - OK if students and junior researchers review senior researchers
> - Improves quality of the code
{: .discussion}
