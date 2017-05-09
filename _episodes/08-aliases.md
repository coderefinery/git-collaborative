---
layout: episode
title: "Aliases"
teaching: 10
exercises: 0
questions:
  - "How can I remember all these complex git commands?"
objectives:
  - "Learn to use aliases for most common commands"
keypoints:
  - "If you're frustrated about remembering a command, you should create an alias"
---

## What was that command again?

- git can do many things for you if you just know the right command
- the right command may not be intuitive and it may require multiple handles
- if you like a command you're likely to want to use it repeatedly

---

## Aliases

- aliases are a simple way to improve the usability of git
- aliases are based on simple string replacement in the command
- aliases can either be specific to a repository or global
  - global aliases help you do the things you're used to across git projects
  - per-project aliases can also be created

### A global alias

Global aliases

A simple shortcut
```shell
$ git config --global alias.co checkout
$ cd a_git_repo
$ git co [branch_name]
```

A more useful shortcut
```shell
$ git config --global alias.ls "log --graph --decorate --pretty=oneline --abbrev-commit"
$ cd a_git_repo
$ git ls
```

### A local alias

Local aliases are stored in .git/config and not syncronized with remotes.

```shell
$ cd a_git_repo
$ git config alias.who "shortlog -s --"
$ git who
```

### Using external commands

It's possible to call external commands using the exclamation mark character
"!".

```shell
$ cd a_git_repo
$ git config alias.hi '!echo hello'
$ git hi
```

## Food for thought: when to alias?

- How many times should you wait before aliasing a command?
- Do you believe a list of generic two-letter acronyms for common commands will
save your time?
