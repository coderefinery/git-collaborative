# Quick reference

## Other cheatsheets

See the [git-intro cheatsheet](https://coderefinery.github.io/git-intro/reference/) for
the basics.

* [Interactive git cheatsheet](http://www.ndpsoftware.com/git-cheatsheet.html)
* [Very detailed 2-page git
  cheatsheet](https://aaltoscicomp.github.io/cheatsheets/git-for-normal-people-cheatsheet_1.0.pdf)


## Glossary

* **remote**: Roughly, another git repository on another computer.  A
  repository can be linked to several other remotes.
* **push**: Send a branch from your current repository to another repository
* **fetch**: Update your view of another repository
* **pull**: Fetch (above) and then merge
* **origin**: Default name for a remote repository.
* **origin/NAME**: A branch name which represents a remote branch.
* **master**: Default name for main branch.
* **merge**: Combine the changes on two branches.
* **conflict**: When a merge has changes that affect the same lines,
  git can not automatically figure out what to do.  It presents the
  conflict to the user to resolve.
* **issue**: Feature of web repositories that allows discussion
  related to a repository.
* **pull request**: A Github/Gitlab feature that allows you to send a
  code suggestion using a branch, which allows one-button merging.  In
  Gitlab, called "**merge request**".
* **git hook**: Code that can run before or after certain actions, for
  example to do tests before allowing you to commit.
* **bare repository**: A copy of a repository that only is only the `.git`
  directory: there are no files actually checked out.  Directory names
  usually like `something.git`


## Commands we use

This excludes most introduced in the [git-intro
cheatsheet](https://coderefinery.github.io/git-intro/reference/).

Setup:

* `git clone <url> [<target-directory>]`: Make a copy of existing
  repository at &lt;url&gt;, containing all history.

Status:

* `git status`: Same as in basic git, list status
* `git remote [-v]`: List all remotes
* `git graph`: see a detailed graph of commits.  Create this command
  with `git config --global alias.graph "log --all --graph --decorate --oneline"`

General work:

* `git checkout <branch-name>`: Make a branch active.
* `git push [<remote-name>] [<branch>:<branch>]`: Send commits and
  update the branch on the remote.
* `git pull [<remote-name>] [<branch-name>]`: Fetch and then merge
  automatically.  Can be convenient, but to be careful you can fetch
  and merge separately.
* `git fetch [<remote-name>]`: Get commits from the remote.  Doesn't
  update local branches, but updates the remote tracking branches
  (like origin/NAME).
* `git merge [<branch-name>]`: Updates your current branch with
  changes from another branch.  By default, merges to the branch is is
  tracking by default.
* `git remote add <remote-name> <url>`: Adds a new remote with a
  certain name.
