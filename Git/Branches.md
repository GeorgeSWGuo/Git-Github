# Git Branches

## Master
In git, we are always working on a branch. The default branch name is **master**.<br>
In 2020, Github renamed the default branch from **master** to **main**. The default Git branch name is still **master**.

## Head
Head is simply a **pointer** that refers to the current location in your repository. It points to a particular branch reference.

## Viewing Branches
```
git branch
```
Look for the * which indicates the branch you are currently on.

## Creating and Switching Branches
```
git branch <branch-name>
```
This just creates the branch. It does not switch you to that branch (the Head stays the same).
```
git switch <branch-name>
```
Once you have created a new branch, use **git switch xx** to switch to it.
```
git checkout <branch-name>
```
The **checkout** command is another way of switching, but it also does a million additional things.
```
git switch -c <branch-name>
```
Use **git switch** with the **-c** flag to create a new branch and switch to it all in one go.

## Switching Branches with Unstaged Changes

## Deleting Branches
```
git branch -d <branch-name>
git branch --delete <branch-name>
```
The branch must be fully merged in its upstream branch.
```
git branch --delete --force <branch-name>
git branch -D <branch-name>
```
Allow deleting the branch **irrespective of its merged status**.

## Renaming Branches
```
git branch -m <new-name>
git branch --move <new-name>
```
Before renaming, we need to **switch to that branch first**.


