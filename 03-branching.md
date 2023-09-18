# Branching
Diverge from the main line of development and continue to do work without messing with that main line.
- lightweight
- instantaneous
- switch fast

## 1. Branching in a Nutshell
### How Git Stores Data
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

### Underlying Basics
> a lightweight movable pointer to a commit: a simple file that contains 40 character SHA-1 checksum of the commit it points to.
> `git branch <branch>  # creates a new pointer to the same commit you're currently on.
> `git checkout <branch>    # switch to another branch: 1. move `HEAD` back to the object branch. 2. revert the files in working directory back to the the snapshot that `branch-name` points to.
> `git checkout -b <branch>     # create a new branch and switch to it at the same time.
> `git switch <branch>  # same as `git checkout`
> `git switch -c <branch>   # `-c` flag stands for create.
> `git switch -`    # return to the previous branch without specifying branch name.

`master`: default branch in Git, created by `git init` and automatically moves forward after every commit(pointing to the last commit).
`HEAD`: a pointer to the local branch you're currently on. Use `git log --decorate` to see which branch you're on. `git log` will only show commit history below the branch you've checked out, use `git log branch-name` or `git log --all` instead.

## 2. Basic Branching and Merging
It's best to have a clean working state when you switch branches: If you have uncommited changes that conflict with the branch you're checking out, Git won't let you do switch.

> ` git merge <branch-merge-in> <branch-merge-into>`  # merge branch to the current branch you're on, so remember to firstly switch to the branch you wich to merge into.
> ` git branch -d <branch>  # `-d` flag stands delete when successfully merging a branch.

### Fast-forward 
The pointer simply moves forward if you try to merge one commit with a commit that can be reached by following the first commit's history.(There is no divergent work to merge together) 

### Three-way Strategy
> The commit on the branch isn't a direct ancestor of the branch you're merging in.

Use two snapshots pointed to by the branch tips and the common ancestor of the two. Then create a new snapshot that results from these three snapshots and automatically create a new commit that points to it.(Thus it has more than one parent)

### Basic Merge Conflicts
1. If you change the same part of the same file differently in the two branches.
2. Git will pause the process of automatically creating a new commit.
3. Use `git status` to see which files are unmerged.
4. Open them manually(run `git mergetool` to use a graphical tool).
5. Standard conflit-resolution markers:
    - `<<<< branch-merge-into`
    - `=====`:seperates files
    - `>>>> branch-merge-in`
6. Either choose  one side or the other or merge the contents yourself.
7. Use `git add <file> to mark resolution`.
8. `git commit` to finalize the merge commit.(create default merge-conflict commit message)

