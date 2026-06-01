# English GitHub Lecture Notes

Markdown/ Outline version of the content


## Outline <!-- omit in toc -->

<!-- markdownlint-disable MD007 -->

* [Hands-on A Overview](#hands-on-a-overview)
  * [Local Configuration](#local-configuration)
  * [GitHub Configuration](#github-configuration)
  * [Linking Local \& GitHub](#linking-local--github)
  * [Create a Local Git Repository](#create-a-local-git-repository)
  * [Add a README.md file to the Local Repo](#add-a-readmemd-file-to-the-local-repo)
  * [Check Git's Status](#check-gits-status)
  * [Saving #1 \* Add a File to Git's Staging Area](#saving-1--add-a-file-to-gits-staging-area)
  * [Saving #2 \* Add a File to Git Repo](#saving-2--add-a-file-to-git-repo)
  * [Create a GitHub Repository](#create-a-github-repository)
  * [Local Git :arrow\_forward: GitHub](#local-git-arrow_forward-github)
  * [Hands-On A is Completed](#hands-on-a-is-completed)
* [Hands-On A's Concepts](#hands-on-as-concepts)
  * [Saving Changes with Git](#saving-changes-with-git)
  * [Working with Remote Repos](#working-with-remote-repos)
  * [git push \[remote\] \[branch\]](#git-push-remote-branch)
  * [Hands-on A Review](#hands-on-a-review)
  * [Hands-on A Quiz Time](#hands-on-a-quiz-time)
* [Hands-on B - Make \& Merge Branches](#hands-on-b---make--merge-branches)
  * [Create a New Branch](#create-a-new-branch)
  * [Changing develop Branch](#changing-develop-branch)
  * [Confirming the Change on GitHub](#confirming-the-change-on-github)
  * [Create \& Merge Pull Request](#create--merge-pull-request)
  * [GitHub repo -\> Update Local repo](#github-repo---update-local-repo)
* [What are branches? - Overview of Hands-on B](#what-are-branches---overview-of-hands-on-b)
  * [Git Branches](#git-branches)
  * [Branches - Website](#branches---website)
  * [Git Push vs Pull - Teamwork](#git-push-vs-pull---teamwork)
* [GitHub Workflow](#github-workflow)
  * [#1 - Create a Branch](#1---create-a-branch)
  * [#2 - Making a Commit](#2---making-a-commit)
  * [#3 - Open a Pull Request](#3---open-a-pull-request)
  * [#4 - Test](#4---test)
  * [#5 - Merge to main](#5---merge-to-main)
  * [Overview of GitHub Workflow](#overview-of-github-workflow)

---


## Hands-on A Overview

---


### Local Configuration

Create a folder
Configure it to be managed by git


### GitHub Configuration

* Create a "folder" like thing on GitHub
* It is called repository


### Linking Local & GitHub

* Configure the two to be linked
* Create a file on the local side and run git commands, the file will appear on GitHub.com


### Create a Local Git Repository

* With your terminal, go to Documents and create a directory named `learning_git`
  * `pwd ~/Documents/learning_git`
* In this folder, using the `git init` command, initialize a repository
* Repository is often shortened to Repo


### Add a README.md file to the Local Repo

* Create a README.md file
  * README file is used to describe a software/ git repo's purpose and usage.
* Open the current learning_git directory with VS Code
* Add a description of your repository in the markdown file


### Check Git's Status

* git status
* command that shows the working directory's & staging area's state
* **Changes to be committed**:
  * You can see which changes have & have not been staged
* **Untracked files**:
  * You can see which files are not being tracked by git
* See that the README.md needs to be tracked by git


### Saving #1 \* Add a File to Git's Staging Area

* git add [file/folder]
* command to add the [file/folder] to the staging area
* Now the README.md is now in staging area
* We prepped the file! Now it is GREEN!
* Next, we need to commit the file to have git track the changes


### Saving #2 \* Add a File to Git Repo

* git commit -m "message"
* command to add the file/folder to the repository
* Now the README.md is now in the repository
* specifically the main branch
* git commit commands makes git fully track the file
* Similar to the game check-point
* -m is the adding message option
* It is important to include the purpose of the changes as commit's message for teamwork + history


### Create a GitHub Repository

* Create a Repository
  * <https://github.com/new>
* Name your repository learning_git
* Do not initialize repository with README!


### Local Git :arrow_forward: GitHub

* Push the existing repository!
  * Get the URL by clicking on `Clone or download` button & copying the HTTPS link
* `git remote add origin <link>`
  * connects the git managed local repository with GitHub's remote
* `git remote`
* command to manage the remote repos


### Hands-On A is Completed

* Install & Configure git on PC
* Create & Configure GitHub
* Create & push a local repository

---


## Hands-On A's Concepts

---


### Saving Changes with Git

* There are 2 commands to transfer the items between the "locations"
* There are 3 "locations" where files, folders, and changes are stored


#### working directory

* the current local directory that you are working on.
* all changes first takes place here


#### git add

* command that promotes a change from working directory to staging area


#### staging area

* the buffer between the working directory & the repository
* used to be called the 'index'
* the promoted changes are bundled together, waiting for the next commit


#### Why have Staging Area?

* To stage a file = prepare the file for a commit


##### Staging Area Metaphor

* Imagine you are making music
  * You write various songs with varying messages. (Everything from a hateful to a loving songs)
  * Now do you want to upload all your music randomly?
  * No, you want to upload the songs bundled as albums with a theme.
* To make a romantic album:
  * you `git add` only your love songs
  * As you are still looking for and selecting songs to add to the album, the selected songs are stored in the `Staging Area`
  * Once you have all the songs you want in the album stored in the `Staging Area`, time to commit!
  * you `git commit -m` with the album title, "Love Song"


#### git commit

* command to record changes to the repository
* used once all the files with the changes you want to be saved are in staging area
* Game Check-In
* it is like when you defeated the boss & want to save your progress in the game
* comments per commit provides a natural documentation


#### repository

* git repository is the actual ".git" folder inside a project
* the folder tracks all the changes made in the project
* i.e. the historian
* remote repository (GitHub)
* the repository on GitHub's server, allowing the code to be viewed by others


### Working with Remote Repos

* `git remote add origin <link>`
* git creates an alias of the remote repository when you clone a remote repository to your local machine
* i.e. nickname is assigned per remote repository's URL
* Most common alias is called "origin."
* Thus, both following commands does the same thing:
  * git push -u <https://github.com/user/repo.git> main
  * git remote add ALIAS <https://github.com/ahandsel/repo.git>
  * git push -u ALIAS main


#### git remote command

* manages the connection between your local & remote repositories


#### git remote --verbose

* lists out the URLs that Git has stored & alias (nickname) that can be used when reading & writing to that remote repo


### git push [remote] [branch]

* command to upload local repo content to a remote repo
* i.e. export the commits from your local -> remote repo
* counterpart to git fetch (import commits to local repo)

Note: Pushing can potentially overwrite changes!

* git push command works only for remote repo that has not been modified since your last push or clone
  * i.e. No one else changed the remote repo after you
  * if you & another user cloned at the same time and they push upstream before you, your push will rightly be rejected
  * you will need to fetch their work and include it in your push first


### Hands-on A Review

* Saving with Git
* git remote
  * Command to manage the connection between the local & remote repos
* git push
  * Command to upload local repo content to a remote repo


### Hands-on A Quiz Time

* Q1: How is Git & GitHub related?
  * Hint: "hub" means the center of an activity or network.
* Q2: Which comes first, `git add` or `git commit`?
  * Hint: "commit" means to pledge yourself to a certain action (like marriage).
* Q3: What does `git push` command do?
  * Hint: "git push" command does the opposite of "git fetch" command.

= = = = = = = = =


## Hands-on B - Make & Merge Branches

---


### Create a New Branch

* By default, a repository has a **main** branch
* Let's create a new branch named **develop**
* `git checkout -b <branch_name>`
  * command to create a new branch & switch to it
* `git branch`
  * command to view a list of branches
  * current branch has the asterisk (\*)

```sh
$ git checkout -b develop
Switched to a new branch 'develop'

$ git branch
* develop
main
```


### Changing develop Branch

* While being in the **develop** branch, create a file.
* Run `git add` and `git commit` to save it to the local repo.
* Run `git status` to confirm the changes.
* Run `git push` to push the changes to GitHub repo

```sh
$ touch develop_file.md
$ git add develop_file.md
$ git commit -m "develop only"
[develop f946eb0] File only in develop branch
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 develop_file.md
$ git status
On branch develop
nothing to commit, working tree clean
$ git push -u origin develop
```

---


### Confirming the Change on GitHub

* Only the develop branch included the new file
* Add another file in develop branch
* Then view the Network graph
  * `https://github.com/USER/REPO/network`


### Create & Merge Pull Request

* **Pull Requests** shows others your changes without actual modifying
  * useful for code review
* On GitHub, create the **pull request** to merge **develop** -> **main** branch
* Confirm the changes and **Merge** Pull request
* This results in **main** branch having the two new files!


### GitHub repo -> Update Local repo

* Currently, your GitHub repo is ahead of the local copy
  * Use `git pull` command to address this
* `git pull origin main`
  * pull the latest repo version from GitHub to the local repo
* Following commands
  * `git checkout main`
  * `git pull origin main`
  * `git branch -d develop`
  * `git branch`
* Outcome:

  ```sh
  $ git checkout main
  Switched to branch 'main'
  Your branch is behind 'origin/main' by 4 commits & can be fast-forwarded
    (use "git pull" to update your local branch)

  $ git pull origin main
  remote: Enumerating objects: 1, done.
  remote: Counting objects: 100% (1/1), done.
  remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
  Unpacking objects: 100% (1/1), 631 bytes | 210.00 KiB/s, done.
  From https://github.com/ahandsel/learning_git
  * branch            main     -> FETCH_HEAD
    5f9f89b..1438ca5  main     -> origin/main
  Updating d775d42..1438ca5
  Fast-forward
  2nd_file.md     | 0
  develop_file.md | 0
  2 files changed, 0 insertions(+), 0 deletions(-)
  create mode 100644 2nd_file.md
  create mode 100644 develop_file.md

  $ git branch -d develop
  Deleted branch develop (was c6e6c83).

  $ git branch
  * main
  ```

---


## What are branches? - Overview of Hands-on B


### Git Branches


#### What are branches?

* movable pointer to a `git commit`
* mechanism that manages multiple timelines, allowing for changes without impacting the main line
* `git checkout`
  * command to switch branches
* `git branch -d <branch-name>`
  * command to delete branches


#### Why use branches?

* allows for a separation between stable, in-development, and experimental changes
* Example: This GitHub Slides
  * Each Hands-on and concept section can be a branch.
  * Each can be developed in parallel.


### Branches - Website

* main branch contains the 'live' code that runs the website.
* changes in main impacts users
* Two coders want to modify the website at the same time.
  * Make 3x branches:
  * main -> live code
  * feature_A -> for coder A to modify
  * feature_B -> for coder B to modify
* Once the code developments are done, merge the branches.


### Git Push vs Pull - Teamwork


#### `git push`

* the 'upload' command
* "Push" is forcing the changes to the target repo.
  * `[ your code ] -- pushing → [target]`
* A "push request" would be the target repo requesting you to push your changes.


#### `git pull`

* the 'download' command
* "Pull" is the target repo grabbing your changes
  * `[ your code] }-- pulling -- [target]`
* A "pull request" is you requesting the target repository to please grab your changes.


## GitHub Workflow


### #1 - Create a Branch

* The code for the **live** website is in the **main** branch
* Any changes to here will effect the users!
* If you want to create a new page, first create a new **feature** branch.
  * This is where you will do the development for the new page.
* `git checkout -b develop`, `git branch`


### #2 - Making a Commit

* In your **feature** branch, you are modifying code.
* Each time you want to save a change, make a `commit`.
* This keeps track of changes and provides a transparent history.
* Commits allow for roll backs and references.


### #3 - Open a Pull Request

* When you are ready to share your changes to others, open a **Pull Request**.
* Pull Requests are the start of code review.
* Make & review comments at the Pull Request tab on GitHub.


### #4 - Test

* After code review, deploy your code in a testing environment to make sure everything works.
* Example: Test if the website looks and acts as expected on _Zendesk Preview_ mode.


### #5 - Merge to main

* Merge your code into the **main** branch.
* Now your changes are live & visible to the users.
* Once merged, **Pull Requests** acts as reference points.
* Example: Pull Request for new logo will become a reference point to indicate the "before" and the "after" of the logo change.


### Overview of GitHub Workflow

* <https://commonflow.org/spec/1.0.0-rc.5.html>
