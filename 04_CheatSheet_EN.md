# Git Cheat Sheet

_🇯🇵 日本語版：[04_CheatSheet.md](04_CheatSheet.md)_

The following is an overview of useful Git command line (CLI) commands.

[GitHub Git Cheat Sheet - GitHub CheatSheet](https://training.github.com/downloads/github-git-cheat-sheet/)


## Create a repo

| Command                 | Explanation                                           |
| ----------------------- | ----------------------------------------------------- |
| `git init`              | Converts the current folder into a new Git repo       |
| `git clone [url]`       | Clone (download) a repo that already exists on GitHub |
| `git remote add origin` | Link the local repo to an empty GitHub repo           |

URL

* Template = `https://github.com/{UserName}/{repo}.git`
* Example = `https://github.com/ahandsel/Git_GitHub_Slides.git`


## Branches

| Command                    | Explanation                                          |
| -------------------------- | ---------------------------------------------------- |
| `git status`               | Lists all new or changed files that can be committed |
| `git branch [branch-name]` | Create a new branch                                  |
| `git branch -d [branch]`   | Deletes the specified branch                         |
| `git checkout [branch]`    | Move to the specified branch                         |
| `git merge [branch]`       | Merges the specified branch into the current branch  |


## Sync Changes Between Local & Remote

| Command                       | Explanation                                                                  |
| ----------------------------- | ---------------------------------------------------------------------------- |
| `git fetch [remote] [branch]` | Download the latest information from GitHub (remote repo) to your local repo |
| `git push [remote] [branch]`  | Upload (push) local repo commits to GitHub (remote repo)                     |
| `git pull [remote]`           | Updates current branch with all new commits from the remote branch (GitHub)  |

⚡ `git pull` is a combination of `git fetch` and `git merge` commands


## Snapshot

| Command                     | Explanation                                                          |
| --------------------------- | -------------------------------------------------------------------- |
| `git add [file]`            | Add a file from the working directory to the staging area            |
| `git status`                | Lists all new or changed files that can be committed                 |
| `git add -A`                | Add all new and modified files to the staging area                   |
| `git commit -m "[message]"` | Records file snapshots permanently in version history with a message |


## Make Changes

| Command                          | Explanation                                                                |
| -------------------------------- | -------------------------------------------------------------------------- |
| `git log`                        | Display the commit history in a list                                       |
| `git log --follow [file]`        | Shows a list of version history for the specified file, including renaming |
| `git diff [branch A] [branch B]` | Shows the difference between the two branches                              |
| `git show [commit]`              | Shows meta info and changes of the specified commit                        |


## Redo Commits

| Command               | Explanation                                     |
| --------------------- | ----------------------------------------------- |
| `git reset [commit]`  | Forces it back to the specified commit state    |
| `git revert [commit]` | Command to cancel the specified commit          |
| `git revert HEAD`     | Create a new commit to undo the previous commit |


## Done <!-- omit in toc -->

[README_EN.md](README_EN.md) ⚙️
