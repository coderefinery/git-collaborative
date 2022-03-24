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

Git implements a **distributed** version control.
This means that any type of repository links that you can think of can be
implemented - not just "everything connects to one central server".

In Git, all repositories are equivalent but we typically we consider one repository
as the main development line and this is marked as "central".
The "central" is a role, not a technical difference.

In this episode, we will explore the usage of a **centralized workflow** for collaborating online on a project
**within one repository**.


## Centralized layout

```{figure} img/forking/centralized.svg
:alt: Centralized layout
:width: 50%

Centralized layout.
```

Features:

- Typically all developers have both read and write permissions (double-headed arrows).
- Suited for cases where **all developers are in the same group or organization or project**.
- **Everybody who wants to contribute needs write access**.
- Good idea to write-protect the main branch (typically `master` or `main`).

Real life examples:

- Within the CodeRefinery team we mostly use this approach: [https://github.com/coderefinery](https://github.com/coderefinery)
- [https://github.com/ropensci/plotly](https://github.com/ropensci/plotly)


## Exercise: Part 1 - creating a pull request

In this exercise we will practice collaborative centralized workflow in small
groups.  We'll discuss how this leads to code review and discuss a number of
typical pitfalls.

````{prereq} Exercise preparation
- We form small groups (4-5 persons).
- Each group needs to appoint someone who will host the shared GitHub repository: *an administrator*.
- For online teaching, use breakout rooms.
- **One person per group (administrator)** generates a new repository
  from the template <https://github.com/coderefinery/template-centralized-workflow-exercise>
  called `centralized-workflow-exercise` (There is no need to tick *"Include all branches"* for this exercise):
  ```{figure} img/centralized/generate_repo.png
  :alt: Screenshot of generating the exercise repository
  :width: 100%
  ```
- Then **everyone in your group** needs their GitHub account to be added as collaborator to the exercise repository:
  - Participants give their GitHub usernames to their chosen administrator (in their respective group, in online workshops you can use the Zoom chat for private communication within the breakout room).
  - Administrator gives the other group members the newly created GitHub repository URL.
  - Administrator adds participants as collaborators to their project (Settings → Manage Access → Invite a collaborator).
  - Group members need to accept the invitation. GitHub emails you an invitation link, but if you don't receive it
    you can go to your GitHub notifications in the top right corner. The administrator can also "copy invite link"
    and share it within the group.

- Watching and unwatching repositories:
  - Now that you are a collaborator, you get notified about new issues and pull
    requests via email.
  - If you do not wish this, you can "unwatch" a repository (top of the project page).
  - However, we recommend watching repositories you are interested in. You can learn things from experts just by
    watching the activity that come through.
````

```{exercise} Centralized-1: Clone a repository, add a file, push changes as a branch, and create a pull request
- Helper prepares an exercise repository (see above) - this will take 10 minutes or so. Most of the time will
  go into **communicating the usernames of the exercise group** and to add them as collaborators and for them to **accept
  the invitation** to the exercise repository.
- Before we start with the exercise, instructor mentions all steps and explains what happens during a `git clone`.
- The exercise group works on steps 1-8 (15-20 minutes).
- After step 8 you can return to the main room. Please ask questions both during group work and in main room.

Full exercise is below.
```

```{callout} Hint for breakout rooms
If the helper in the room is the one who sets up the central repository, they
cannot easily demostrate the steps via screen-sharing as the repository's owner. A
good alternative is to have one of the learners screen-share and get advice on the
steps from other learners and helpers!
```


### 1. Clone your administrator's group repository

```console
$ git clone <repository-url> centralized-workflow-exercise
```

Where `<repository-url>` is the repository created by the exercise administrator.

This is a representation of what happens when you clone:

```{figure} img/centralized/01-remote.svg

remote
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
- They only move during `git pull` or `git fetch` or `git push`.
- Only `git pull` or `git fetch` or `git push` require network.
- All other operations are local operations.


### 2. Step into the newly created directory

```console
$ cd centralized-workflow-exercise
```

Try to find out where this repository was cloned from using `git remote -v`.


### 3. Create a branch `yourname-somefeature` pointing at your commit

Create a branch from the current `master`. Also adapt "yourname-somefeature" to a better name:

```console
$ git branch yourname-somefeature master
$ git checkout yourname-somefeature
```

The `yourname-` prefix has no special meaning here (not like `origin/`): it is just part of a
branch name to indicate who made it.


### 4. Create a file with a unique name, e.g.: `yourusername.txt`

In this file share your favourite cooking recipe or haiku or Git trick or whatever.


### 5. Stage and commit the change

```console
$ git add yourusername.txt
$ git commit
```

```{figure} img/centralized/01-remote.svg

remote
```

```{figure} img/centralized/04-local.svg

local
```


### 6. Push your change as a new branch

```console
$ git push origin -u yourname-somefeature
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


### 7. Browse the network of branches and commits

After you have pushed your branch and other participants have too, browse the
network of branches and commits (on GitHub click on Insights -> Network) and
discuss with others what you see.


### 8. Submit a pull request

Submit a pull request from your branch towards the `master` branch.
Do this through the web interface.

A pull-request means: "please review my changes and if you agree, merge them with a mouse-click". In a popular project, it means that anyone can
contribute with *almost no work* on the maintainer's side - a big win.


## Exercise: Part 2 - code review and merging changes

```{exercise} Centralized-2: Merge the pull requests (together)
- **We do step 9 and 10 together** (instructor demonstrates, and everybody follows along in their repositories).
```

### 9. Discuss and accept pull requests

**We do this step together on the main screen (in the main room)**. The instructor shows a submitted
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

**Code review and protected branches**

- A good setting is to make the `master` or `main` branch **protected** and all changes to it have to go
  through code review.
- Centralized workflow with protected branches is a good setup for many projects.

**code review**

- You see what others are working on
- Collaborative learning
- OK if students and junior researchers review senior researchers
- Improves quality of the code

**Read more**

- This is a great resource: [Practical git PRs for small teams](https://scicomp.aalto.fi/scicomp/practical-git-prs/)
```

Once the pull-request is accepted, the change is merged:

```{figure} img/centralized/06-remote.svg

central
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


### 10. Update your local copy

Your branch `yourname-somefeature` is not needed anymore but more importantly,
you need to sync your local copy: Everybody needs to do this step in their
exercise repository but we do this together in the main room so that we can
discuss this step and ask questions.

```console
$ git checkout master
$ git pull origin master
```

```{figure} img/centralized/06-remote.svg

central
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
