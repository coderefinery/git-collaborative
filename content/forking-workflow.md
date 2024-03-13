# How to contribute changes to repositories that belong to others

In this episode we prepare you to suggest and contribute changes to
repositories that belong to others. These might be open source projects that
you use in your work.

We will see how Git and services like GitHub or GitLab can be used to suggest
modification without having to ask for write access to the repository and
accept modifications without having to grant write access to others.


## Exercise

::::::{prereq} Exercise preparation
:::::{tabs}
  ::::{tab} Part of team/exercise room

  **Maintainer (team lead)**:
  - Create an exercise repository by
    [generating from a template](https://help.github.com/en/articles/creating-a-repository-from-a-template)
    using this template: <https://github.com/coderefinery/template-forking-workflow-exercise>
    called `forking-workflow-exercise`
  - In this case we **do not add collaborators** to the repository (this is the point of this example).
  - Share the link to the newly created repository with your group.

  **Learners in exercise team**: Fork the newly created repository (not the
  "coderefinery" one) and then **clone your fork** (if you wish to work locally).
  ::::

  ::::{tab} Following on your own
  The instructors are the **maintainers**.  All watchers are
  **collaborators**.

  We create(d) these the day before hopefully.  **Choose only one to
  work with**:
  - Not recorded:
    <https://github.com/cr-workshop-exercises/forking-workflow-exercise> (this
    will not be shown on stream or recorded in our videos, but is be public on
    the internet until it is deleted)
  - Recorded:
    <https://github.com/cr-workshop-exercises/forking-workflow-exercise-recorded>
    (this will be shown on stream and recorded, **your username and comments
    may appear in the recorded video on YouTube**)

  Here we don't need your GitHub usernames because the point of this exercise
  is to show that we can collaborate without granting write permissions.

  Learners following on their own: Fork one of these two repositories
  and then **clone your fork** to your computer (if you wish to work locally).
  ::::
:::::
::::::

:::{exercise} Exercise: Collaborating within the same repository (25 min)

**Technical requirements**:
- If you create the commits locally: [Being able to authenticate to GitHub](https://coderefinery.github.io/installation/ssh/)

**What is familiar** from the previous workshop days:
- Forking a repository ([previous lesson](https://coderefinery.github.io/git-intro/browsing/))
- Creating a branch ([previous lesson](https://coderefinery.github.io/git-intro/commits/))
- Committing a change on the new branch ([previous lesson](https://coderefinery.github.io/git-intro/commits/))
- Opening and merging pull requests ([previous lesson](https://coderefinery.github.io/git-intro/merging/))

**What will be new** in this exercise:
- Opening a pull request towards the upstream repository.
- Pull requests can be coupled with automated testing.
- Learning that your fork can get out of date.
- After the pull requests are merged, updating your fork with the changes.
- Learn how to approach other people's repositories with ideas, changes, and requests.

**Exercise tasks**:
1. Open an issue in the upstream exercise repository where you describe the
   change you want to make. Take note of the issue number.
1. Create a new branch in your fork of the repository.
1. Make a change to the recipe book on the new branch and in the commit cross-reference the issue you opened.
   See the walk-through below for how to do this.
1. Open a pull request towards the upstream repository.
1. Team leaders will merge the pull requests. For individual participants, the
   instructors and workshop organizers will review and merge the pull requests.
   During the review, pay attention to the automated test step (here for
   demonstration purposes, we test whether the recipe contains an ingredients
   and an instructions sections).
1. After few pull requests are merged, update your fork with the changes.
1. Check that in your fork you can see changes from other people's pull requests.
:::


## Help and discussion


### Opening a pull request towards the upstream repository

We have learned in the previous episode that pull requests are always from
branch to branch. But the branch can be in a different repository.

When you open a pull request in a fork, by default GitHub will suggest to
direct it towards the default branch of the upstream repository.

This can be changed and it should always be verified, but in this case this is
exactly what we want to do, from fork towards upstream:
:::{figure} img/forking-workflow/pull-request-form.png
:width: 100%
:class: with-border
:alt: Screenshot of a pull request from fork towards upstream
::::


### Pull requests can be coupled with automated testing

We added an automated test here just for fun and so that you see that this is
possible to do.

In this exercise, the test is silly. It will check whether the recipe contains
both an ingredients and an instructions section.

In this example the test failed:
:::{figure} img/forking-workflow/all-checks-failed.png
:width: 60%
:class: with-border
:alt: Screenshot of a failed test in a pull request
::::

Click on the "Details" link to see the details of the failed test:
:::{figure} img/forking-workflow/check-details.png
:width: 60%
:class: with-border
:alt: Screenshot of details why the test failed
::::

**How can this be useful?**
- The project can define what kind of tests are expected to pass before a pull
  request can be merged.
- The reviewer can see the results of the tests, without having to run them
  locally.

**How does it work?**
- We added a [GitHub Actions workflow](https://github.com/coderefinery/recipe-book-template/blob/main/.github/workflows/check-recipes.yml)
  to automatically run on each push or pull request towards the `main` branch.

What tests or steps can you image for your project to run automatically with
each pull request?


### How to update your fork with changes from upstream

This used to be difficult but now it is two mouse clicks.

Navigate to your fork and notice how GitHub tells you that your fork is behind.
In my case, it is 9 commits behind upstream. To fix this, click on "Sync fork"
and then "Update branch":
:::{figure} img/forking-workflow/sync-fork.png
:width: 80%
:class: with-border
:alt: Screenshot on GitHub fork page showing that the fork is behind
::::

After the update my "branch is up to date" with the upstream repository:
:::{figure} img/forking-workflow/fork-after-update.png
:width: 80%
:class: with-border
:alt: Screenshot on GitHub after fork has been updated
::::


### How to approach other people’s repositories with ideas, changes, and requests

**Contributing very minor changes**
- Clone or fork+clone repository
- Create a branch
- Commit and push change
- Open a pull request or merge request

**If you observe an issue and have an idea how to fix it**
- Open an issue in the repository you wish to contribute to
- Describe the problem
- If you have a suggestion on how to fix it, describe your suggestion
- Possibly **discuss and get feedback**
- If you are working on the fix, indicate it in the issue so that others know that somebody is working on it and who is working on it
- Submit your fix as pull request or merge request which references/closes the issue

:::{admonition} Motivation
- **Inform others about an observed problem**
- Make it clear whether this issue is up for grabs or already being worked on
:::

**If you have an idea for a new feature**
- Open an issue in the repository you wish to contribute to
- In the issue, write a short proposal for your suggested change or new feature
- Motivate why and how you wish to do this
- Also indicate where you are unsure and where you would like feedback
- **Discuss and get feedback before you code**
- Once you start coding, indicate that you are working on it
- Once you are done, submit your new feature as pull request or merge request which references/closes the issue/proposal

:::{admonition} Motivation
- **Get agreement and feedback before writing 5000 lines of code** which might be rejected
- If we later wonder why something was done, we have the issue/proposal as
  reference and can read up on the reasoning behind a code change
:::



## Summary

- This forking workflow lets you propose changes to repositories for
  which *you have no access*.
- This is the way that much modern open-source software works.
- You can now contribute to any project you can view.
