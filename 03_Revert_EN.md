# What is Git & GitHub? -- Revert

_🇯🇵 日本語版：[03_Revert.md](03_Revert.md)_

This section introduces `git revert` and explains how to undo files with Git.


## Outline <!-- omit in toc -->

* [Preparing for Time Travel](#preparing-for-time-travel)
  * [Local Git](#local-git)
  * [GitHub](#github)
  * [Create Sample Files and Branches](#create-sample-files-and-branches)
* [Revert: Rewind the Clock](#revert-rewind-the-clock)
  * [View the History](#view-the-history)
  * [GitHub - timeline branch](#github---timeline-branch)
  * [GitHub - timeline's commits](#github---timelines-commits)
* [Visit the Past](#visit-the-past)
* [Go Back One Commit](#go-back-one-commit)
* [Go Back by Commit Hash](#go-back-by-commit-hash)
* [Reset vs Revert](#reset-vs-revert)
* [Next Section](#next-section)


## Preparing for Time Travel


### Local Git

In the previous section, you created, merged, and deleted the `develop` branch.

Let's get down to just the `main` branch.
If you still have the `develop` branch, please delete it.

1. Move to the `learning_git` folder.

   ```sh
   cd ~/learning_git
   ```

2. Check the current Git status.

   ```sh
   git status
   ```

   ```terminal
   On branch develop
   Your branch is up to date with 'origin/develop'.
   nothing to commit, working tree clean
   ```

3. Check the branches in the repository.

   ```sh
   git branch
   ```

   ```terminal
   - develop
     main
   ```

4. Since you are on the `develop` branch, switch to `main`.

   ```sh
   git checkout main
   ```

   ```terminal
   Switched to branch 'main'
   Your branch is up to date with 'origin/main'.
   ```

5. Delete the `develop` branch.

   ```sh
   git branch --delete develop
   ```

   ```terminal
   warning: deleting branch 'develop' that has been merged to
            'refs/remotes/origin/develop', but not yet merged to HEAD.
   Deleted branch develop (was 4f98baf).
   ```

6. Let's also delete the develop_file.md file.

   ```sh
   rm develop_file.md
   ```


### GitHub

1. Go to the `learning_git` repository on GitHub.
   * github.com/`UserName`/learning_git
2. Check whether there is only one branch.
   * github.com/`UserName`/learning_git/branches
3. If there is a `develop` branch, [delete the branch](https://docs.github.com/en/github/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-and-deleting-branches-within-your-repository#deleting-a-branch).
   * ![03_Revert_DeleteBranch](img/03_Revert_DeleteBranch.png)

---


### Create Sample Files and Branches

Create files for time travel.

1. Switch to the `main` branch.

   ```sh
   git checkout main
   ```

2. Create a `timeline` branch.

   ```sh
   git checkout -b timeline
   ```

   ```terminal
   Switched to a new branch 'timeline'
   ```

3. Create the following files and commit them separately.
   * `yr_1`, `yr_2`, `yr_3`

   ```sh
   touch yr_1
   git add yr_1
   git commit -m "Year 1"
   ```

   ```sh
   touch yr_2
   git add yr_2
   git commit -m "Year 2"
   ```

   ```sh
   touch yr_3
   git add yr_3
   git commit -m "Year 3"
   ```


## Revert: Rewind the Clock


### View the History

You should have the following four files in the repository.

```sh
ls
```

```terminal
README.md   yr_1   yr_2   yr_3
```

`git log --oneline`

* Lists the commits on the branch.
* Use the commit hash it shows for the checkout and revert commands.

  ```sh
  git log --oneline
  ```

  ```terminal
  7a5bbf4 (HEAD -> timeline) Year 3
  5215f6d Year 2
  f10f791 Year 1
  03098e7 (origin/main, main) README file created
  ```

`git push origin timeline`

* The `timeline` branch is now pushed to GitHub.
* Visit the repository in your browser to confirm.

```sh
git push origin timeline
```


### GitHub - timeline branch

![03_Revert_timelineBranch](img/03_Revert_timelineBranch.png)


### GitHub - timeline's commits

![03_Revert_timelineBranch_Commits](img/03_Revert_timelineBranch_Commits.png)


## Visit the Past

`git log --oneline`

* Lists the commits on the branch.
* Use the commit hash it shows for the checkout and revert commands.

  ```sh
  git log --oneline
  ```

  ```terminal
  7a5bbf4 (HEAD -> timeline, origin/timeline) Year 3
  5215f6d Year 2
  f10f791 Year 1
  03098e7 (origin/main, main) README file created
  ```

`git checkout [commit hash]`

* Turns your working directory into the exact same state as that [`commit`].
* Use it to check whether this is the commit you want to undo.
* Any changes you make in this state are not saved.

  ```sh
  git checkout f10f791
  ```

  ```terminal
  Note: switching to 'f10f791'.

  You are in 'detached HEAD' state. You can look around, make experimental
  changes and commit them, and you can discard any commits you make in this
  state without impacting any branches by switching back to a branch.

  If you want to create a new branch to retain commits you create, you may
  do so (now or later) by using -c with the switch command. Example:

    git switch -c <new-branch-name>

  Or undo this operation with:

    git switch -

  Turn off this advice by setting config variable advice.detachedHead to false

  HEAD is now at f10f791 Year 1
  ```

  ```sh
  ls
  ```

  ```terminal
  README.md  yr_1
  ```


## Go Back One Commit

`git revert HEAD`

* Goes back one commit.

  ```sh
  git checkout timeline
  ```

  ```terminal
  Previous HEAD position was f10f791 Year 1
  Switched to branch 'timeline'
  ```

  ```sh
  ls
  ```

  ```terminal
  README.md  yr_1  yr_2  yr_3
  ```

  ```sh
  git revert HEAD
  ```

  ```terminal
  Removing yr_3
  [timeline 450d385] Revert "Year 3"
  1 file changed, 0 insertions(+), 0 deletions(-)
  delete mode 100644 yr_3
  ```

  ```sh
  ls
  ```

  ```terminal
  README.md  yr_1  yr_2
  ```


## Go Back by Commit Hash

```sh
git log --oneline
```

```terminal
2fb96f6 (HEAD -> timeline) Revert "Year 3"
7a5bbf4 (origin/timeline) Year 3
5215f6d Year 2
f10f791 Year 1
03098e7 (origin/main, main) README file created
```

Notice the `7a5bbf4 (origin/timeline) Year 3` line.
It means the `Revert "Year 3"` commit has not been applied on GitHub (origin) yet.

`git push`

```sh
git push origin timeline
```

```terminal
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 240 bytes | 240.00 KiB/s, done.
Total 2 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote: This repository moved. Please use the new location:
remote:   https://github.com/ahandsel/learning_git_3.git
To https://github.com/ahandsel/learning_git_3.git
   f0c82a0..53a0f3e  timeline -> timeline
```

![03_Revert_10.png](img/03_Revert_10.png)

`git log --oneline`

<span style="color:#AAAB25"> **727642d \(** </span> <span style="color:#38B9C7"> **HEAD \->** </span> <span style="color:#39C026"> **timeline** </span> <span style="color:#AAAB25"> **\,** </span> <span style="color:#CA3323"> **origin/timeline** </span> <span style="color:#AAAB25"> **\)** </span> **Revert "Year 3"**  
<span style="color:#AAAB25"> **f7cf1cb** </span> **Year 3**  
<span style="color:#AAAB25"> **f7fb07c** </span> **Year 2**  
<span style="color:#AAAB25"> **e4df7f2** </span> **Year 1**  
<span style="color:#AAAB25"> **03098e7 \(** </span> <span style="color:#CA3323"> **origin/main** </span> <span style="color:#AAAB25"> **\,** </span> <span style="color:#39C026"> **main** </span> **\) README file created**

`git revert f7fb07` Year 2 commit's hash

```sh
git revert 5215f6d

Removing yr_2
[timeline 6c3367a] Revert "Year 2"
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 yr_2
```

`git log --oneline`

<span style="color:#AAAB25"> **f3fc335 \(** </span> <span style="color:#38B9C7"> **HEAD \->** </span> <span style="color:#39C026"> **timeline** </span> <span style="color:#AAAB25"> **\)** </span> **Revert "Year 2"**

<span style="color:#AAAB25"> **727642d \(** </span> <span style="color:#CA3323"> **origin/timeline** </span> <span style="color:#AAAB25"> **\)** </span> **Revert "Year 3"**

<span style="color:#AAAB25"> **f7cf1cb** </span> **Year 3**

<span style="color:#AAAB25"> **f7fb07c** </span> **Year 2**

<span style="color:#AAAB25"> **e4df7f2** </span> **Year 1**

<span style="color:#AAAB25"> **03098e7 \(** </span> <span style="color:#CA3323"> **origin/main** </span> <span style="color:#AAAB25"> **\,** </span> <span style="color:#39C026"> **main** </span> <span style="color:#AAAB25"> **\)** </span> **README file created**

Revert

`ls`

README.md yr_1

`git push origin timeline`

git revert [commit hash]

`git revert [commit hash]`

* A forward-moving undo command.
* It reverses the changes made by the given [`commit`] and adds the result as a new commit.


## Reset vs Revert

| `git reset [commit]`                                                   | `git revert [commit]`                      |
| ---------------------------------------------------------------------- | ------------------------------------------ |
| A backward-moving undo that deletes commits.                           | A forward-moving undo.                     |
| Goes back to a past [`commit`] and removes every commit made after it. | Creates a new commit at a past [`commit`]. |
| This cleans everything up.                                             | No commits are deleted.                    |
| However, the history of the deleted commits is lost.                   | Use it for public or shared repositories.  |

![03_Revert_GitRevert.png](img/03_Revert_GitRevert.png)


## Next Section

[Git Cheat Sheet - 04_CheatSheet_EN.md](04_CheatSheet_EN.md)


## List of Lecture Guides <!-- omit in toc -->

[README_EN.md](README_EN.md) ⚙️
