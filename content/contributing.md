# How to contribute changes to somebody else's project

```{objectives}
- Avoid frustration and surprises by first discussing and then coding.
```

```{instructor-note}
- 15 min teaching/discussion
```


## Contributing very minor changes

- Fork repository
- Create a branch
- Commit and push change
- File a pull request or merge request


## If you observe an issue and have an idea how to fix it

- Open an issue in the repository you wish to contribute to
- Describe the problem
- If you have a suggestion on how to fix it, describe your suggestion
- Possibly **discuss and get feedback**
- If you are working on the fix, indicate it in the issue so that others know that somebody is working on it and who is working on it
- Submit your fix as pull request or merge request which references/closes the issue

**Motivation**:

- **Inform others about an observed problem**
- Make it clear whether this issue is up for grabs or already being worked on


## If you have an idea for a new feature

- Open an issue in the repository you wish to contribute to
- Write a short proposal for your suggested change or new feature
- Motivate why and how you wish to do this
- Also indicate where you are unsure and where you would like feedback
- **Discuss and get feedback before you code**
- Once you start coding, indicate that you are working on it
- Once you are done, submit your new feature as pull request or merge request which references/closes the issue/proposal

**Motivation**:

- **Get agreement and feedback before writing 5000 lines of code** which might be rejected
- If we later wonder why something was done, we have the issue/proposal as
  reference and can read up on the reasoning behind a code change


## WIP (work in progress) merge requests and draft pull requests

- Convention: Pull requests or merge requests starting with "WIP" are not to be merged yet
- They are there to **collect feedback on unfinished work**
- On GitHub you can create [draft pull requests](https://github.blog/2019-02-14-introducing-draft-pull-requests/)
  which cannot be merged until marked ready for review.
- Also GitLab offers same mechanism (merge request starting with "WIP" or "Draft")

**Motivation**:

- Collect feedback before it is finished and before it becomes more difficult to change
- Communicate to others what is partially done if it affects their work


## Licenses matter

- If you submit code that is derivative work or code somebody else wrote, clarify license
- If you receive pull requests with a lot of code, **clarify its license and
  copyright** with the submitter, before merging


## How to make sure that you don't merge malicious code

(this is typically not a problem for most of us but can be a problem for some)

- Since commit hashes depend on all their parents you cannot modify the past
  without all future hashes changing
- Projects like <https://github.com/torvalds/linux> or <https://github.com/Homebrew/brew>
  have to be extremely careful what they accept
- Do not blindly merge submitted pull requests
- Browse the code changes before merging them
- If you get an extremely large changeset, ask for more information
- Possibly verify whether the submitter is not trying to impersonate somebody you know
- Git commits can be PGP signed to verify authenticity


```{keypoints}
- Communicate and discuss before coding massive changes.
- **Cross-reference discussions, proposals, and code changes**.
```
