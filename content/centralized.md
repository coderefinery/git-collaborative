# Centralized workflow

```{objectives}
- Understand how to collaborate using a centralized workflow.
- Understand the difference between local branch, origin/branch, and remote branch.
```

```{instructor-note}
- 20 min teaching
- 40 min exercises
```


## Meaning of "central" in a distributed version control

In this episode, we will explore the usage of a **centralized workflow** for collaborating online on a project
**within one repository on Github**.  This means that everyone has
access to that **central repository** - convenient (but doesn't scale to a huge
project).

In {doc}`the next section <distributed>`, we will see that Git is
**distributed** version control.
This means that any type of repository links that you can think of can be
implemented - not just "everything connects to one central server".



## Centralized layout

```{figure} img/forking/centralized.svg
:alt: Centralized layout
:width: 50%

Centralized layout. **Red** is the repository on GitHub.  **Blue** is
where all contributors work on their own computers.
```

Features:

- Typically all developers have both read and write permissions (double-headed arrows).
- Suited for cases where **all developers are in the same group or organization or project**.
- **Everybody who wants to contribute needs write access**.
- Good idea to write-protect the main branch (typically `master` or `main`).

Real life examples:

- Within the CodeRefinery team we mostly use this approach: [https://github.com/coderefinery](https://github.com/coderefinery)
- [https://github.com/ropensci/plotly](https://github.com/ropensci/plotly)


## Exercise preparation

In this exercise we will practice collaborative centralized workflow in
groups.  An **administrator** will create a repository, and
**collaborators** will contribute to it.  We'll discuss how this leads
to code review and discuss a number of typical pitfalls.

``````{prereq} Exercise preparation
`````{tabs}
  ````{tab} Part of team/exercise room
  - In-person: We form small groups (4-5 persons). Video: use breakout rooms.
  - Each group needs to appoint someone who will host the shared
    GitHub repository: *an administrator*.
    This is typically the exercise lead (if available).  Everyone else
    is a *collaborator*.
  - **Administrator** (one person per group) generates a new repository
    from the template <https://github.com/coderefinery/template-centralized-workflow-exercise>
    called `centralized-workflow-exercise` (There is no need to tick *"Include all branches"* for this exercise):
    ```{figure} img/centralized/generate_repo.png
    :alt: Screenshot of generating the exercise repository
    :width: 100%
    ```
  - Then **everyone in your group** needs their GitHub account to be added as collaborator to the exercise repository:
    - Collaborators give their GitHub usernames to their chosen administrator (in their respective group, in online workshops you can use the Zoom chat for private communication within the breakout room).
    - Administrator gives the other group members the newly created GitHub repository URL.
    - Administrator adds participants as collaborators to their project (Settings → Manage Access → Invite a collaborator).
  ````

  ````{tab} Participating via stream
  The instructors are the **administrators**.  All watchers are
  **collaborators**.  This exercise is only possible during our
  livestream courses - otherwise we will not grant you access and the
  repositories may not exist.

  ```{admonition} If you have not requested access (our emails asked yesterday)
  ---
  class: dropdown
  ---
  If you have not yet requested access, could you please [open an
  issue in this
  repository](https://github.com/cr-workshop-exercises/centralized-workflow-exercise/issues/new).
  Give any title like "please add me" and then click submit.  Wait a
  minute for staff to add you, then wait for the invite email to arrive and *accept the invitation from the email*.
  ```

  We create(d) these the day before hopefully.  **Choose only one to
  work with.  You must have requested access already, see above**:

  - Not recorded: <https://github.com/cr-workshop-exercises/centralized-workflow-exercise> (this will not be shown on stream or recorded in our videos, but is be public on the Internet until it is deleted)
  - Recorded: <https://github.com/cr-workshop-exercises/centralized-workflow-exercise-recorded> (this will be shown on stream and recorded, **your username and comments may appear in the recorded video on YouTube**)

  The preparation typically happens already the day before where we ask
  participants to send us their usernames and we add them all.
  ````
`````

- **Don't forget to accept the invitation**
  - Check <https://github.com/settings/organizations/>
  - Alternatively check the inbox for the email account you registered with
    GitHub. GitHub emails you an invitation link, but if you don't receive it
    you can go to your GitHub notifications in the top right corner. The
    administrator can also "copy invite link" and share it within the group.

(unwatch)=

- **Watching and unwatching repositories**
  - Now that you are a collaborator, you get notified about new issues and pull
    requests via email.
  - If you do not wish this, you can "unwatch" a repository (top of
    the project page).
    - If you are a livestreamer, you will need to unwatch both of the
      two above repositories under the "Participating via stream" tab
      above.
  - However, we recommend watching repositories you are interested
    in. You can learn things from experts just by watching the
    activity that come through a popular project.
  ```{figure} img/centralized/unwatch.png
  :alt: Unwatching a repository

  Unwatch a repository by clicking "Unwatch" in the repository view,
  then "Participating and @mentions" - this way, you will get
  notifications about your own interactions.
  ```

``````


## Exercise: Part 1 - creating a pull request

```{exercise} Centralized-1: Clone a repository, add a file, push changes as a branch, and create a pull request
- Before we start with the exercise, instructor points to the preparation (above).
- The exercise group works on steps A-H (15-20 minutes).
- **After step H you can either return to the main room or take a break or help
  others**. Please ask questions both during group work and in the collaborative document.  There
  are also optional exercises.

The exercise is steps A-H below.
```

```{callout} Hint for breakout rooms
If the helper in the room is the one who sets up the central repository, they
cannot easily demostrate the steps via screen-sharing as the repository's owner. A
good alternative is to have one of the learners screen-share and get advice on the
steps from other learners and helpers!
```

Before and after each action you take, run the following informational
commands.  Carefully observe what happens, especially in `git graph`:

- `git graph` - almost every time
- `git status` - when you modify files


### Step A. Clone your administrator's group repository

```console
$ git clone <repository-url> centralized-workflow-exercise
```

Where `<repository-url>` is the repository created by the exercise administrator.

This is a representation of what happens when you clone:

```{figure} img/centralized/01-remote.svg

remote or central
```

```{figure} img/centralized/01-local.svg

local
```

Here and in what follows, "c1" is a commit, "b1" etc. are commits on side branches
and "m1" is a merge commit.

- We clone the entire history, all branches, all commits. In our case, we have one branch (we did not include *all branches* when creating our repository from template) and we have only one commit (*initial commit*).
- `git clone` creates pointers `origin/master` so you can see the branches of the origin.
- `origin` refers to where we cloned from, try: `git remote -v`.
- `origin` is a shortcut for the full URL.
- `origin/master` is a read-only pointer.
- The branches starting with `origin/` only move during `git pull` or `git fetch` or `git push`.
- Only `git pull` or `git fetch` or `git push` require network.
- All other operations are local operations.


### Step B. Change directory into the newly created directory

```console
$ cd centralized-workflow-exercise
```

Try to find out where this repository was cloned from using `git remote -v`.


### Step C. Create a branch `yourname-somefeature` pointing at your commit

Create a branch from the current `master`. Also adapt "yourname-somefeature" to a better name:

```console
$ git branch yourname-somefeature master
$ git checkout yourname-somefeature
```

The `yourname-` prefix has no special meaning here (not like `origin/`): it is just part of a
branch name to indicate who made it.


### Step D. Create a file with a unique name, e.g.: `yourusername.txt`

In this file share your favourite cooking recipe or haiku or Git trick or whatever.


### Step E. Stage and commit the change

```console
$ git add yourusername.txt
$ git commit
```

```{figure} img/centralized/01-remote.svg

remote or central
```

```{figure} img/centralized/04-local.svg

local (read figure left to right)
```


### Step F. Push your change as a new branch

```console
$ git push origin -u yourname-somefeature
```

````{admonition} If you get a password request for https://github.com when you try to push
---
class: warning, dropdown
---
Probably you cloned with the HTTPS URL (see `git remote -v` to
confirm).  You can change this to SSH by going to the repository page,
clicking "Code", copying the SSH url (starts with `git@github.com:`),
and then updating the URL with:

```console
$ git remote set-url origin <repository-url>
```
````


```{figure} img/centralized/04-remote.svg

remote or central (read figure left to right)
```

```{figure} img/centralized/04-local.svg

local (read figure left to right)
```

```{note}
**Meaning of `-u` | `--set-upstream`**

The `-u` or `--set-upstream` will connect the local branch with the newly created upstream/remote branch
and track it. This has the following advantages:
- If you from here on only type `git push` or `git pull` without branchname, Git will know what branch you
  refer to (depending also on your Git configuration). However, we still recommend to explicitly type where
  you want to push/pull to/from and which branch explicitly.
- When you type `git status`, Git will inform you whether your local branch is ahead or behind the upstream branch
  that it tracks.

However, also without the `-u` this step and the rest of the exercise will
work. The fact that the local and remote branch are not connected is not a
problem if you explicitly type out the remote and branch name every time.
```


### Step G. Browse the network of branches and commits

After you have pushed your branch and other participants have too, browse the
network of branches and commits (on GitHub click on Insights -> Network) and
discuss with others what you see.


### Step H. Submit a pull request

Submit a pull request from your branch towards the `master` branch.
Do this through the web interface.

There are **several options to open a pull request**:
- Follow the link printed to terminal output when git-pushing a branch to GitHub/GitLab
- Visit the GitHub repository in the browser after pushing the branch and click on the green button "Compare & pull request"
- Click on "Pull requests" on top of the GitHub repository and either "Compare & pull request" or "New pull request"
- Click on "Branches" and then "New pull request" from the respective branch.

Meaning of a pull request: think of it as change proposal. In a popular project, it means that anyone can
contribute with *almost no work* on the maintainer's side - a big win.


## Exercise: Part 2 - code review and merging changes

```{exercise} Centralized-2: Merge the pull requests (together)
- **We do step 2A and 2B together** (instructor demonstrates, and everybody follows along in their repositories).
```

```{instructor-note}
At this stage it might be good to show how to submit and how to review a pull request.
- When co-teaching change roles and switch screenshares also.
- Discuss what you look at when submitting.
- Discuss what you look at when reviewing.
```


### Step 2A. Discuss and accept pull requests

**We do this step together on the main screen (in the main room) or on stream**. The instructor shows a submitted
pull request, discusses what features to look at, and how to discuss and review.

At the same time, helpers can review open pull requests from their exercises groups.

```{discussion}
**Naming**

- In GitLab or BitBucket these are named **merge requests**, not **pull requests**.
- Which one do you feel is more appropriate and in which
  context? (The name **pull request** may make more sense in the forking workflow: next episode).
- It can be useful to think of them as **change proposals**.

**Pull requests are from branch to branch**

- They originate from a source branch and are directed towards a branch.
- Not from commit to branch.
- Pull requests create new commits on the target branch.
- They do not create new branches.

**Pull requests can be used for code review**

- Pull requests are like change proposals.
- We recommend that pull requests are reviewed by someone else in your group.
- In our example everyone has write access to the "central" repository.

**Protected branches**

- A good setting for large projects is to make the `master` or `main` branch **protected** and all changes to it have to go
  through code review.
- Centralized workflow with protected branches is a good setup for many projects.

**Code review**

- You see what others are working on
- Collaborative learning
- OK if students and junior researchers review senior researchers
- Improves quality of the code

**Read more**

- This is a great resource: [Practical git PRs for small teams](https://scicomp.aalto.fi/scicomp/practical-git-prs/)
```

Once the pull-request is accepted, the change is merged:

```{figure} img/centralized/06-remote.svg

remote or central
```

```{figure} img/centralized/04-local.svg

local
```

Finally also discuss the "network" on GitHub.

```{instructor-note}
At this stage demonstrate how to suggest small changes to pull/merge requests:
- [GitHub](http://haacked.com/archive/2019/06/03/suggested-changes/)
- [GitLab](https://docs.gitlab.com/ee/user/project/merge_requests/reviews/suggestions.html)
```


### Step 2B. Update your local copy

Your branch `yourname-somefeature` is not needed anymore but more importantly,
you need to sync your local copy: Everybody needs to do this step in their
exercise repository but we do this together in the main room so that we can
discuss this step and ask questions.

```console
$ git checkout master
$ git pull origin master
```

```{figure} img/centralized/06-remote.svg

remote or central
```

```{figure} img/centralized/07-local.svg

local
```

## Optional exercises

```{exercise} (optional) Centralized-3: Cross-referencing issues using "#NNN"
We will submit another change by a pull request but this time we will **first create an issue**.

1. Open an issue on GitHub and describe your idea for a change. This gives
   others the chance to give feedback/suggestions. **Note the issue number**, you
   will need it in step 3.
2. Create a new branch and switch to it.
3. On the new branch create a commit and in the commit message write what you
   did, but also add that this "closes #1" (if the issue that you refer to had the number
   1).
4. Push the branch and open a new pull request. If you forgot to refer to the
   issue number in step 3, you can still refer to it in the pull request
   form.
5. Note how now commits, pull requests, and issues can be cross-referenced by including `#NNN`.
6. Notice how after the pull request is merged, the issue gets automatically
   closed.  This only happens for certain keywords like `closes` or `fix`.
7. Discuss the value of cross-referencing them and of auto-closing issues
   with commits or pull requests.
```

````{exercise} (optional) Centralized-4: Why did we create a feature branch "yourname-somefeature"? (exercise/discussion)
  This exercise is done in groups of 4-5 persons and can be done through a discussion only.

  Pushing directly to the main branch is perfectly fine for simple personal projects -
  the pull-request workflows covered here are for larger projects or for collaborative development.
  Guidelines for simpler workflows are given in the
  [how much git is necessary?](https://coderefinery.github.io/git-intro/level/) episode of the git-intro lesson.

  In collaborative development, whenever we update our repository we create a new branch
  and create a pull-request. Let's now imagine that everyone in your group makes a new change (create a new file)
  but without creating a new branch.

  1. You all create a new file in the master branch, stage and commit your change locally.
  2. Try to push the change to the upstream repository:

     ```console
     $ git push origin master
     ```
     You probably see something like this:

     ```console
     $ git push

     To https://github.com/user/repo.git
      ! [rejected]        master -> master (non-fast-forward)
     error: failed to push some refs to 'https://github.com/user/repo.git'
     To prevent you from losing history, non-fast-forward updates were rejected
     Merge the remote changes (e.g. 'git pull') before pushing again.  See the
     'Note about fast-forwards' section of 'git push --help' for details.
     ```

  - The push only worked for one participant.
  - Discuss why push for everybody else in this group was rejected?

  ```{solution}
  The push for everyone except one person fails because they are missing one
  commit in their local repository that exists on the remote. They will first
  need to pull the remote changes before pushing their own, which will usually
  result in a merge commit.
  ```
````

````{discussion} Discussion: How to make changes to remote branches
  We can create a local branch `somefeature` tracking `origin/somefeature`:

  ```console
  $ git checkout -b somefeature origin/somefeature
  ```

  If there is no local branch `somefeature` and there is a remote branch `origin/somefeature`, then this is enough:

  ```console
  $ git checkout somefeature
  ```

  The long form is only needed if you have multiple remotes containing a branch called `somefeature`
  (we will learn about multiple remotes in the next episode).

  Once we track a remote branch, we can pull from it and push to it:

  ```console
  $ git pull origin somefeature
  $ git push origin somefeature
  ```

  We can also delete remote branches:

  ```console
  $ git push origin --delete somefeature
  ```
````

```{callout} Creating pull requests from the command line
There are several possibilties:
- <https://cli.github.com/>
- <https://hub.github.com/>
- <https://github.com/NordicHPC/git-pr>
```

```{callout} How you can find out in which repositories you are a collaborator
Visit <https://github.com/settings/repositories> where you will see
an overview of all repositories you have write access to.
```

```{callout} GitHub/GitLab organizations
- Projects often start under a personal namespace.
- If you want the project to live beyond the interest or work time of one person,
  one can share projects under an "organization".
- You can then invite collaborators to an organization.
- This is what we do in the CodeRefinery project: <https://github.com/coderefinery>
```

```{keypoints}
- Centralized workflow is often used for remote collaborative work.
- `origin` refers to where you cloned from (but you can relocate it).
- `origin/mybranch` is a read-only pointer to branch `mybranch` on `origin`.
- These read-only pointers only move when you `git fetch`/`git pull` or `git push`.
```
