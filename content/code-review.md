# Practicing code review

In this episode we will practice the code review process. We will learn how to
ask for changes in a pull request, how to suggest a change in a pull request,
and how to modify a pull request.

This will enable research groups to work more collaboratively and to not only
improve the code quality but also to learn from each other.


## Exercise

:::{prereq} Exercise preparation
We can continue in the same exercise repository which we have used in the
previous episode.
:::

:::{exercise} Exercise: Practicing code review (25 min)

**Technical requirements**:
- If you create the commits locally: [Being able to authenticate to GitHub](https://coderefinery.github.io/installation/ssh/)

**What is familiar** from the previous workshop days:
- Creating a branch ([previous lesson](https://coderefinery.github.io/git-intro/commits/))
- Committing a change on the new branch ([previous lesson](https://coderefinery.github.io/git-intro/commits/))
- Opening and merging pull requests ([previous lesson](https://coderefinery.github.io/git-intro/merging/))

**What will be new** in this exercise:
- As a reviewer, we will learn how to ask for changes in a pull request.
- As a reviewer, we will learn how to suggest a change in a pull request.
- As a submitter, we will learn how to modify a pull request without closing
  the incomplete one and opening a new one.

**Exercise tasks**:
1. Create a new branch and one or few commits: in these improve something but also
   deliberately introduce a typo and also a larger mistake which we will want to fix during the code review.
1. Open a pull request towards the main branch.
1. As a reviewer to somebody else's pull request, ask for an improvement and
   also directly suggest a change for the small typo. (Hint:
   suggestions are possible through the GitHub web interface, view of
   a pull request, "Files changed" view, after selecting some lines.
   Look for the "±" button.)
1. As the submitter, learn how to accept the suggested change.  (Hint:
   GitHub web interface, "Files Changed" view.)
1. As the submitter, improve the pull request without having to close and open
   a new one: by adding a new commit to the same branch. (Hint: push
   to the branch again.)
1. Once the changes are addressed, merge the pull request.
:::


## Help and discussion

From here on out, we don't give detailed steps to the solution.  You
need to combine what you know, and the extra info below, in order to
solve the above.

### How to ask for changes in a pull request

Technically, there are at least two common ways to ask for changes in a pull
request.

Either in the comment field of the pull request:
:::{figure} img/code-review/comment.png
:width: 60%
:class: with-border
:alt: Screenshot of a pull request comment field
::::

Or by using the "Review changes":
:::{figure} img/code-review/files-changed.png
:width: 100%
:class: with-border
:alt: Screenshot of a pull request navigating to the "Review changes" tab
::::

And always please be kind and constructive in your comments. Remember that the
goal is not gate-keeping but **collaborative learning**.


### How to suggest a change in a pull request as a reviewer

If you see a very small problem that is easy to fix, you can suggest a change
as a reviewer.

Instead of asking the submitter to tiny problem, you can suggest a change by
clicking on the plus sign next to the line number in the "Files changed" tab:
:::{figure} img/code-review/leave-comment.png
:width: 100%
:class: with-border
:alt: Screenshot of leaving a comment to a line in a pull request
::::

Here you can comment on specific lines or even line ranges.

But now the interesting part is to click on the "Add a suggestion" symbol (the
one that looks like plus and minus). Now you can fix the tiny problem (in this
case a typo) and then click on the "Add single comment" button:
:::{figure} img/code-review/add-suggestion.png
:width: 60%
:class: with-border
:alt: Sequence of clicks to add a suggestion to a line in a pull request
::::

The result is this and the submitter can accept the change with a single click:
:::{figure} img/code-review/commit-suggestion.png
:width: 60%
:class: with-border
:alt: Screenshot of a pull request with a suggested change
::::

After accepting with "Commit suggestion", the improvement gets added to the
pull request.


### How to modify a pull request to address the review comments

If the reviewer asks for changes, it is not necessary to close the pull request
and later open a new one. It can even be counter-productive to do so: This can
fragment the discussion and the history of the pull request and can make it
harder to understand the context of the changes.

A much better mechanism to recognize that pull requests are not implemented
from a specific commit to a specific branch, but **always from a branch to a
branch**.

This means that you can make amendments to the pull request by adding new
commits to the same source branch. This way the pull request will be updated
automatically and the reviewer can see the new changes and comment on them.

The fact that pull requests are from branch to branch also strongly suggests
that it is a good practice to create a new branch for each pull request.
Otherwise you could accidentally modify an open pull request by adding new
commits to the source branch.
