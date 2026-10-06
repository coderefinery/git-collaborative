# Non-bare and bare repositories

```{objectives}
- Understanding the difference between non-bare and bare repositories.
- Being able to create a common repository for a group on our local computer or server.
```

```{instructor-note}
- 10 min teaching/demonstration
```


## Non-bare repository

- A **non-bare repository** contains `.git/` as well as a snapshot of your
  tracked files that you can directly edit called **the working tree** (the
  actual files you can edit).
- **This is where we edit and commit changes**.
- When we create a repository with `git init`, it is a non-bare, "normal", repository.


## Bare repository

- A **bare repository** contains only the `.git/` part, no files you can directly edit.
- By convention the names of bare repositories end with `.git` to emphasize this.
- We never do actual editing work inside a bare repository.
- GitHub, GitLab, etc. store a bare repository.
- You can also create a bare repository on your computer/server to store your private repository.

If we have enough time, the instructor demonstrates how to create a bare
repository on the local computer:

````{exercise} Bare-1: Create and use a bare repository
- Create a new local repository with `git init`.
  ```console
  $ cd /path/to/example
  $ git init
  ```
- Populate it with a file and a commit or two.
- Create one or two branches.
- Clone this repository on the same computer with either `--bare` or `--mirror`:
  ```console
  $ git clone --bare /path/to/example /path/to/example-bare
  ```
- Inspect the bare repository.
- Clone the bare repository:
  ```console
  $ git clone /path/to/example-bare /path/to/example-clone
  $ cd /path/to/example-clone
  ```
- Inside the clone inspect `git remote -v`.
- Inside the clone create a commit and push the commit to `origin`.
- The bare repository can be cloned several times and one can exercise pushing and pulling changes.
````

```{keypoints}
- We do programming work inside non-bare repositories.
- We can create a local common bare repository where we can push to and pull from.
```
