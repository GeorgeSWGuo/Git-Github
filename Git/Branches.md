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
git checkout -b <branch-name>
```
Use **git switch** with the **-c** flag to create a new branch and switch to it all in one go. Similarly using **checkout -b**.

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

## Merging
Very often we want to incorporate changes from one branch into another.<br>
<br>
**Note that:**
- We merge branches, not specific commits
- We always merge to the current Head branch

To merge, we need to <br>
1. Switch to the branch we want to merge the changes into
2. Use the **git merge** command to merge changes from a specific branch into the current branch
```
git switch master
git merge branch1
```
**Fast Forward**<br>
Simply caught up<br>
<br>
**Not Fast Forward**<br>
Rather than performing a simple fast forward, Git performs a "merge commit" .<br>
We end up with **a new commit** on the master branch.
- No Conflict
- Conflict

## Conflicts
Depending on the specific changes you are trying to merge, Git may not be able to automatically merge.<br>
This results in **merge conflicts**, which you need to manually resolve.<br>
<br>
The content from your current Head (the branch you are trying to merge content into) is displayed: <br>
between the <<<<<<< HEAD and ======= <br>
The content from the branch you are trying to merge from is displayed: <br>
between the ======= and >>>>>>> symbols <br>
<br>
**Resolving Conflicts**
1. Open up the files with merge conflicts.
2. Edit the files to remove the conflicts.
3. Remove the conflict "markers" in the document.
4. Add your changes and then make a commit.

## Diffs
We can use the **git diff** command to view changes between commits, branches, files, our working directory, et al.
```
git diff
git diff HEAD
git diff -- staged
git diff --cached
```
Without additional options, **git diff** lists all the changes in our working directory that are not staged for the next commit.<br>
**git diff HEAD** lists all changes in the working tree since your last commit, including **both staged and unstaged**.<br>
**git diff --staged** or **git diff --cached** will list the changes between the staging area and our last commit.<br>
```
git diff HEAD <filename>
git diff --staged <filename>
```
We can view the changes within a specific file by providing git diff with a filename.<br>
```
git diff <branch1>..<branch2>
git diff <commit1hashes>..<commit2hashes>
```
Compare two branches and compare two commits.<br>
<br>
**Compared Files:**<br>
For each comparison, Git explains which files it is comparing. Usually this is two versions of the same file. Git also declares one file as "A" and the other as "B". File A gets a **minus** sign (-). File B gets a **plus** sign (+).<br>
A diff won't show the entire contents of a file, but instead only shows portion or "chunks" that were modified. A **chunk** also includes some unchanged lines before and after a change to provide some context.<br>

## Stashing
Consider a situation:<br>
You do some new work, but don't make any commits. What happens when I switch back to master?<br>
1. Your changes come with you to the destination branch
2. Git won't let you switch if it detects potential conflicts

**git stash** could help you save changes that you are not yet ready to commit. You can stash changes and then come back to them later.<br>
Running git stash will take all uncommitted changes (staged and unstaged) and stash them, reverting the changes in your working copy.
```
git stash
```
If you have untracked files (files that you have never checked in to Git), they will not be included in the stash. Fortunately, you can use the **-u** option to tell git stash to include those untracked files.
```
git stash -u
```
Use **git stash pop** to remove the most recently stashed changes in your stash and re-apply them to your working copy.
```
git stash pop
```
Use **git stash apply** to apply whatever is stashed away, without removing it from the stash. This can be useful if you want to apply stashed changes to multiple branches.
```
git stash apply
```
**stashing multiple times**<br>
You can add multiple stashes onto the stack of stashes. They will all be stashed in the order you added them.<br>
Run **git stash list** to view all stashes.
```
git stash list
```
**applying specific stashes**<br>
Git assumes you want to apply the most recent stash when you run **git stash apply**, but you can also specify a particular stash like:
```
git stash apply stash@{2}
```
**dropping stashes**<br>
To delete a particular stash, you can use:
```
git stash drop stash@{2}
```
To clear our all stashes, run:
```
git stash clear
```

