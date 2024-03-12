# Collaborative distributed version control

We have learned how to make a Git repository for a single person. What
about sharing?

- Share the folder using email or using some file sharing service:
  This would lead to many back and forth emails and would be difficult
  keep all copies synchronized.
- One person’s repository on the web: allows one person to keep track of
  more projects, gain visibility, feedback, and recognition.
- Common repository for a group: everyone can directly update the same repository.
  Good for small groups.
- Forks or copies with different owners: anyone can suggest changes, even without
  advance permission. Maintainers approve what they agree with.

Being able to share more easily (going down the above list) is
*transformative* (easier to change something, that is you are not the sole owner)
because it allows projects to scale to a new level.
**This can’t be done without proper tools.**

**In this lesson we will learn how to keep repositories in sync and how to
work with remote repositories on GitHub and other services.** We will
discover and exercise the centralized as well as the forking workflows,
and finally look into how to automate tasks using Git hooks.

```{prereq}
1. Basic understanding of Git.
2. You need a [GitHub](https://github.com) account.

We will do this exercise on [GitHub](https://github.com) but also
[GitLab](https://gitlab.com) and
[Bitbucket](https://bitbucket.org) allow similar workflows and
basically everything that we will discuss is transferable. With this
material and these exercises we do not endorse the company
[GitHub](https://github.com). We have chosen to demonstrate a
number of concepts using examples with
[GitHub](https://github.com) because it is currently the most
popular web platform for hosting Git repositories and the chance is
high that you will interact with
[GitHub](https://github.com)-based repositories even if you choose
to host your Git repository on another platform.
```

```{toctree}
:maxdepth: 1
:caption: Core episodes

concepts.md
same-repository.md
forking-workflow.md
contributing.md
code-review.md
```

```{toctree}
:maxdepth: 1
:caption: Optional episodes

hooks.md
bare-repos.md
```

```{toctree}
:maxdepth: 1
:caption: Reference

reference
exercises
guide
PDF version <https://coderefinery.github.io/git-collaborative/lesson.pdf>
```

```{toctree}
:maxdepth: 1
:caption: About

All lessons <https://coderefinery.org/lessons/core/>
CodeRefinery <https://coderefinery.org/>
Reusing <https://coderefinery.org/lessons/reusing/>
```
