# Instructor guide


## Approximate schedule

Times here are in CE(S)T.

- 08:50 - 09:00 (10 min) Soft start and icebreaker question

- 09:00 - 09:15 (15 min) Recap Git, any HedgeDoc questions to highlight
- 09:15 - 09:25 (10 min) [Concepts around collaboration](https://coderefinery.github.io/git-collaborative/concepts/)
    - Explain terms: Pull, push, clone, fork. Focus on pull and not fetch.
    - Focus more on clone and less on generating from templates and importing.
- 09:25 - 10:00 (35 min) [Collaborating within the same repository](https://coderefinery.github.io/git-collaborative/same-repository/)
  - Exercise (incl preparation)

- 10:00 - 10:10 (10 min) Break

- 10:10 - 10:30 (20 min) [Collaborating within the same repository](https://coderefinery.github.io/git-collaborative/same-repository/)
  - Demo and Q/A
- 10:30 - 11:00 (30 min)  [Practicing code review](https://coderefinery.github.io/git-collaborative/code-review/)

- 11:00 - 12:00 (60 min) Break

- 12:00 - 12:50 (50 min) [Distributed version control and forking workflow](https://coderefinery.github.io/git-collaborative/distributed/)
    - Concepts and what are exercise outcomes
    - [Exercise](https://coderefinery.github.io/git-collaborative/distributed/#exercise-preparation)

- 12:50 - 13:00 (10 min) Break

- 13:00 - 13:30 (30 min) Discussion, demonstration, Q&A, feedback, what to expect next week


## Preparing exercises within exercise groups

Exercise leads typically prepare exercise repositories for the exercise group
(although the material speaks about "maintainer" who can also be one of the
learners). Preparing the first exercise (centralized workflow) **will take more
time** than preparing the second (forking workflow). Most preparation time is not
the generating part but will go into communicating the URL to the exercise
group, communicating their usernames, adding them as collaborators, and waiting
until everybody accepts the GitHub invitation to join the newly created
exercise repository.


## Preparing exercises for the live stream


### What instructors need to do at least 1 day before the workshop

- This **takes 30-60 minutes** to set up. Allocate the time for this before the workshop.
- Make sure to remove all participants from a previous workshop from these two places:
  - <https://github.com/orgs/cr-workshop-exercises/teams/stream-exercise-participants>
  - <https://github.com/orgs/cr-workshop-exercises/people>
- We create the exercises **in an organization** (not under your username) so
  that you can give others admin access to add collaborators. Also this way
  you can then fork yourself if needed.
- All exercise repositories can be created from
  <https://github.com/coderefinery/recipe-book-template> by `git clone
  --mirror` from the template followed by `git push --mirror` towards the exercise repository.
- We have created two versions of each **a day in advance** to signal which one might end up
  being discussed on recording/stream:
  - `centralized-workflow-exercise-recorded`
  - `centralized-workflow-exercise`
  - `forking-workflow-exercise-recorded`
  - `forking-workflow-exercise`
- Protect the default branch of the two `centralized-*` repositories (but this
  can also be done on stream as the very first step if you are sure you will remember as instructor).


### What to communicate to learners at least 1 day before the workshop

- [Example email from a previous workshop](https://coderefinery.github.io/2025-03-25-workshop/communication/#getting-ready-for-day-2-and-3-of-coderefinery-workshop)


### How should learners request access

This is also in the email template above but they need to:
- Open an issue at https://github.com/cr-workshop-exercises/access-requests/issues/new?template=access-request.md

- Accept invitation from GitHub sent to their email address (that GitHub
  knows about).

- "Unwatch" both these repositories by clicking the "Unwatch" button (top
   middle of the screen) and then select "Participating and mentions":
   - <https://github.com/cr-workshop-exercises/centralized-workflow-exercise>
   - <https://github.com/cr-workshop-exercises/centralized-workflow-exercise-recorded>


### How to add learners to the team stream-exercise-participants

You need to be "owner" of
<https://github.com/orgs/cr-workshop-exercises/teams/stream-exercise-participants>
to be able to add people to the team.


1) Check <https://github.com/cr-workshop-exercises/access-requests/issues>.
   Any open issue means the person hasn't been added yet.

2) Assign one issue to yourself. This way other organizers know that this is being worked on.

3) Add person to <https://github.com/orgs/cr-workshop-exercises/teams/stream-exercise-participants>
  - Click on "Add member" -> "Invite" -> "Add (username) to stream-exercise-participants"
  - **Do not add/invite the person anywhere else**, not as collaborator to any
    exercise repo directly. Only add/invite them into the team
    "stream-exercise-participants". Motivation: This way we give instructors the control over when the exercise can start. Otherwise
    learners might merge changes before the lesson and thus change the example and confuse instructors and learners.

4) Close the issue on <https://github.com/cr-workshop-exercises/access-requests/issues> with the following comment (feel free to adapt it):
```
Thanks! I have added you to the collaborative exercise team.

What you should do before the exercise starts:

1) You will get an invitation from GitHub to your email address (that GitHub
   knows about). Please accept that invitation so that you can participate in
   the collaborative exercise.

2) To make sure you don't get too many emails during the exercise, don't forget
   to "unwatch" both
   https://github.com/cr-workshop-exercises/centralized-workflow-exercise and
   https://github.com/cr-workshop-exercises/centralized-workflow-exercise-recorded.
   To "unwatch", go to the repository and click the "Unwatch" button (top
   middle of the screen) and then select "Participating and mentions".
```


## Why we teach this lesson

In order to collaborate efficiently using Git, it's essential to have a solid
understanding of how remotes work, and how to contribute changes through pull
requests or merge requests. The [git-intro lesson](https://coderefinery.github.io/git-intro/)
teaches participants how to
work efficiently with Git when there is only one developer (more precisely: how
to work when there are no remote Git repositories yet in the picture). This
lesson dives into the collaborative aspects of Git and focuses on the possible
collaborative workflows enabled by web-based repository hosting platforms like
GitHub.

This lesson is meant to directly benefit workshop participants who have prior
experience with Git, enabling them to put collaborative workflows involving
code review directly into practice when they return to their normal work. For
novice Git users (who may have learned a lot in the git-intro lesson) this
lesson is somewhat challenging, but the lesson aims to introduce them to the
concepts and give them confidence to start using these workflows later when
they have gained some further experience in working with Git.


## Intended learning outcomes

By the end of this lesson, learners should:
- Understand the concept of remotes
- Be able to describe the difference between local and remote branches
- Be able to describe the difference between centralized and forking workflows
- Know how to use pull requests or merge requests to submit changes to another projects
- Know how to reference issues in commits or pull/merge requests and how to auto-close issues
- Know how to update a fork
- **Be able to contribute in code review as submitter or reviewer**


## Interesting questions you might get

- If participants run `git graph` they might notice `origin/HEAD`.  This has been
  omitted from the figures to not overload the presentation. This pointer represents the
  default branch of the remote repository.


## Timing

- The centralized collaboration episode is densest and introduces many new concepts,
  so at least an hour is required for it.
- The forking-workflow exercise repeats familiar concepts (only
  introduces forking and distributed workflows), and it takes maybe half the
  time of the first episode.
- The "How to contribute changes to somebody else's project" episode can be
  covered relatively quickly and offers room for discussion if you have time left.
  However, this should not be skipped as this is perhaps the key learning outcome.


## Typical pitfalls

### Difference between pull and pull requests

The difference between pull and pull requests can be confusing, explain clearly
that pull requests or merge requests are a different mechanism specific to
GitHub, GitLab, etc.


### Pull requests are from branch to branch, not from commit to branch

The behavior that additional commits to a branch from which a pull request has
been created get appended to the pull request needs to be explained.


## Other practical aspects

- In in-person workshops participants really have to sit next to someone, so
  that they can see the screens. From the beginning.
- Emphasize use of `git graph` a lot, just like in the git-solo lesson.
