---
layout: episode
title: Rebase and Fast Forward
teaching: 15
exercises: 15
questions:
  - Does the cleanliness of branch history matter?
  - Why should we consider a rebase model?
  - When is it ok to Force Push?
objectives:
  - Understand how rebasing and fast forwarding work
---

### Fast-Forward vs. Merge Commit

Remember that git does fast-forward merges whenever it can. This is a good
default, as a messy merge history makes for messy reading.

In a typical software development set-up there is a central place where
changes are approved and this is called upstream. When other people work on
the same code base it is possible that the upstream has changed while you work
on your feature.

Most of the time you could still make a pull request even if some parts of the
codebase have changed: if the same areas of code have not been touched, an
automatic merge commit can typically be created. Some people prefer to have
merge commits to make each merge explicit. This approach favours
accountability: someone made the change and someone (preferably someone else)
merged it.

On the other hand many want as linear a history as possible. This can be
accomplished by *fetching* and then *rebasing* one's own development branch on
the upstream. This approach favours a linear history, someone made each
feature and ` git log` reads like a linear history.

### Rebasing

What rebasing does is it takes the commits in the other branch, (upstream in
our case) and re-plays all the commits made to the branch being replaced. This
makes almost identical commits to replace the original commits.

Remember that a commit is the state of all files tracked by git. These new
commits will reflect the state introduced by the changes in the upstream.

### Rebase workflow

This assumes that origin is your fork and you have another remote named
upstream.

In addition this assumes that a remote branch has already been pushed to.

```shell
$ git remote add upstream https://github.com/coderefinery/example.git
$ git fetch upstream
$ git rebase upstream master
$ git push -f origin my_branch
```

A regular git push won't work: as the commits are different from the ones you
pushed earlier git detects that pushing the new commits and the new pointer to
the remote ref would cause the old commits to be lost. Hence you have to use
the --force option to push and cause git to intentionally cause the commits to
be unreachable from any branch.

Remember that this leads to git garbage collection to remove these lost
commits eventually, but typically not immediately.


### Exercise: Rebase and Force Push

Fork the repository at https://github.com/Jyrsa/sw-development .

It contains a typical situation: there were two parallel pull requests and one
has been merged into master. In this team we have chosen to maintain a linear
history so a merge commit is not desired.

1. Clone your fork of repository
2. Add the original https://github.com/Jyrsa/sw-development -repository as an
   upstream
3. Check out the branch `episode_viii`
   * Here we pretend that you merged from upstream master after creating your
     branch `episode_viii`
4. Rebase that branch on `master`
5. `git push -f` the branch `episode_viii` and make a pull request.

You can make the pull request to the original repo or just to the
master inside your own. The main point here is that you rebased the changes in
master to your own branch and used the much vaunted Force Push.

![]({{ site.baseurl }}/img/rebase/force_push.jpg)

### Food for thought

`git rebase -i` will permit you to, among other things `squash` a number of
commits you have made. Why do some teams prefer doing this? What could be a
downside of squashing all feature branches to a single commit?
