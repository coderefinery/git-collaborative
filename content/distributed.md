# Distributed version control and forking workflow

```{objectives}
- Get a mental representation of what is happening on GitHub/GitLab.
- Get comfortable with the forking workflow.
```

```{instructor-note}
- 20 min teaching
- 40 min exercises
```


## Forking layout

```{figure} img/forking/forking-overview.svg
:alt: Forking workflow
:width: 50%

Forking workflow.
```

In the **forking layout**, again we call one repository the "central"
repository but people push to **forks** (their own copies of the
repository on GitHub/GitLab/Bitbucket).

Features:

- **Anybody can contribute without asking for permission** (to public projects).
- Maintainer still has **full control over what is merged**.
- There is now **more than one remote** to work with.

Real life examples:

- NumPy: [https://numpy.org/devdocs/dev/index.html](https://numpy.org/devdocs/dev/index.html)
- [https://github.com/jupyterlab/jupyterlab](https://github.com/jupyterlab/jupyterlab)


## Working with multiple remotes

- There is nothing special about the name `origin`. The `origin` is just an alias/placeholder (think of "sticky note" referring to an URL).
- We can call these aliases as we like.
- We can add and remove remotes:

```console
$ git remote add upstream https://github.com/project/project.git
$ git remote rm upstream
$ git remote add group-repo https://example.com/exciting-project.git
$ git remote rm group-repo
$ git remote add upstream https://github.com/project/project.git
$ git remote add downstream https://github.com/userX/project.git
```

We typically synchronize remotes via the local clone on our local computer.

To see all remotes:

```console
$ git remote --verbose
```

```{warning}
**We will work with a new repository for this exercise!**

For this exercise we will fork a different repository compared to earlier today.
Please step out of the repository and check that you fork the **forking**-workflow-exercise.
```


## Exercise: Part 1 - creating a pull request

```{exercise} Distributed-1: Fork a repository and create a pull request
As an example we will collaboratively develop a cookbook for taco recipes,
inspired by [tacofancy](https://github.com/sinker/tacofancy).

**Objectives**:
- Learn how to fork, modify the fork, and file a pull request towards the forked repo.
- Learn how to update your fork with upstream changes.

**Exercise**:
- Helper prepares an exercise repository (see below; this will take 5-10 minutes).
- **The exercise group works on steps A-E** (15-20 minutes).
- There are two optional steps after step E for those who want more steps.
- After step E you can return to the main room. Please ask questions both during group work and in main room.
- **We will review the pull requests and update forks together** (instructor demonstrates, and everybody follows along in their repositories).
```

```{prereq} Exercise preparation
**Helpers in breakout-rooms**:
- Create an exercise repository by
  [generating from a template](https://help.github.com/en/articles/creating-a-repository-from-a-template)
  using this template: <https://github.com/coderefinery/template-forking-workflow-exercise>
  called `forking-workflow-exercise`
- In this case we **do not add collaborators** to the repository (this is the point of this example).
- Share the link to the newly created repository in the shared document with your group.

**Learners in breakout-rooms**: Fork the helper's newly created repository and clone the fork.

**Instructor**: Prepare an exercise repository for participants following via stream (see below).

**Learners following via stream**: Fork the repository created by the
instructor on stream and then clone the fork to your computer.
```


### Step A: Fork and clone

Here is a pictorial representation of this part:

```{figure} img/forking/forking-1.svg

Forking followed by cloning.
```

This is how it looks after we fork:

```{figure} img/forking/github-remote-01.svg

central
```

```{figure} img/forking/github-remote-01.svg

fork
```

- A fork is basically a (bare) clone.
- The upstream repo and the fork are in principle independent repositories.
- When forking we copy all commits, all branches.

After we clone the fork we have three in principle independent repositories:

```{figure} img/forking/github-remote-01.svg

central
```

```{figure} img/forking/github-remote-01.svg

fork
```

```{figure} img/forking/github-local-01.svg

local
```


### Step B: Open an "issue" as a change proposal

Before we start any coding, open a new "Issue" on the central repository as a
"proposal" where you describe your idea for a recipe with the possibility to
collect feedback from others. After creating this issue note the issue number.
We will later refer to this issue number.

Discuss with your neighbor why it can be useful to open an issue before
starting the actual coding.


### Step C: Modify and commit

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

```{figure} img/forking/github-remote-01.svg

central
```

```{figure} img/forking/github-remote-01.svg

fork
```

```{figure} img/forking/github-local-02.svg

local
```


### Step D: Push your changes to the fork

Now push your new branch to your fork. Your branch is probably called something
else than "feature". Also verify where "origin" points to.

```console
$ git push origin feature
```

```{figure} img/forking/github-remote-01.svg

central
```

```{figure} img/forking/github-remote-02.svg

fork
```

```{figure} img/forking/github-local-03.svg

local
```


### Step E: File a pull request

Then file a pull request from the branch on your fork towards the master branch on the repository where you forked from.

Here is a pictorial representation for parts D and E:

```{figure} img/forking/forking-2.svg

Push followed by a pull request.
```

A pull-request means: "please review my changes and if you agree, merge them with a mouse-click".

Once the pull-request is accepted, the change is merged:

```{figure} img/forking/github-remote-03.svg

central
```

```{figure} img/forking/github-remote-02.svg

fork
```

```{figure} img/forking/github-local-03.svg

local
```

Wait here until we integrate all pull requests into the central repo
together on the big screen.

Observe how the issues automatically close after the pull requests are merged
(provided the commit messages contain [the right keywords](https://help.github.com/en/articles/closing-issues-using-keywords)).

```{exercise} (optional) Distributed-2: Send a conflicting pull request
If you complete parts A-E much earlier than others, try to send another pull request
where you anticipate a conflict with your first pull request.
```

```{exercise} (optional) Distributed-3: Making changes to your pull request after it has been opened.
You can do that by pushing new commits to the branch where you sent the pull
request from. Observe how they end up added to your pull request.
```


## Exercise: Part 2 - code review and merging changes

**We do this step together on the main screen (in the main room)**. The instructor shows a submitted
pull request, discusses what features to look at, and how to discuss and review.

At the same time, helpers can review open pull requests from their exercises groups.


```{exercise} (optional) Distributed-4: Squash merge a pull request
If you complete this exercise much earlier than others, pair up with somebody,
create a new repository, fork it, and send a pull request with several
small commits. On the other computer accept these with "Squash and merge" and later compare the source
and target repositories/branches how they differ after the small commits got squashed into one.
```


## Exercise: Part 3 - Updating forks

We do this part **after the contributions from all participants have been
integrated**.

Once this is done, practice to update your forked repo with the upstream
changes and verify that you got the files created by other participants.

Make sure that the contributions from other participants are not only on your
local repository but really also end up in your fork.

Here is a pictorial representation of this part:

```{figure} img/forking/forking-3.svg

Pull followed by push to a different remote.
```

We will discuss three solutions:

```{instructor-note}
It would be great to present both the "shorter route" and the updating fork via
the web interface. One way to do this is to encourage a participant to share
screen while they demonstrate the "shorter route" and then to also demonstrate
the web interface fork update on the instructor computer.
```


### Using the web interface (GitHub)

On GitHub it is now also possible to update the fork by pressing a button (see
screenshot below):

```{figure} img/forking/fetch-and-merge.png
:alt: Updating the fork via GitHub web interface

Updating the fork via GitHub web interface.
```


### Shorter route

Remotes are aliases. We can use remote URLs directly.

Here we pull from the central repo and push to our fork
(replace with the repository you forked if needed):

```console
$ git checkout master
$ git pull <central-repository-url> master
$ git push <fork-url> master
```


### Longer route

- Upstream repo receives other changes (other merged pull-requests)
- How do we get these changes to the forked repo?
- Replace below with the repository you forked, if needed

```console
$ git remote add upstream <central-repository-url>
$ git fetch upstream
```

```{figure} img/forking/github-remote-03.svg

central
```

```{figure} img/forking/github-remote-02.svg

fork
```

```{figure} img/forking/github-local-04.svg

local
```

```console
$ git checkout master
$ git merge upstream/master
```

```{figure} img/forking/github-remote-03.svg

central
```

```{figure} img/forking/github-remote-02.svg

fork
```

```{figure} img/forking/github-local-05.svg

local
```

```console
$ git push origin master
```

```{figure} img/forking/github-remote-03.svg

central
```

```{figure} img/forking/github-remote-04.svg

fork
```

```{figure} img/forking/github-local-06.svg

local
```

---

```{figure} img/forking/remote.jpg
```
- Luke Skywalker: *You know, I did feel something. I could almost see the remote.*
- Ben Kenobi: *That's good. You've taken your first step into a larger world.*

[from Star Wars Episode IV - A New Hope]


```{discussion} Discussion: Always create a feature branch
For each pull request create a new branch.

Motivation:
- Limits the risk that commits get accidentally appended to an open pull request.
- History-rewrite (rebased and/or squashed commits) on the central repository does not lead to a diverging local default branch.

See also [this
blogpost](https://blog.jasonmeridth.com/posts/do-not-issue-pull-requests-from-your-master-branch/)
for an explanation.
```


```{keypoints}
- Working with multiple remotes is not as scary as it might look.
- `origin` is just an alias/placeholder.
- We can add and remove remotes.
- We can call these aliases/placeholders as we like.
- We typically synchronize/updates remotes via the local clone.
- To see all remotes use `git remote -v`.
- If you are more than one person contributing to a project, consider using code review.
```
