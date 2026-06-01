# What is Git & GitHub? -- Prep Guide

<!-- markdownlint-disable MD026 -->

_🇯🇵 日本語版：[00_Prep.md](00_Prep.md)_

This is a guide to get you ready for the `Intro to Git & GitHub` lecture.

Here are the steps to do in preparation for the lecture (in order):

1. [GitHub.com Account](#githubcom-account)
2. [Visual Studio Code (VS Code) + Command Line](#visual-studio-code-vs-code--command-line)
3. [Install Git](#install-git)
4. [GitHub Desktop App](#github-desktop-app)
5. [GitHub Command Line (GitHub CLI)](#github-command-line-github-cli)
6. [Configure Git](#configure-git)


## Outline <!-- omit in toc -->

* [GitHub.com Account](#githubcom-account)
  * [Step 1 - Create a GitHub.com Account](#step-1---create-a-githubcom-account)
  * [Step 2 - Set up Two-Factor Authentication](#step-2---set-up-two-factor-authentication)
* [Visual Studio Code (VS Code) + Command Line](#visual-studio-code-vs-code--command-line)
* [Install Git](#install-git)
  * [Install Git for MacOS](#install-git-for-macos)
  * [Install Git for Windows 10](#install-git-for-windows-10)
* [GitHub Desktop App](#github-desktop-app)
* [GitHub Command Line (GitHub CLI)](#github-command-line-github-cli)
  * [GitHub CLI for MacOS](#github-cli-for-macos)
  * [GitHub CLI for Windows](#github-cli-for-windows)
* [Configure Git](#configure-git)
  * [Add GitHub.com Login](#add-githubcom-login)
  * [Add GitHub Enterprise Login](#add-github-enterprise-login)
  * [Confirm GitHub Authentications were Successful](#confirm-github-authentications-were-successful)
  * [Default Branch - main](#default-branch---main)
* [Optional Setups](#optional-setups)
  * [Windows - Install cash](#windows---install-cash)
* [Next section - Basics and Settings](#next-section---basics-and-settings)

---


## GitHub.com Account


### Step 1 - Create a GitHub.com Account

Create a GitHub.com account by signing up here:

* [github.com/join](https://github.com/join)

Check out unsplash.com for free images to use for your profile pic:

* [unsplash.com/s/photos/cute](https://unsplash.com/s/photos/cute)
* [unsplash.com/s/photos/profile-dog](https://unsplash.com/s/photos/profile-dog)
* [unsplash.com/collections/410090/animals](https://unsplash.com/collections/410090/animals)


### Step 2 - Set up Two-Factor Authentication

1. Open GitHub.com's `Two-factor authentication` settings: [github.com/settings/security](https://github.com/settings/security)
   * Click on the `Enable two-factor authentication` button
   * Select `Set up using an app` option and click the `Continue` button
2. Scan the QR Code with a two-factor authentication app
   * Recommended two-factor authentication apps:
     * [1Password](https://1password.com/)
     * [Microsoft](https://www.microsoft.com/en-us/account/authenticator)
     * [Authy](https://authy.com/guides/github/)
     * [Enpass](https://www.enpass.io/)
3. Enter the 6-digit code from the two-factor authentication app
4. Download the recovery codes and click the `I have saved my recovery codes` button
5. Finally, click the `Done` button

Here is a gif that goes over Step 2:

* ![GitHub_Settings_TwoFactor.gif](./img/GitHub_Settings_TwoFactor.gif)


### Resources <!-- omit in toc -->

* GitHub Help Doc: [Configuring two-factor authentication - GitHub Docs](https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication)
* YouTube: [How to setup 2FA with GitHub](https://youtu.be/5DKqXeorDHY)

---


## Visual Studio Code (VS Code) + Command Line

Install VS Code from here:

* [code.visualstudio.com](https://code.visualstudio.com/)

Setup the ability to open VS Code from the command line:

1. Launch VS Code App
2. Open the `Command Palette` with the following shortcut:
   * Mac: `Command` + `Shift` + `P`
   * Windows: `Ctrl` + `Shift` + `P`
3. Type `shell` and select the `Shell Command: Install 'code' command in PATH` option
   * ![VSCode_shell_command.png](img/VSCode_shell_command.png)
4. Restart the Terminal
5. In the Terminal, type `code .` to open the current folder in VS Code

---


## Install Git

* [Install Git for MacOS](#install-git-for-macos)
* [Install Git for Windows 10](#install-git-for-windows-10)


### Install Git for MacOS

1. Install [Homebrew (brew.sh)](https://brew.sh/) with the following command:

   ```shell
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. Update and upgrade `brew` before installing new packages

   ```shell
   brew update && brew upgrade
   ```

3. Install git with Homebrew

   ```shell
   brew install git
   ```

4. Confirm the install by checking the git version

   ```shell
   git --version
   
   # If you see this, you are all set!
   git version 2.36.1
   ```


#### Debugging <!-- omit in toc -->

|                                     |                                       |
| ----------------------------------- | ------------------------------------- |
| If the following result is returned | `git version 1.7.10.2 (Apple Git-33)` |
| Run this command!                   | `brew link --force git`               |
| Or do this!                         | `export PATH=/usr/local/bin:$PATH`    |


#### Now you are ready! <!-- omit in toc -->

Next section is [GitHub Desktop App](#github-desktop-app)!

---


### Install Git for Windows 10

1. Install git for windows from [gitforwindows.org](https://gitforwindows.org/)
2. Accept the Installation Wizard's default setting EXCEPT for the following settings:
   1. For `Choosing the default editor used by Git` setting, select the `Use Visual Studio Code as Git's default editor` option
   2. For `Adjusting the name of the initial branch in new repositories` setting, select the `Override the default branch name for new repositories` option
   3. For `Configuring the line ending conversions` setting, select the `Checkout as is, commit as is` option
   4. For `Configuring the terminal emulator to use with Git Bash` setting, select the `Use Windows's default console window` option
   5. For the last settings page, select the `Launch Git Bash` option and deselect the `View Release Notes` option


#### Screenshots of the Installation Wizard settings <!-- omit in toc -->

The non-default settings are highlighted.

|                                                         |                                                         |
| ------------------------------------------------------- | ------------------------------------------------------- |
| ![windows_git_step_1.png](img/windows_git_step_1.png)   | ![windows_git_step_2.png](img/windows_git_step_2.png)   |
| ![windows_git_step_3.png](img/windows_git_step_3.png)   | ![windows_git_step_4.png](img/windows_git_step_4.png)   |
| ![windows_git_step_5.png](img/windows_git_step_5.png)   | ![windows_git_step_6.png](img/windows_git_step_6.png)   |
| ![windows_git_step_7.png](img/windows_git_step_7.png)   | ![windows_git_step_8.png](img/windows_git_step_8.png)   |
| ![windows_git_step_9.png](img/windows_git_step_9.png)   | ![windows_git_step_10.png](img/windows_git_step_10.png) |
| ![windows_git_step_11.png](img/windows_git_step_11.png) | ![windows_git_step_12.png](img/windows_git_step_12.png) |
| ![windows_git_step_13.png](img/windows_git_step_13.png) | ![windows_git_step_14.png](img/windows_git_step_14.png) |


#### Now you are ready! <!-- omit in toc -->

Next section is [GitHub Desktop App](#github-desktop-app)!

---


## GitHub Desktop App

1. Download the GitHub Desktop App from here: [desktop.github.com](https://desktop.github.com/)
2. Then click the `Sign in to GitHub.com` button
3. A browser window will launch
4. Log into your GitHub.com account by following the screenshots below:

|        |                                                   |        |                                                   |
| ------ | ------------------------------------------------- | ------ | ------------------------------------------------- |
| Step 1 | ![GitHubDesktop_1.png](./img/GitHubDesktop_1.png) | Step 2 | ![GitHubDesktop_2.png](./img/GitHubDesktop_2.png) |
| Step 3 | ![GitHubDesktop_3.png](./img/GitHubDesktop_3.png) | Step 4 | ![GitHubDesktop_4.png](./img/GitHubDesktop_4.png) |
| Step 5 | ![GitHubDesktop_5.png](./img/GitHubDesktop_5.png) | Step 6 | ![GitHubDesktop_6.png](./img/GitHubDesktop_6.png) |

GitHub Desktop App's documentation:

* English: [GitHub Desktop - GitHub Docs](https://docs.github.com/en/desktop)

---


## GitHub Command Line (GitHub CLI)

* [GitHub CLI for MacOS](#github-cli-for-macos)
* [GitHub CLI for Windows](#github-cli-for-windows)


### GitHub CLI for MacOS

1. Update and upgrade brew before installing new packages

   ```shell
   brew update && brew upgrade
   ```

2. Install [GitHub CLI](https://cli.github.com/) with the following command:

   ```shell
   brew install gh
   ```

3. Restart the computer before using GitHub CLI


#### Now you are ready! <!-- omit in toc -->

Next section is [Configure Git](#configure-git)!


### GitHub CLI for Windows

1. Install [GitHub CLI](https://cli.github.com/) by going to [cli.github.com](https://cli.github.com) and clicking on the `Download for Windows` button
2. Accept the Installation Wizard's default setting
3. Restart the computer before using GitHub CLI


#### Now you are ready! <!-- omit in toc -->

Next section is [Configure Git](#configure-git)!

---


## Configure Git


### Add GitHub.com Login

We will use GitHub CLI's `gh auth login` command to configure the GitHub login

Where to run the commands?

* For Mac users: Use the [Terminal](https://support.apple.com/guide/terminal/welcome/mac) for both git commands (`git`) and GitHub CLI commands (`gh`)
* For Windows users: Use the [Command Prompt](https://en.wikipedia.org/wiki/Cmd.exe) for both git commands (`git`) and GitHub CLI commands (`gh`)

Add GitHub.com login to your computer by going through the following steps:

1. Run `gh auth login` command
2. For `What account do you want to log into?` prompt, select `GitHub.com` option
3. For `What is your preferred protocol for Git operations?` prompt, select `HTTPS` option
4. For `Authenticate Git with your GitHub credentials? (Y/n)` prompt, type `y`
5. Copy the 9-character code and hit `enter`
6. A browser window will launch
7. Enter the 9-character code to the GitHub website
8. Click the `Authorize` button


### Add GitHub Enterprise Login

1. Run `gh auth login --hostname <hostname>` command
   * Example hostname: `github.dev.ahandsel.co.jp`
2. For `What is your preferred protocol for Git operations?` prompt, select `HTTPS` option
3. For `Authenticate Git with your GitHub credentials? (Y/n)` prompt, type `y`
4. Copy the 9-character code and hit `enter`
5. A browser window will launch
6. Enter the 9-character code to the GitHub website
7. Click the `Authorize` button


### Confirm GitHub Authentications were Successful

Confirm settings with the following command: `gh auth status`

This is what you want to see:

```shell
❯ gh auth status
github.com
  ✓ Logged in to github.com as ahandsel (/Users/***/.config/gh/hosts.yml)
  ✓ Git operations for github.com configured to use https protocol.
  ✓ Token: *******************

github.dev.ahandsel.co.jp
  ✓ Logged in to github.dev.ahandsel.co.jp as ahandsel (/Users/***/.config/gh/hosts.yml)
  ✓ Git operations for github.dev.ahandsel.co.jp configured to use https protocol.
  ✓ Token: *******************
```


### Default Branch - main

* `main` or `master` is set as the default branch name by git.
* The past default is `master` but now it is best-practice to use `main` (given the meaning of the world _master_ 😅)

Use the following command to set the default branch name to `main` for your computer.

```shell
git config --global init.defaultBranch main
```

---


## Optional Setups


### Windows - Install cash

1. Install [Node.js](https://nodejs.org/en/about/) on Windows
   * [Download | Node.js](https://nodejs.org/en/download/)
2. Verify Node.js installation by running the following command on Command Prompt
   * `node --version`
3. Install [dthree/cash](https://github.com/dthree/cash) so you can run Linux commands on Windows Command Prompt
   * Install command: `npm install cash-global -g`

---


## Next section - Basics and Settings

Go to the [Basics & First Repo - 01_Start_EN.md](01_Start_EN.md) section 💪


## List of Lecture Guides <!-- omit in toc -->

[README_EN.md](README_EN.md) ⚙️
