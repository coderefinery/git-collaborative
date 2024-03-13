# How to contribute changes to repositories that belong to others

In this episode we prepare you to suggest and contribute changes to
repositories that belong to others. These might be open source projects that
you use in your work.

We will see how Git and services like GitHub or GitLab can be used to suggest
modification without having to ask for write access to the repository and
accept modifications without having to grant write access to others.


## Exercise

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


## Solution and walk-through

We will add this before the lesson.
