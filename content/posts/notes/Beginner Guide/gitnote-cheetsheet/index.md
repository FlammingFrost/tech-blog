---
title: Git Command Guide
seo_title: Git Command Guide
summary: Some common and useful git commands.
description:
slug: bg/gitnote
author: FlammingFrost
math: false # set to true to enable KaTeX rendering

draft: false # set to false to publish
date: 2023-07-28
lastmod: 2023-09-06 # both date and lastmod will show in the post's footer

feature_image:
feature_image_alt:

categories:
  - Cheet sheet
tags:
  - git
series: 
  - Beginner's Guide
toc: true # set to true to enable a Table of Contents
related: true # set to true to enable Related Posts section
social_share: true # set to true to enable Social Sharing buttons
newsletter: false # set to true to enable Newsletter section, at the bottom of the page
disable_comments: false # set to true to disable comments for a specific post
---

> Some commonly used git commands. 

## Initialize Git Local Repository

### From local folder

`$ git init`

### From online repository

`$ git clone url`

## General git update routine

Suppose you have edited some file in repository, and ready for commitment. To update file in stage,

- `$ git add .` To add all file changes. (Including add, delete and change)
- `$ git add filename` To specific a file updata to stage.

After file changes have been recoreded in stage, you can check these changes via

- `git status` Provides a list of change file. This command will also list change in this folder that have NOT been add to stage.
- `git diff filename` Provides a detailed change of a specific file.

To commit these changes to local repository, use

`git commit -m "commit message"` Commit changes to local repository. The `-m` flag is used to add a commit message.

There are some other useful flags for `git commit` command.

- `-a` Commit all changes, but not including new files.
- `-v` Show the difference between the last commit and the current commit.

## Git log (Version Control)

To reset to a previous version, you need to know the version code of that version. To check all version code, use

`git log` Show all commit history.

`git log --pretty=oneline` Show all commit history in one line.

`git log --graph` Show all commit history in graph.

`git log --pretty=oneline --graph --decorate --all` Show all commit history in graph with branch name.

## Git reset (Version Control)

### Reset to a previous version

- `git reset --hard HEAD^` Reset to the previous version. `HEAD` means the current version, `HEAD^` means the previous version, `HEAD^^` means the previous two versions, and so on.
- `git reset --hard HEAD~n` Reset to the previous n version.
- `git reset --hard commit_id` Reset to a specific version. `commit_id` is the version code of the version you want to reset to.

> To check all version code, use `git reflog`.

### Reverse changes before commit

- In files manually.

- Commit then reset (not elegant).

- Delete changes in workspace.

  1. `git status` To check the difference.
  2. `git checkout -- filename` Reverse all change in current workspace.

  > `git checkout -- .` Reverse all change in current workspace. If there is a previous version in stage, this command will reverse to that version. If not, this command will reverse to the latest version in the local repository.

## Git branch

Generally, before you start a new feature, you should create a new branch. After the feature is completed, merge the branch into the main branch.

The temporary branch is only used to develop a new feature. After the feature is completed, it will be merged into the main branch, and then the temporary branch will be deleted. The branch is ususally named "dev".

### Create a new branch

`git branch branch_name` Create a new branch.

`git checkout branch_name` Switch to a new branch.

`git checkout -b branch_name` Create a new branch and switch to it.

`git branch -m old_branch_name new_branch_name` Rename a branch.

### Merge branch

`git merge branch_name` Merge a branch into the current branch.

If there is a conflict, you need to manually modify the conflict file, and then add it to the stage, and then commit it.

### Delete branch

`git branch -d branch_name` Delete a branch.

### Check branch

`git branch` Check all branch.

`git branch -v` Check all branch with last commit message.

`git branch -a` Check all branch, including remote branch.

## Git remote

### Add remote repository

`git remote add origin url` Add a remote repository.

### Push local repository to remote repository

`git push origin branch_name` Push local repository to remote repository.

`git push -u origin main` Push local repository to remote repository. `-u` flag is used to set the default push branch.

`git push -f origin main` Push local repository to remote repository. `-f` flag is used to force push. This command will overwrite the remote repository.

### Clone remote repository

`git clone url` Clone a remote repository.

### Check remote repository

`git remote -v` Check all remote repository.

## Manage submodules

In some project, you could include other project as submodule. On github, you can see the submodule as a link to another repository. 
- A git repository should not be included in another git repository. I can only be included as a submodule.
- If you want to edited files in submodule, you cancel the link and clone the submodule as a local repository.
- When pushed to remote repository, the submodule will be pushed as a link, instead of the whole repository.

### Add submodule

`git submodule add url` Add a submodule.

`git submodule add url path` Add a submodule to a specific path.

### Update submodule

`git submodule update --init --recursive` Update submodule.

## Git stash

When you want to switch to another branch, but there are some uncommitted changes in the current branch, you can use `git stash` to save the current workspace, and then switch to another branch. After switching to another branch, you can use `git stash pop` to restore the workspace.

`git stash` Save the current workspace.

`git stash list` Check all stash.

`git stash apply` Restore the last stash.

`git stash apply stash@{n}` Restore the n-th stash.

`git stash drop` Delete the last stash.

`git stash drop stash@{n}` Delete the n-th stash.

`git stash pop` Restore the last stash and delete it.

`git stash pop stash@{n}` Restore the n-th stash and delete it.

`git stash clear` Delete all stash.