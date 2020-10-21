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

## Centralized workflow

### Meaning of "central" in a distributed version control

![The GitHub Octocat]({{ site.baseurl }}/img/forking/github_octocat.jpeg)

Git implements a **distributed** version control.
This means that any type of repository links that you can think of can be
implemented - not just "everything connects to one central server".

In Git, all repositories are equivalent but we typically we consider one repository
as the main development line and this is marked as "central".
The "central" is a role, not a technical difference.

In this episode, we will explore the usage of a **centralized workflow** for collaborating online on a project
**within one repository**.


### Centralized layout

![]({{ site.baseurl }}/img/forking/centralized.svg)

Features:

- Typically all developers have both read and write permissions (double-headed arrows).
- Suited for cases where **all developers are in the same group or organization or project**.
- **Everybody who wants to contribute needs write access**.
- Good idea to write-protect the main branch (typically `master` or `main`).

Real life examples:

- Within the CodeRefinery team we mostly use this approach: [https://github.com/coderefinery](https://github.com/coderefinery)
- [https://github.com/ropensci/plotly](https://github.com/ropensci/plotly)

---

## Centralized workflow exercise

In this exercise we will practice collaborative centralized workflow in small
groups.  We'll discuss how this leads to code review and discuss a number of
typical pitfalls.


> ## Exercise preparation
>
> - We form small groups (4-5 persons).
> - Each group needs to appoint someone who will host the shared GitHub repository: *an administrator*.
> - For online teaching, use breakout rooms.
> - **One person per group (administrator)** generates a new repository
>   from the template [template-centralized-workflow-exercise](https://github.com/coderefinery/template-centralized-workflow-exercise)
>   called `centralized-workflow-exercise` (There is no need to tick *"Include all branches"* for this exercise):
> <img src="{{ site.baseurl }}/img/centralized/generate_repo.png" width="700"/>
>
> - Then **everyone in your group** needs their GitHub account to be added as collaborator to the exercise repository:
>   - Participants give their GitHub usernames to their chosen administrator (in their respective group).
>   - Administrator gives the other group members the newly created GitHub repository URL.
>   - Administrator adds participants as collaborators to their project (Settings → Manage Access → Invite a collaborator).
>   - Group members need to accept the invitation (GitHub emails you an invitation link).
> - You can use this template to share this information in the collaborative document:
>
> ```
> # Group N
>
> - administrator: someuser
> - exercise URL: https://github.com/someuser/centralized-workflow-exercise
> - collaborators:
>   - anotheruser
>   - yetanotheruser
>   - myusername
>   - otherusername
> ```
{: .prereq}

> ## Watching and unwatching repositories
>
> - Now that you are a collaborator, you get notified about new issues and pull
>   requests via email.
> - If you do not wish this, you can "unwatch" a repository (top of the project page).
> - However, we recommend watching repositories you are interested in. You can learn things from experts just by
>   watching the activity that come through.
{: .callout}

> ## Exercise description
>
> - Helper prepares an exercise repository (see above) - this will take 10 minutes or so.
> - The exercise group works on steps 1-8 (15-20 minutes).
> - After step 8 you can return to the main room. Please ask questions.
> - We do step 9 and 10 together (instructor demonstrates, and everybody follows along in their repositories).
> - Before we start with the exercise, instructor mentions all steps and explains what happens during a `git clone`.
{: .challenge}


#### 1. Clone your administrator's group repository

```
$ git clone {{ site.centralized_workflow_exercise_url }}.git centralized-workflow-exercise
```

Where you replace `coderefinery` by the namespace of the repository administrator.

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

Try to find out where this repository was cloned from using `git remote -v`.


#### 3. Create a branch `yourname-somefeature` pointing at your commit

Create a branch from the current `master`:

```
$ git branch yourname-somefeature
$ git checkout yourname-somefeature
```

The `yourname-` prefix has no special meaning here (not like `origin/`): it is just part of a
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
$ git push origin -u yourname-somefeature
```

Can we leave out the `-u`?


#### 7. Browse the network of branches and commits

After you have pushed your branch and other participants have too, browse the
network of branches and commits and discuss with others what you see.


#### 8. Submit a pull request

Submit a pull request from your branch towards the `master` branch.
Do this through the web interface.

A pull-request means: "please review my changes and if you agree, merge them with a mouse-click". In a popular project, it means that anyone can
contribute with *almost no work* on the maintainer's side - a big win.


#### 9. Discuss and accept pull requests

**We do this step together on the main screen (in the main room)**. The instructor shows a submitted
pull request, discusses what features to look at, and how to discuss and review.

At the same time, helpers can review open pull requests from their exercises groups.

> ## Code review and protected branches
>
> - Pull requests are like change proposals.
> - We recommend that pull requests are reviewed by someone else in your group.
> - In our example everyone has write access to the "central" repository.
> - A good setting is to make the `master` or `main` branch **protected** and all changes to it have to go
>   through code review.
> - Centralized workflow with protected branches is a good setup for many projects.
{: .callout}

Once the pull-request is accepted, the change is merged:

*central*: ![]({{ site.baseurl }}/img/centralized/06-remote.svg)

*local*: ![]({{ site.baseurl }}/img/centralized/04-local.svg)

Finally also discuss {{ site.centralized_workflow_exercise_url }}/network.


#### 10. Update your local copy

Your branch `yourname-somefeature` is not needed anymore but more importantly, you need to sync your local copy:
Everybody needs to do this step in their exercise repository but we do this together in the main room
so that we can discuss this step and ask questions.

```
$ git checkout master
$ git pull origin master
```
*central*: ![]({{ site.baseurl }}/img/centralized/06-remote.svg)

*local*: ![]({{ site.baseurl }}/img/centralized/07-local.svg)

---

> ## Exercise/discussion: Why did we create a feature branch `yourname-somefeature`?
>
> This exercise is done in groups of 4-5 persons and can be done through a discussion only.
> Whenever we make update to our repository, we create a new branch and make pull-request. Let's now imagine that everyone in your group makes a new change (create a new file) but without creating a new branch.
>
> 1. You all create a new file in the master branch, stage and commit your change locally.
> 2. Try to push the change to the upstream repository:
>
> ```
> $ git push origin master
> ```
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
> - The push only worked for one participant.
> - Discuss why push for everybody else in this group was rejected?
{: .challenge}

> ## Discussion: How to make changes to remote branches
>
> We can create a local branch `somefeature` tracking `origin/somefeature`:
>
> ```shell
> $ git checkout -b somefeature origin/somefeature
> ```
>
> If there is no local branch `somefeature` and there is a remote branch `origin/somefeature`, then this is enough:
>
> ```shell
> $ git checkout somefeature
> ```
>
> Once we track a remote branch, we can pull from it and push to it:
>
> ```shell
> $ git pull origin somefeature
> $ git push origin somefeature
> ```
>
> We can also delete remote branches:
>
> ```shell
> $ git push origin --delete somefeature
> ```
{: .discussion}

> ## Creating pull requests from the command line
>
> There are several possibilties:
> - <https://cli.github.com/>
> - <https://hub.github.com/>
> - <https://github.com/NordicHPC/git-pr>
{: .callout}

> ## How you can find out in which repositories you are a collaborator
>
> Visit <https://github.com/settings/repositories> where you will see
> an overview of all repositories you have write access to.
{: .callout}

> ## GitHub/GitLab organizations
>
> - Projects often start under a personal namespace.
> - If you want the project to live beyond the interest or work time of one person,
>   one can share projects under an "organization".
> - You can then invite collaborators to an organization.
> - This is what we do in the CodeRefinery project: <https://github.com/coderefinery>
{: .callout}
