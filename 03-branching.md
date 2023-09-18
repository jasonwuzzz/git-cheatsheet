# Branching
Diverge from the main line of development and continue to do work without messing with that main line.
- lightweight
- instantaneous
- switch fast

## How Git Stores Data
commit object:
- a pointer to the snapshot(root project tree).
- commit message.
- author's name and email address.
- zero/one/mutiple pointers to its parent(s).

tree object
- contents of the directory.
- file names.

blob object:
- content of file.


## Underlying Basics
> a lightweight movable pointer to a commit: a simple file that contains 40 character SHA-1 checksum of the commit it points to.
> `git branch branch-name`  # creates a new pointer to the same commit you're currently on.
> `git checkout branch-name`    # switch to another branch: 1. move `HEAD` back to the object branch. 2. revert the files in working directory back to the the snapshot that `branch-name` points to.
> `git checkout -b branch-name`     # create a new branch and switch to it at the same time.
> `git switch branch-name`  # same as `git checkout`
> `git switch -c branch-name`   # `-c` flag stands for create.
> `git switch -`    # return to the previous branch without specifying branch name.

`master`: default branch in Git, created by `git init` and automatically moves forward after every commit(pointing to the last commit).
`HEAD`: a pointer to the local branch you're currently on. Use `git log --decorate` to see which branch you're on. `git log` will only show commit history below the branch you've checked out, use `git log branch-name` or `git log --all` instead.
