# Instructor guide


## Schedule Day 3

- 08:50 - 09:00: Soft start and icebreaker question
- 09:00 - 09:15: Recap Git, any HedgeDoc questions to highlight
- 09:15 - 09:30: [Concepts around collaboration](https://coderefinery.github.io/git-collaborative/remotes/)
    - Explain terms: Pull, push, clone, fork. Focus on pull and not fetch.
    - Focus more on clone and less on generating from templates and importing.
- 09:30 - 11:00: [Centralized workflow](https://coderefinery.github.io/git-collaborative/centralized/)
    - 9:30 - 9:45: Explain concepts
    - 9:45 - 9:55: Break
    - 9:55 - 10:00: Inform clearly what is expected outcome
    - 10:00 - 10:30: [Exercise](https://coderefinery.github.io/git-collaborative/centralized/#exercise-preparation)
    - 10:30 - 11:00: Instructors go through the exercise. Discussion and answering questions
- 11:00 - 12:00: Lunch Break
- 12:00 - 13:10: [Distributed version control and forking workflow](https://coderefinery.github.io/git-collaborative/distributed/)
    - 12:00 - 12:15: Concepts and what are exercise outcomes
    - 12:15 - 12:45: [Exercise](https://coderefinery.github.io/git-collaborative/distributed/#exercise-preparation)
    - 12:45 - 12:55 Break
    - 12:55 - 13:10: Instructors go through excercises. Discussion and answering questions
- 13:10 - 13:30: [How to contribute changes to somebody else’s project](https://coderefinery.github.io/git-collaborative/contributing/) and Q&A


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


## Preparing exercises

Exercise leads typically prepare exercise repositories for the exercise group
(although the material speaks about "maintainer" who can also be one of the
learners). Preparing the first exercise (centralized workflow) will take more
time than preparing the second (forking workflow). Most preparation time is not
the generating part but will go into communicating the URL to the exercise
group, communicating their usernames, adding them as collaborators, and waiting
until everybody accepts the GitHub invitation to join the newly created
exercise repository.

**Live stream**:
- Create the centralized exercises **in an organization** (not under your username) so
  that you can give others admin access to add collaborators. Also this way you
  can then fork yourself if needed.
- For CR workshops, the exercises were placed under
  <https://github.com/cr-workshop-exercises>. The instructors or team leads need to have owner status in the organization in order to invite people.
- We have created two versions of each **a day in advance** to signal which one might end up
  being discussed on recording/stream:
  - `centralized-workflow-exercise-recorded`
  - `centralized-workflow-exercise`
  - `forking-workflow-exercise-recorded`
  - `forking-workflow-exercise`
- Protect the default branch of the two `centralized-*` repositories.
- We create a organization team, `stream-exercise-participants`.  The
  *centralized* workflow exercise repos have this team added as a
  collaborator (*not* forking - they fork so they don't need write
  access there).
- We have collected usernames of people who want to contribute via
  issues on GitHub.  Make a fifth repository, `access-requests`,
  create a sample access request issue there, and have learners make a
  new issue in that repository.  The day/morning before the day of the lesson the instructor or team leader now has to invite the learners to the team. Three steps:
      1. copy the learners GitHub username from the issue
      2. go to [team member page, example linked here](https://github.com/orgs/cr-workshop-exercises/teams/stream-exercise-participants/members) and invite that username to the team (this means first clicking invite and then scrolling down to click the "add username to ..." button. This sends an email to that users email that is connected to their GitHub account.
      3. In the issue, copy following text (or similar) to the issue and "close with comment":
  ```
  We have added you to the CodeRefinery exercise repository.

  What you should do before the exercise starts:

  You will get an invitation from GitHub to your email address (that GitHub knows about). Please accept that invitation so that you can participate in the collaborative exercise.
  To make sure you don't get too many emails during the exercise, don't forget to "unwatch" both https://github.com/cr-workshop-exercises/centralized-workflow-exercise and https://github.com/cr-workshop-exercises/centralized-workflow-exercise-recorded.
  To "unwatch", go to the repository and click the "Unwatch" button (top middle of the screen) and then select "Participating and @mentions".
``
  
  - Why a fifth repository?  So that learners don't get emails from all
    other access requests once they get added to the team
  - [Example email requesting learners to join](https://coderefinery.github.io/2024-03-12-workshop/communication/#2024-03-12-exercise-preparation-for-learners-without-own-group)
  - [Example issue comment]([https://github.com/cr-workshop-exercises/access-requests/issues/110](https://github.com/cr-workshop-exercises/access-requests/issues/41))


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
