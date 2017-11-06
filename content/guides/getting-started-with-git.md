+++
title = "Getting Started With Git"
date = "2017-10-17T20:03:45-07:00"
hide_authorbox = true
disable_comments = true
draft = false
enable_toc = true
+++

# Installation

Download Git from one of the links on [this page](https://git-scm.com/downloads).

You can also install one of the graphical programs for Git, but for this guide we will be using the command-line commands.

# Configuration

Git requires a few options to be set up before you can do any work on a git repository, so we'll set them up now. Use the below commands, replacing the name and email with your own.

```bash
$ git config --global user.email "joe.smith@example.com"
$ git config --global user.name "Joe Smith"
```

If you're running a Linux system, the default editor on your system is probably Vi(m). To change this for git, you can run this command (replace `nano` with your preferred editor).

```bash
$ git config --global core.editor "nano"
```

# Creating A New Repository

Open the terminal program on your computer. If you're on Windows, we recommend using the "Git Bash" program instead of Command Prompt, though you can use both.

Navigate to the folder you want to contain your git repository. For this example, we'll use the user's `Documents` folder. You do this on all systems using the `cd` command.

<!-- Also %HOMEPATH% -->
**Windows (Command Prompt):**

```batchfile
> cd %USERPROFILE%\Documents
```

**Windows (Git Bash)/Mac/Linux:**

```bash
$ cd $HOME/Documents
```

Now create and switch to a directory that will contain your new git repository. For the sake of this guide, we'll call it `hello-world`.

**All systems:**

```bash
$ mkdir hello-world && cd hello-world
```

We're going to initalize a new git repository in this folder.

**All systems:**

```bash
$ git init
Initialized empty Git repository in /home/joesmith/Documents/hello-world/.git/
```

Run `git status` to check the state of your new repository.

```bash
$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

Congratulations! You've created a new git repository.

# Adding Changes To The Staging Area

Now that we have a git repository, let's start adding files to it.

The first thing to do is to create a file. You can do this from the command-line:

**Windows (Command Prompt):**

```batchfile
> copy NUL hello-world.txt
```

**Windows (Git Bash)/Mac/Linux:**

```bash
$ touch hello-world.txt
```

To add changes to the repository, we use the `git add` command.

**All systems:**

```bash
$ git add hello-world.txt
```

The `git add` command can take any number of files and/or folders as arguments, so this is also valid:

```bash
$ git add README.md main.h main.c tests/
```

Now run `git status` to see the new state of your repository.

```bash
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

      hello-world.txt

nothing added to commit but untracked files present (use "git add" to track)
```

## Removing Staged Files

A subset of adding changes to the staging area is *deleting* files. To delete a file from the repository, you use the `git rm` command. So, to delete the file we just created (assuming it's being tracked by Git), we would use this command:

```bash
$ git rm hello-world.txt
```

This command will remove the file from the repository *and delete the file from the disk*. To only stop Git from tracking the file and *keep* the file itself, use the `--cached` flag.

```bash
$ git rm --cached hello-world.txt
```

## Viewing Changes

If you aren't sure what changes you've made to a tracked file, you can run the `git diff` command to view them.

{{% alert %}}
`git diff` only shows changes in tracked files because, as far as Git is concerned, untracked files don't exist. So, once they are added to the repository, the full contents are what has changed.
{{% /alert %}}

There are two different ways to run the `git diff` command. On its own, `git diff` displays all *not yet staged* changes to all tracked files. To view changes that have been added to the staging area (via `git add [filename]`), add the `--staged` flag: `git diff --staged`.

## Committing Staged Changes

The next step is to "commit" some changes to the repository. The command for this is `git commit`. There are a few ways this command can be run, depending on what you want to do. Each command takes a "commit message," or a short description of what has been changed in all of the files in this commit.

{{% alert %}}
If you get an error running one of these `git commit` commands that says "Please tell me who you are," go back to the [Configuration](#configuration) section and set your name and/or email address.
{{% /alert %}}

- `git commit`: This command will open the default editor and allow you to type a commit message in a temporary file. Once the editor exits, git will process the file and make the commit.
- `git commit -m "Commit message"`: This command takes the commit message as a parameter instead of opening an editor. `-m` can be repeated per line in the commit message.
- `git commit -a`: This command automatically adds the changes to all files already tracked by Git (all modifications and deletions, but not new files). It opens a text editor to write the commit message, but can use the `-m` flag to avoid that.

```bash
$ git commit -m "Hello, World!"
```

{{% alert %}}
If you accidentally committed something, and want to undo the commit, you can use the command `git reset HEAD~1`. This will remove the last commit while leaving the changes intact. It will **not** work if you are trying to undo the only commit in the repository. If you want to **add** something to the commit you just made, just add the changes to staging and use `git commit --amend` - it will overwrite the previous commit with the new changes.
{{% /alert %}}

## Creating Branches

Branches are Git's way of separating out different work items. Branches create their own commit history starting from the time of branching, thus allowing you to switch what you are working on without losing all of the changes you made to something else. The "main" branch of a Git repository is usually the `master` branch, while work tends to happen in other branches. A normal repository might look something like this, for instance:

- `master`: The main "stable" version of the code.
- `development`: The branch where "unstable" development code eventually ends up.
- `feature_1`: Working on adding a new feature to the codebase.
- `issue_26`: Working on resolving issue #26, whatever that is.
- And so on.

There is a `git branch` command, but it's easier to use the `git checkout` command for making a new branch instead, because `git checkout` will automatically switch to the new branch while `git branch` will stay on the current one. The `-b` flag tells `git checkout` to create the new branch.

```bash
$ git checkout -b new_branch
```

You can then use `git branch` to view the branches in the repository.

```bash
$ git branch
  master
* new_branch
```

You can switch to another existing branch using the `git checkout` command without the `-b` flag.

```bash
$ git checkout master
Switched to branch 'master'
$ git branch
* master
  new_branch
```

To delete a branch, add the `-d` flag to `git branch`.

```bash
$ git branch -d new_branch
Deleted branch new_branch (was 9b1f478).
```

## Merging Changes Between Branches

Let's take another look at the example branches from the last section:

- `master`: The main "stable" version of the code.
- `development`: The branch where "unstable" development code eventually ends up.
- `feature_1`: Working on adding a new feature to the codebase.
- `issue_26`: Working on resolving issue #26, whatever that is.
- And so on.

The way that these branches are set up, code is eventually going to make its way from `feature_1` or `issue_26` to `development` and then to `master`. To do this, we use the `git merge` command. For example, the following commands will merge the `issue_26` branch into `development`:

```bash
$ git checkout development
$ git merge issue_26
```

If the `development` branch hasn't changed since the `issue_26` branch was created, the changes to `issue_26` will be "replayed" on `development`, and the merge is done.

This is usually not the case, though. Other issues have probably been fixed since our developer started on issue #26, and these changes would have been merged to `development` already. Sometimes Git can safely automerge the changes - if the files `issue_26` changed weren't changed in `development`, for instance - but this isn't always the case.

If two different histories have changes to the same part of the same file, this is known as a **merge conflict**. Merge conflicts need to be manually resolved by a developer before the changes can be committed. Git comes with a built-in command called `git-mergetool` [docs](https://www.git-scm.com/docs/git-mergetool) that can use a merge resolution program on your computer to help with merging, or you can open the conflicting file(s) in an editor and manually resolve the conflict. GitHub provides some [documentation](https://help.github.com/articles/resolving-a-merge-conflict-using-the-command-line/) on how to manually resolve a merge conflict.

# Working With Remote Repositories

Making and committing changes are nice for doing homework, but your work is still only on your computer. The next step is creating a central remote repository that you can send your changes to.

## Cloning

The process of downloading a copy of a remote git repository to your computer is called *cloning*. To clone a repository, you use the `git clone` command (shocking, I know). Using the SPU Developers `hello-world` repo as an example, the command looks like this:

```bash
$ git clone https://github.com/SPUDevelopers/hello-world
```

The downloaded repository contains the current state, as well as all history and branches (more on branches later).

{{% alert %}}
If you use the example repository above, you'll find that you're unable to `push` any changes as explained below. In order to practice updating the remote repository, you'll need to create your own on [GitHub](https://github.com/) ([Docs](https://help.github.com/articles/creating-a-new-repository/)) or a similar site and clone that one.
{{% /alert %}}

## Updating The Local Copy

Whether you did work from another machine or you have a teammate working on the same repository, your local copy may fall out of date. When this happens, you'll need to `fetch` the changes from the remote repository.

While there is a `git fetch` command, most people tend to use `git pull` instead, which fetches changes *and* merges them if there are any conflicts. `origin` is the name of the remote resource to pull from (and doesn't usually change), while `master` is the branch name. By default, Git will use `origin` and the current branch when updating.

```bash
# These commands will do the same thing
# when on the master branch.
$ git pull
$ git pull origin master
```

## Updating The Remote Repository

You've made changes to your local repository and want to update the copy on GitHub (or wherever your remote repository is). For this, you use the `git push` command. It's usually a good idea to make sure your local repository is fully up-to-date before pushing changes, to avoid any conflicts.

```bash
$ git pull
Already up-to-date.
$ git push
```

If you are getting conflicts **and you know it is safe to do so**, you can force the remote repository to accept your revision history using the `--force` flag. This will overwrite any difference between the remote repository and your local one, and may result in a very upset team member. Still, it's useful if you know you aren't overwriting anyone else's work and you did a `git commit --amend` *after* pushing your changes. Oops!

```bash
$ git push --force
```

# So Much More

Git has many more features than the ones we've gone over, but that is beyond this document. To learn more, check out the [online documentation](https://www.git-scm.com/doc) for Git.
