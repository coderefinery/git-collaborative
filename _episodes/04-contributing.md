---
layout: episode
title: How to contribute changes to somebody else's project
teaching: 15
exercises: 0
questions:
  - What steps can we recommend to contribute changes to somebody else's project?
objectives:
  - Avoid frustration and surprises by first discussing and then coding.
keypoints:
  - Communicate and discuss before coding massive changes.
  - Cross-reference discussions, proposals, and code changes.
---

## Very minor changes

- Fork repository
- Create a branch
- Commit and push change
- File a pull request

---

## If you observe an issue and have an idea how to fix it

- Open an issue in the repository you wish to contribute to
- Describe the problem
- If you have a suggestion on how to fix it, describe your suggestion
- Possibly discuss and get feedback
- If you are working on the fix, indicate it in the issue so that others know that somebody is working on it and who is working on it
- Submit your fix as pull request which references/closes the issue

**Motivation**:

- Inform others about an observed problem
- Make it clear whether this issue is up for grabs or already being worked on

---

## If you have an idea for a new feature

- Open an issue in the repository you wish to contribute to
- Write a short proposal for your suggested change or new feature
- Motivate why and how you wish to do this
- Discuss and get feedback before you code
- Once you start coding, indicate that you are working on it
- Once you are done, submit your new feature as pull request which references/closes the issue/proposal

**Motivation**:

- Get agreement and feedback before writing 5000 lines of code which might be rejected
- If we later wonder why something was done, we have the proposal as reference and can read up on the reasoning behind a code change

---

## WIP (work in progress) merge requests and draft pull requests

- Convention: Pull requests or merge requests starting with "WIP" are not to be merged yet
- They are there to collect feedback on unfinished work
- On GitHub you can create [draft pull requests](https://github.blog/2019-02-14-introducing-draft-pull-requests/)
  which cannot be merged until marked ready for review.

**Typical workflow**:

- Open an issue in the repository you wish to contribute to
- Write a short proposal for your suggested change or new feature
- Motivate why and how you wish to do this
- Discuss and get feedback before you code
- Once you start coding, indicate that you are working on it
- Once you are done, submit your new feature as pull request which references/closes the issue/proposal

**Motivation**:

- Get agreement and feedback before writing 5000 lines of code which might be rejected
- If we later wonder why something was done, we have the proposal as reference and can read up on the reasoning behind a code change

---

## How to make sure that you don't merge malicious code

- Since commit hashes depend on all their parents you cannot modify the past
  without all future hashes changing
- Projects like
  [https://github.com/torvalds/linux](https://github.com/torvalds/linux)
  or
  [https://github.com/bitcoin/bitcoin](https://github.com/bitcoin/bitcoin)
  have to be extremely careful what they accept
- Do not blindly merge submitted pull requests
- Browse the code changes before merging them
- If you get an extremely large changeset, ask for more information
- Possibly verify whether the submitter is not trying to impersonate somebody you know
- Git commits can be PGP signed to verify authenticity
