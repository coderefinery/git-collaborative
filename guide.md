---
layout: default
permalink: /guide/
---

# Instructor guide

### Prepare at the latest the day before

First verify that these repos exist - **never remove these**, **never use these directly during a course**:
- [https://github.com/coderefinery/template-centralized-workflow-exercise](https://github.com/coderefinery/template-centralized-workflow-exercise)
- [https://github.com/coderefinery/template-forking-workflow-exercise](https://github.com/coderefinery/template-forking-workflow-exercise)

In a previous workshop you may have used
[https://github.com/coderefinery/forking-workflow-exercise](https://github.com/coderefinery/forking-workflow-exercise).
If yes, deactivate Travis for this repository. If you have used a different
exercise repository (in your own workshop), please make sure that Travis is not
activated for that repository before we continue.

Then delete the copied exercise repositories from a previous workshop. They may be at a
different location. **Make sure to not remove the templates above**. You only want to remove their copies:
- [https://github.com/coderefinery/centralized-workflow-exercise](https://github.com/coderefinery/centralized-workflow-exercise)
- [https://github.com/coderefinery/forking-workflow-exercise](https://github.com/coderefinery/forking-workflow-exercise)

Now use the [GitHub importer](https://github.com/new/import) to create new copies:

Centralized exercise (you are welcome to use a different target address):
- Your old repository’s clone URL: [https://github.com/coderefinery/template-centralized-workflow-exercise](https://github.com/coderefinery/template-centralized-workflow-exercise)
- Your new repository details: coderefinery / centralized-workflow-exercise

Forking exercise (you are welcome to use a different target address):
- Your old repository’s clone URL: [https://github.com/coderefinery/template-forking-workflow-exercise](https://github.com/coderefinery/template-forking-workflow-exercise)
- Your new repository details: coderefinery / forking-workflow-exercise

Now re-activate
[Travis CI](https://travis-ci.org/organizations/coderefinery/repositories)
for the forking-workflow-exercise repository before you push changes to it.

To test that Travis CI is correctly set up,
fork [https://github.com/coderefinery/forking-workflow-exercise](https://github.com/coderefinery/forking-workflow-exercise),
submit a pull request, and
verify that testing is triggered by the pull request, then you can close the pull request again.

Add at least one other helper as an admin to the newly copied centralized-workflow-exercise (let the
other helpers know who that is), so that someone can give latecomers
write access without asking the main presenter.

After inviting participants as collaborators, give them the invite link, otherwise
the invitations can be swallowed by spam filters.

The motivation for the above steps:
- Start with a clean repository without contributions.
- Avoid participants forking a fork which sets a confusing merge base.


### Before you start teaching, check the centralized workflow exercise

Check [https://github.com/coderefinery/centralized-workflow-exercise](https://github.com/coderefinery/centralized-workflow-exercise)
(or the location which you chose to use instead).

- If you see changes from last workshop, stop and apply the above steps.

Compare:
- [https://github.com/coderefinery/template-centralized-workflow-exercise/network](https://github.com/coderefinery/template-centralized-workflow-exercise/network) (the template)
- [https://github.com/coderefinery/centralized-workflow-exercise/network](https://github.com/coderefinery/centralized-workflow-exercise/network) (the copy you have created)

- If they are not the same and you see new changes from this workshop
  (participants who race ahead), reset the repository with a hard reset to its initial state.
- Remind participants that we have to do all steps of the centralized workflow
  exercise together for minimum confusion.


### How to start

(Here can be a starting anecdote or a starting question.)


### Questions to involve participants

(Here list a couple of questions that can be asked to
wake participants up.)


### Timing

- The first episode is densest and introduces many new concepts,
  so at least an hour is required for it.
- The forking-workflow exercise (episode 3) repeats familiar concepts (only
  introduces forking and distributed workflows), and it takes maybe half the
  time of the first episode.
- The "How to contribute changes to somebody else's project" episode can be
  covered really quickly and offers room for discussion if you have time left.


### Core aspects

- Be able to submit a change to another project.
- Understand how to update a fork.
- Be able to contribute in code review.


### Sessions which can be skipped if time is tight

- The bare vs non-bare episode can be skipped over without any harm done.
- The hooks episode is typically skipped.


### Typical pitfalls

- The difference between pull and pull requests can be confusing, explain clearly that
  pull requests are a different mechanism specific to GitHub, GitLab, etc.
- The behavior that additional commits to a branch from which a pull request has been created get appended
  to the pull request needs to be explained.


### Centralized workflow exercise

Remind participants to not rush ahead but do one step at
a time collectively and discuss after each step. The effect
is then better.

If some participants already go ahead, they will manage to push
changes and the history will be different than what is expected.


### Other practical aspects

- Participants really have to sit next to someone, so that they can see the screens. From the beginning.
- Emphasize use of `git graph` a lot, just like in the git-solo lesson.
