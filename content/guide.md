# Instructor guide

## Why we teach this lesson

In order to collaborate efficiently using Git, it's essential to have a solid
understanding of how remotes work, and how to contribute changes through pull
requests.  The git-intro lesson teaches participants how to work efficiently
with Git when there is only one developer. This lesson dives into the
collaborative aspects of Git and focuses on the possible collaborative
workflows enabled by web-based repository hosting platforms like GitHub.

This lesson is meant to directly benefit workshop participants who have prior
experience with Git, enabling them to put collaborative workflows involving
code review directly into practice when they return to their normal work. For
novice Git users (who may have learned a lot in the git-intro lesson) this
lesson is somewhat challenging, but the lesson aims to introduce them to the
concepts and give them confidence to start using these workflows later when
they have gained some further experience in working with Git.


## Intended learning outcomes

By the end of this lesson, learners should:
- understand the concept of remotes
- be able to describe the difference between local and remote branches
- be able to describe the difference between centralized and forking workflows
- know how to use pull requests to submit changes to another projects
- know how to reference issues in commits or pull requests and how to auto-close issues
- know how to update a fork.
- be able to contribute in code review.


## Interesting questions you might get

If participants run `git graph` they might notice `origin/HEAD`.  This has been
omitted from the figures to not overload them.  This pointer represents the
default branch of the remote repository.


## Timing

- The centralized collaboration episode is densest and introduces many new concepts,
  so at least an hour is required for it.
- The forking-workflow exercise repeats familiar concepts (only
  introduces forking and distributed workflows), and it takes maybe half the
  time of the first episode.
- The "How to contribute changes to somebody else's project" episode can be
  covered really quickly and offers room for discussion if you have time left.


## Typical pitfalls

### Difference between pull and pull requests

The difference between pull and pull requests can be confusing, explain clearly
that pull requests are a different mechanism specific to GitHub, GitLab, etc.


### Pull requests are from branch to branch, not from commit to branch

The behavior that additional commits to a branch from which a pull request has
been created get appended to the pull request needs to be explained.


## Other practical aspects

- Participants really have to sit next to someone, so that they can see the
  screens. From the beginning.
- Emphasize use of `git graph` a lot, just like in the git-solo lesson.
