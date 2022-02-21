# Instructor guide

## Why we teach this lesson

In order to collaborate efficiently using Git, it's essential to have a solid understanding of
how remotes work, and how to contribute changes through pull requests.
The git-intro lesson teaches participants how to work efficiently with Git when there is only
one developer. This lesson dives into the collaborative aspects of Git and focuses on the possible
collaborative workflows enabled by web-based repository hosting platforms like GitHub.

This lesson is meant to directly benefit workshop participants who have prior experience with Git,
enabling them to put collaborative workflows involving code review directly into practice
when they return to their normal work. For novice Git users (who may have learned a lot in the git-intro
lesson) this lesson is somewhat challenging, but the lesson aims to introduce them to the concepts
and give them confidence to start using these workflows later when they have gained some further experience
in working with Git.

## Intended learning outcomes

By the end of this lesson, learners should:
- understand the concept of remotes
- be able to describe the difference between local and remote branches
- be able to describe the difference between centralized and forking workflows
- know how to use pull requests to submit changes to another projects
- know how to reference issues in commits or pull requests and how to auto-close issues
- know how to update a fork.
- be able to contribute in code review.

## How to teach this lesson

### Preparing the exercises and cleaning up

- Exercises are templates but we do not use the templates directly but
  [generate exercises from them](https://help.github.com/en/articles/creating-a-repository-from-a-template).
- You need to prepare the exercises at least one day before by generating them from a template.
- After the workshop please remove the generated exercises (if created under
  https://github.com/coderefinery), otherwise the instructor in a future
  workshop may not have the permissions to do so.


#### How to customize the lesson for your workshop

You can adjust the location of the exercises in case you plan to generate/import them to a custom place.

This is the default:

```yaml
centralized_workflow_exercise_url: https://github.com/coderefinery/centralized-workflow-exercise
forking_workflow_exercise_url: https://github.com/coderefinery/forking-workflow-exercise
```

But you can change these in `_config.yml`
and this will change the locations in this instructor guide
but also in the lesson episodes.


#### Prepare exercise repositories

First verify that these repos exist - **never remove these**, **never use these directly during a course**:
- [https://github.com/coderefinery/template-centralized-workflow-exercise](https://github.com/coderefinery/template-centralized-workflow-exercise)
- [https://github.com/coderefinery/template-forking-workflow-exercise](https://github.com/coderefinery/template-forking-workflow-exercise)

Then delete the copied exercise repositories from a previous workshop.
**Make sure to not remove the templates above** - you only want to remove their copies:
- [{{ site.centralized_workflow_exercise_url }}]({{ site.centralized_workflow_exercise_url }})
- [{{ site.forking_workflow_exercise_url }}]({{ site.forking_workflow_exercise_url }})

Now create the two above exercises by [generating](https://help.github.com/en/articles/creating-a-repository-from-a-template)
these two templates:
- [https://github.com/coderefinery/template-centralized-workflow-exercise](https://github.com/coderefinery/template-centralized-workflow-exercise)
- [https://github.com/coderefinery/template-forking-workflow-exercise](https://github.com/coderefinery/template-forking-workflow-exercise)

Finally give all instructors admin rights to the two newly created exercise repositories and write-protect the
`master` branch until we really start pushing to the repository.

The motivation for the above steps:
- Start with a clean repository without contributions.
- Avoid participants forking a fork which sets a confusing merge base.


#### Make it easier for participants to join the centralized exercise

Add at least one other helper as an admin to the newly copied centralized-workflow-exercise (let the
other helpers know who that is), so that someone can give latecomers
write access without asking the main presenter.

After inviting participants as collaborators, give them the invite link, otherwise
the invitations can be swallowed by spam filters.

---

### Before you start teaching, check the centralized workflow exercise

Check [{{ site.centralized_workflow_exercise_url }}]({{ site.centralized_workflow_exercise_url }}) (adjust the URL if you have imported the exercise into another custom location):
- If you see changes from last workshop, stop and apply the above steps ("Preparing the exercises").

---

### Interesting questions you might get

If participants run `git graph` they might notice `origin/HEAD`.
This has been omitted from the figures to not overload them.
This pointer represents the default branch of the remote repository.

---

### Timing

- The centralized collaboration episode is densest and introduces many new concepts,
  so at least an hour is required for it.
- The forking-workflow exercise repeats familiar concepts (only
  introduces forking and distributed workflows), and it takes maybe half the
  time of the first episode.
- The "How to contribute changes to somebody else's project" episode can be
  covered really quickly and offers room for discussion if you have time left.

---

### Sessions which can be skipped if time is tight

- The bare vs non-bare episode can be skipped over without any harm done. We have discussed this episode
  in only one workshop so far and I think it was more confusing than helpful.
- The hooks episode is typically skipped.

---

### Typical pitfalls

#### Difference between pull and pull requests

The difference between pull and pull requests can be confusing, explain clearly that
pull requests are a different mechanism specific to GitHub, GitLab, etc.


#### Pull requests are from branch to branch, not from commit to branch

The behavior that additional commits to a branch from which a pull request has been created get appended
to the pull request needs to be explained.

---

### Other practical aspects

- Participants really have to sit next to someone, so that they can see the screens. From the beginning.
- Emphasize use of `git graph` a lot, just like in the git-solo lesson.
