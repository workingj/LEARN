# [![Git](https://git-scm.com/images/logo@2x.png)](https://git-scm.com)

- [Git - Book](https://git-scm.com//book/en/v2)
- [Git Extension Pack - Don Jayamanne](https://marketplace.visualstudio.com/items?itemName=donjayamanne.git-extension-pack)
- [Top Visual Studio Code Git Extensions in 2020](https://www.youtube.com/watch?v=N8L6RJ5uZoE)
- A distributed version control system, each user has the entire repository on their computer
- Helps you maintain a detailed history of the project as well as the ability to work on different versions of it.
- Lets you jump back to any point in the project to recover data or files.

- [](#)
  - [Configure Git](#configure-git)
  - [Usefull Overview](#usefull-overview)
  - [Create repositories](#create-repositories)
  - [Branches](#branches)
  - [Commit](#commit)
  - [Push](#push)
  - [Redo commits](#redo-commits)
  - [Tags](#tags)
  - [Connect to a remote repository](#connect-to-a-remote-repository)
  - [Update from remote repository](#update-from-remote-repository)
  - [Check out a repository](#check-out-a-repository)
  - [Undo local changes](#undo-local-changes)
  - [Make changes](#make-changes)
  - [Synchronize changes](#synchronize-changes)
  - [The .gitignore file](#the-gitignore-file)
  - [Create a new local repository](#create-a-new-local-repository)
  - [Branches](#branches-1)
  - [Add one or more files to staging](#add-one-or-more-files-to-staging)
  - [Commit](#commit-1)
  - [Push](#push-1)
  - [Tags](#tags-1)
  - [Connect to a remote repository](#connect-to-a-remote-repository-1)
  - [Update from remote repository](#update-from-remote-repository-1)
  - [Check out a repository](#check-out-a-repository-1)
  - [Undo local changes](#undo-local-changes-1)
  - [Commands](#commands)
  - [Terminology](#terminology)
  - [Commit Message Guidelines](#commit-message-guidelines)
  - [HOW TO'S](#how-tos)
  - [Tipps](#tipps)
  - [git help](#git-help)

## Configure Git

- Configure **user** name to be used with your commits.
  `git config --global user.email`

- Configure the **email** address to be used with your commits.
  `git config --global user.email workingj@pm.me`

- Set the **default Editor**
  `git config --global core.editor "code --wait"`

- Enables helpful **colorization** of command line output
  `git config --global color.ui auto`

- **Alias** `git checkout` to `git co`
  `git config --global alias.co checkout`

### SSH

- SSH Key für Github.com generieren

  `console
ssh-keygen -t ed25519 -C "adress@server"
`

- Kopieren des SSH-Keys in den Zwischenspeicher und bei Github einfügen

  `console
clip < ~/.ssh/id_ed25519.pub
`

- SSH Zugang Testen & Fingerprint vergleichen:

  `ssh -T git@github.com`

  SHA256:uNiVztksCsDhcc0u9e8BujQXVUpKZIDTMczCvj3tD2s (RSA)
  SHA256:br9IjFspm1vxR3iA35FWE+4VTyz1hYVLIE2t1/CeyWQ (DSA – veraltet)
  SHA256:p2QAMXNIC1TJYWeIOttrVc98/R1BUFWu3/LiyKgUfQM (ECDSA)
  SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU (Ed25519)

## Usefull Overview

![Git Ebenen](./images/git_ebenen.png)

## Create repositories

A new repository can either be created locally, or an existing repository can be cloned. When a repository was initialized locally, you have to push it to GitHub afterwards.

- `git init` turns an existing directory into a new Git repository inside the folder you are running this command. After using the git init command, link the local repository to an empty GitHub repository using the following command:
- `git remote add origin [url]` Specifies the remote repository for your local repository. The url points to a repository on GitHub.
- `git remote -v` List all currently configured remote repositorie`
- `git clone [url]` Clone (download) a repository that already exists on GitHub, including all of the files, branches, and commits

## BRANCHES & MERGING

Isolating work in branches, changing context, and integrating changes
Any commits you make will be made on the branch you’re currently “checked out” to.

- `git status` to see which branch that is.
- `git branch` list your branches. a \* will appear next to the currently active branch
- `git branch -M main` rename master to main
- `git branch [branch-name]` create a new branch at the current commit
- `git branch -d [branch-name]` Deletes the specified branch

- `git checkout <branchname>` switch to another branch and check it out into your working directory
- `git checkout -b <branchname>` Create a new branch and switch to it

- `git switch -c [branch-name]` Switches to the specified branch and updates the working directory
- `git diff [sourcebranch] [targetbranch]` Preview changes, before merging
- `git merge [branch]` merge the speciﬁed branch’s history into the current one This is usually done in pull requests

- `git log` show all commits in the current branch’s history
- `git log --oneline` show all commits less verbose

## STAGING, COMMITING and SNAPSHOTS

Working with snapshots and the Git staging area

- `git status` show modiﬁed ﬁles in working directory, staged for your next commit
- `git add [file]` add a ﬁle as it looks now to your next commit (stage)
- `git add .` Add all files to staging for your next commit
- `git reset [file]` unstage a ﬁle while retaining the changes in working directory
- `git diff` diﬀ of what is changed but not staged
- `git diff --staged` diﬀ of what is staged but not yet committed
- `git commit -m “[descriptive message]”` commit your staged content as a new commit snapshot
- `git commit -a -m "message"` Commit any files you’ve added with git add, and also commit any files you’ve changed:

### Redo commits

Erase mistakes and craft replacement history

- `git reset [commit]` Undoes all commits after [commit], preserving changes locally
- `git reset --hard [commit]` Discards all history and changes back to the specified commit. CAUTION! Changing history can have nasty side effects

## PUSHING, SHARING & UPDATING

Retrieving updates from another repository and updating local repos

- `git remote add [alias] [url]` add a git URL as an alias
- `git fetch [alias]` fetch down all the branches from that Git remote
- `git merge [alias]/[branch]` merge a remote branch into your current branch to bring it up to date
- `git push [alias] [branch]` Transmit local branch commits to the remote repository branch
- `git pull` fetch and merge any commits from the tracking remote branch

- `git push origin master` Send changes to the master branch of your remote repository
- `git push --all origin` Push all branches to your remote repository:
- `git push origin :<branchname>` Push a branch into your remote repository:

## INSPECT & COMPARE

Examining logs, diffs and object information

- `git log` show the commit history for the currently active branch
- `git log branchB..branchA` show the commits on branchA that are not on branchB
- `git log --follow [file]` show the commits that changed file, even across renames
- `git diff branchB...branchA` show the diff of what is in branchA that is not in branchB
- `git show [SHA]` show any object in Git in human-readable format

## Tags

1. `git tag 1.0.0 < commitID >` You can use tagging to mark a significant changeset, such as a release. CommitId is the leading characters of the changeset ID, up to 10, but must be unique.
2. `git log` Get the ID using:
3. `git push --tags origin` Push all tags to remote repository:

## Undo local changes

1. `git checkout -- <filename>` You can replace the changes in your working tree with:
2. `git fetch origin git reset --hard origin/master` To drop all your local changes and commits, fetch the latest history from the server and point your local master branch at it, do this:

- `git restore index.html` will undo all uncommitted local changes in the specified file. Please be careful because you cannot get these changes back once you've discarded them!

## The .gitignore file

Sometimes it may be a good idea to exclude files from being tracked with Git. This is typically done in a special file named `.gitignore`. You can find helpful templates for `.gitignore` files at [github.com/github/gitignore](https://github.com/github/gitignore).

## Commands

### **[`git init`](https://git-scm.com/docs/git-init)**

[Git Basics - Getting a Git Repository](https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository#Initializing-a-Repository-in-an-Existing-Directory)

- Creates a repository and does all of the initial setup.
- The `.git` directory is the "repository" where git records all of the commits, configuration files and keeps track of everything! _Never directly edit any files inside the .git directory_

`git init`

### **[`git clone`](https://git-scm.com/docs/git-clone)**

[Cloning an Existing Repository](https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository#_git_cloning)

- takes the path to an existing repository
- by default will create a directory with the same name as the repository that's being cloned
- can be given a second argument that will be used as the name of the directory
- will create the new repository inside of the current working directory
- has a number of different transfer protocols you can use. `https://`, `git://`, ssh...

- `git clone <path-to-repository>`
- `git clone <path-to-repository> <new-folder name>`

### **[`git status`](https://git-scm.com/docs/git-status)**

[Recording Changes to the Repository](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository#Checking-the-Status-of-Your-Files)

- will display information depending on the state of your files, the working directory, and the repository
- You should always run the git status command. Especially when returning to a project after a period of time.

`git status`

### **[`git log`](https://git-scm.com/docs/git-log)**

[Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)

- Show logs for all existing commits
- displays by default: SHA, author, date, commit message
- **Navigating** The Log: `one line | half the page | whole page`

  - scroll **down: `↓ o. j, d, f`**
  - scroll **up: `↑ o. k, u, b`**
  - **quit: `q`**

- `git log` # Zeige das ganze Log
- `git log <sha>` # Zeige nur Commit mit passendem sha
- `git log --grep <text>` # Suche nach Commits mit beinhaltetem text
- `git log --author` # Zeige nur commits von diesem Author
- `git log --oneline` # In nur einer Zeile
- `git log --stat` # Zeigt wieviel und welche Dateien wie oft verändert wurden
- `git log -p|--patch` # displays the files and the location of the lines that
  have been modified and the actual changes that have been made
- `git log --stat -p` # Display the stats info above the patch info
- `git log -p -w` # Ignores all whitespace changes

### **[`git show`](https://git-scm.com/docs/git-show)**

- Displays only Info about the given commit
- [Generating patch text with -p](https://git-scm.com/docs/git-diff#_generating_patch_text_with_p)

git show
`git show <sha>` # Jump to commit with given sha
git show --stat# Zeigt wieviel und welche Dateien wie oft verändert wurden
`git show -p|--patch` # displays the files and the location of the lines that
have been modified and the actual changes that have been made
`git show --stat -p` # Display the stats info above the patch info
`git show -w` # Ignores all whitespace changes

### **[`git diff`](https://git-scm.com/docs/git-diff)**

- Show changes that have been made, changes between commits, commit and working tree, etc

`console
git diff
`

### **[`git add`](https://git-scm.com/docs/git-add)**

- to move files from the Working Directory to the Staging Index (staging)

`bash
git add <file>
git add <folder/file> <folder/file>`
git add . # Add all files and nested files
`

### **[`git rm`](https://git-scm.com/docs/git-rm)**

- removes files from the Staging Index. (unstage)

`console
git rm --cached <file>
`

### **[`git commit`](https://git-scm.com/docs/git-commit)**

- Record changes to the repository
- **each commit should have a single focus.**
- a commit message must be supplied, lines that start with a `#` are comments and will not be recorded
- **keep the message short, explain what the commit does**

`console
git commit # opens the default editor
git commit -m "Initial commit" # bypass editor
`

### **[`git config`](https://git-scm.com/docs/git-config)**

[Customizing Git - Git Configuration](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration)

`console
git config --list  `
`

## Terminology

### Branch

A branch is when a new line of development is created that diverges from the main line of development. This alternative line of development can continue without altering the main line.
Going back to the example of save point in a game, you can think of a branch as where you make a save point in your game and then decide to try out a risky move in the game. If the risky move doesn't pan out, then you can just go back to the save point. The key thing that makes branches incredibly powerful is that you can make save points on one branch, and then switch to a different branch and make save points there, too.

### Checkout

A checkout is when content in the repository has been copied to the Working Directory.
Staging Area / Staging Index / Index
A file in the Git directory that stores information about what will go into your next commit. You can think of the staging area as a prep table where Git will take the next commit. Files on the Staging Index are poised to be added to the repository.

### Commit

Git thinks of its data like a set of snapshots of a mini filesystem. Every time you commit (save the state of your project in Git), it basically takes a picture of what all your files look like at that moment and stores a reference to that snapshot. You can think of it as a save point in a game - it saves your project's files and any information about them.

### Repository / repo

A Git repository is a virtual storage of your project. It allows you to save versions of your code, which you can access when needed.
A repository is a directory which contains your project work, as well as a few files (hidden by default on Mac OS X) which are used to communicate with Git. Repositories can exist either locally on your computer or as a remote copy on another computer. A repository is made up of commits.

### SHA

A SHA isan ID number for each commit. It is a 40-character string composed of characters (0–9 and a–f) and calculated based on the contents of a file or directory structure in Git.

### Staging Index

### VCS / SCM

Version Control System / Source Code Manager

### Working Directory

The Working Directory is the files that you see in your computer's file system. When you open your project files up on a code editor, you're working with files in the Working Directory.
This is in contrast to the files that have been saved (in commits!) in the repository.
When working with Git, the Working Directory is also different from the command line's concept of the current working directory which is the directory that your shell is "looking at" right now.

## Commit Message Guidelines

[Udacity Git Commit Message Style Guide](https://udacity.github.io/git-styleguide/)

### Good Commit Messages

- **Do**

  - do keep the message short (less than 60-ish characters)
  - do explain what the commit does (not how or why!)

- **Do not**

  - do not explain why the changes are made (more on this below)
  - do not explain how the changes are made (that's what git log -p is for!)
  - do not use the word "and" if you have to use "and", your commit message is probably doing too many changes - break the changes into separate commits e.g. "make the background color pink and increase the size of the sidebar"

The best way thatis to come up with a commit message is to finish this phrase, "This commit will...". However, you finish that phrase, use that as your commit message.

**Above all, be consistent in how you write your commit messages!**

### Explain the Why

When you're writing the commit message, the first line is the message itself. After the message, leave a blank line, and then type out the body or explanation including details about why the commit is needed
This details section of a commit message is included in the `git log`

## HOW TO'S

### how to create a pull request on a public repo

1.  fork the repo on the website
2.  git clone your fork to your machine
3.  create a new branch on your local clone
    `git checkout -b name-of-the-branch`
4.  do your edits
    1.  to see your changes
        `git status`
        `git diff`
5.  add your files to the staging index
    `git add <file>`
6.  commit your changes to the repository
    `git commit -m "your message"`
7.  Push the repository to the GitHub
    `git push origin 'branch-name'`
    or:
    `git pull-request (?)`
8.  on the github website create the Pull request

## Tipps

- Nicht zu viel Zeit lassen bis zum Pull request damit sich nciht zu viele changes aufstauen
- Immer wieder Locales mergen von remotechanges in main oder eigene branches um mit aktueller Version zu arbeiten
- mit Team absprechen das es pullrequests gab auf main und jeder seinen working branches updated

## git help

https://www.datacamp.com/community/tutorials/git-push-pull

https://www.youtube.com/watch?v=rgbCcBNZcdQ

https://swcarpentry.github.io/git-novice/
