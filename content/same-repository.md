# Collaborating within the same repository

In this episode, we will learn how to collaborate within the same repository.
We will learn how to cross-reference issues and pull requests, how to review
pull requests, and how to use draft pull requests.

This exercise will form a good basis for collaboration that is suitable for
most research groups.


## Exercise

::::::{prereq} Exercise preparation
:::::{tabs}
  ::::{tab} Part of team/exercise room
  - Form not too large groups (4-5 persons).
  - Each group needs to appoint someone who will host the shared
    GitHub repository: the *maintainer*.
    This is typically the exercise lead (if available).  Everyone else
    is a *collaborator*.
  - The **maintainer** (one person per group) generates a new repository
    from the template <https://github.com/coderefinery/template-centralized-workflow-exercise>
    called `centralized-workflow-exercise` (There is no need to tick *"Include all branches"* for this exercise):
    :::{figure} img/centralized/generate_repo.png
    :alt: Screenshot of generating the exercise repository
    :width: 100%
    :::
  - Then **everyone in your group** needs their GitHub account to be added as collaborator to the exercise repository:
    - Collaborators give their GitHub usernames to their chosen maintainer.
    - Maintainer gives the other group members the newly created GitHub repository URL.
    - Maintainer adds participants as collaborators to their project (Settings -> Collaborators and teams -> Manage access -> Add people).
  ::::

  ::::{tab} Following on your own
  The instructors are the **maintainers**.  All watchers are
  **collaborators**.  This exercise is only possible during our
  livestream courses.
  The preparation typically happens already 1-2 days before.

  :::{admonition} If you have not requested access
  ---
  class: dropdown
  ---
  If you have not yet requested access, could you please [open an
  issue in this
  repository](https://github.com/cr-workshop-exercises/access-requests/issues/new/choose).
  Wait a
  minute for staff to add you, then wait for the invite email to arrive and
  accept the invitation from the email and "unwatch" repositories (below).
  :::

  **Choose only one to work with** (you must have requested access already, see above)

  - Not recorded:
    <https://github.com/cr-workshop-exercises/centralized-workflow-exercise>
    (this will not be shown on stream or recorded in our videos, but is public
    on the internet until it is deleted)
  - Recorded: <https://github.com/cr-workshop-exercises/centralized-workflow-exercise-recorded> (this will be shown on stream and recorded, **your username and comments may appear in the recorded video on YouTube**)
  ::::
:::::

- **Don't forget to accept the invitation**
  - Check <https://github.com/settings/organizations/>
  - Alternatively check the inbox for the email account you registered with
    GitHub. GitHub emails you an invitation link, but if you don't receive it
    you can go to your GitHub notifications in the top right corner. The
    maintainer can also "copy invite link" and share it within the group.

(unwatch)=

- **Watching and unwatching repositories**
  - Now that you are a collaborator, you get notified about new issues and pull
    requests via email.
  - If you do not wish this, you can "unwatch" a repository (top of
    the project page).
  - However, we recommend watching repositories you are interested
    in. You can learn things from experts just by watching the
    activity that come through a popular project.
  :::{figure} img/centralized/unwatch.png
  :alt: Unwatching a repository

  Unwatch a repository by clicking "Unwatch" in the repository view,
  then "Participating and @mentions" - this way, you will get
  notifications about your own interactions.
  :::
::::::

:::{exercise} Exercise: Collaborating within the same repository (25 min)

**Technical requirements**:
- If you create the commits locally: [Being able to authenticate to GitHub](https://coderefinery.github.io/installation/ssh/)

**What is familiar** from the previous workshop days:
- Cloning a repository ([previous lesson](https://coderefinery.github.io/git-intro/local-workflow/))
- Creating a branch ([previous lesson](https://coderefinery.github.io/git-intro/commits/))
- Committing a change on the new branch ([previous lesson](https://coderefinery.github.io/git-intro/commits/))
- Submit a pull request towards the main branch ([previous lesson](https://coderefinery.github.io/git-intro/merging/))

**What will be new** in this exercise:
- If you create the changes locally, you will need to **push** them to the remote repository.
- Learning what a protected branch is and how to modify a protected branch: using a pull request.
- Cross-referencing issues and pull requests.
- Practice to review a pull request.
- Learn about the value of draft pull requests.

**Exercise tasks**:
1. Open an issue where you describe the change you want to make. Note down the
   issue number since you will need it later.
1. Create a new branch.
1. Make a change to the recipe book on the new branch and in the commit
   cross-reference the issue you opened (see the walk-through below for how to do that).
1. Open a pull request towards the main branch.
1. Review somebody else's pull request and give constructive feedback.
1. Try to create a new branch with some half-finished work and open a draft
   pull request. Verify that the draft pull request cannot be merged since it
   is not meant to be merged yet.
:::


## Solution and walk-through

We will add this before the lesson.
