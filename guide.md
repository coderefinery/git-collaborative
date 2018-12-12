---
layout: default
permalink: /guide/
---

# Instructor guide

### Prepare at the latest the day before

First verify that these repos exist:
- https://github.com/bast/centralized-workflow-exercise
- https://github.com/bast/forking-workflow-exercise

If yes, first
deactive Travis for https://github.com/coderefinery/forking-workflow-exercise

Then delete these repos:
- https://github.com/coderefinery/centralized-workflow-exercise
- https://github.com/coderefinery/forking-workflow-exercise

Then create the empty repositories:
- https://github.com/coderefinery/centralized-workflow-exercise
- https://github.com/coderefinery/forking-workflow-exercise

Now re-activate Travis CI for this repo before you push changes to it:
- https://github.com/coderefinery/forking-workflow-exercise

Then mirror the repositories fresh:

```
$ git clone --mirror https://github.com/bast/centralized-workflow-exercise.git
$ cd centralized-workflow-exercise.git
$ git push --mirror git@github.com:coderefinery/centralized-workflow-exercise.git
$ cd ..
$ git clone --mirror https://github.com/bast/forking-workflow-exercise.git
$ cd forking-workflow-exercise.git
$ git push --mirror git@github.com:coderefinery/forking-workflow-exercise.git
$ cd ..
```

The motivation is:
- start with a clean repository without contributions
- avoid participants forking a fork which sets a confusing merge base

After inviting participants as collaborators, give them the invite link, otherwise
the invitations can be swallowed by spam filters.


### Before you start teaching, check https://github.com/coderefinery/centralized-workflow-exercise

- If you see changes from last workshop, stop and apply the above steps.

Compare:
- https://github.com/bast/centralized-workflow-exercise/network
- https://github.com/coderefinery/centralized-workflow-exercise/network

- If they are not the same and you see new changes from this workshop
  (participants who race ahead), reset the repository with the `--mirror` steps above.
- Remind participants that we have to do all steps of the centralized workflow
  exercise together for minimum confusion.


### How to start

<Here can be a starting anecdote or a starting question.>


### Questions to involve participants

<Here list a couple of questions that can be asked to
wake participants up.>


### Timing

<Give hints on timing.>

- The first episode is densest and introduces many new concepts,
  so at least an hour is required for it.
- The forking-workflow exercise (episode 3) repeats familiar concepts (only
  introduces forking and distributed workflows), and it takes maybe half the
  time of the first episode.
- The "How to contribute changes to somebody else's project" episode can be
  covered really quickly


### Core aspects

- Be able to submit a change to another project.
- Understand how to update a fork.
- Be able to contribute in code review.


### Sessions which can be skipped if time is tight

<List optional sessions here.>

- The bare vs non-bare episode can be skipped over without any harm done
- The hooks episode is typically skipped


### Typical pitfalls

<Document here with what participants often struggle.>

- The difference between pull and pull requests can be confusing, explain clearly that
  pull requests are a different mechanism specific to GitHub, GitLab...
- The behavior that additional commits to a branch from which a pull request has been created get appended
  to the pull request needs to be explained


### Centralized workflow exercise

Remind participants to not rush ahead but do one step at
a time collectively and discuss after each step. The effect
is then better.

If some participants already go ahead, they will manage to push
changes and the history will be different than what is expected.


### Other practical aspects

- Participants really have to sit next to someone, so that they can see the screens. From the beginning.
- Emphasize use of `git graph` a lot, just like in git-intro.
