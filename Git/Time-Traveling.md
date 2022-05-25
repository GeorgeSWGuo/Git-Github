# Time Travelling

## Detached HEAD
We can use **git checkout commit-hash** to view a previous commit.
```
git checkout <commit-hash>
```
Then we will be in **'detached HEAD'** state.
- Usually, HEAD points to a specific **branch** reference rather than a particular commit.
- When we checkout a particular commit, HEAD points at that **commit** rather than at the branch pointer.

We have a couple options:<br>
<br>
(1) Stay in detached HEAD to examine the contents of the old commit.<br>
(2) Leave and go back to wherever you were before (reattach the HEAD):
```
git switch master
```
(3) Create a new branch and switch to it. You can now make and save changes, since HEAD is no longer detached.
```
git switch -c newbranch
```

Syntax for referencing **previous commits** relative to a particular commit:<br>
<br>
**HEAD~1** refers to the commit before HEAD (parent)<br>
**HEAD~2** refers to 2 commits before HEAD (grandparent)
```
git checkout HEAD~1
git checkout HEAD~2
git checkout HEAD~8
```
**git switch -** will take you to the last branch you were on
```
git switch -
```

## Discarding Changes
Suppose we have made some changes to a file but don't want to keep them. To revert the file back to whatever it looked like when you **last committed**, use:
```
git checkout HEAD <filename>
git checkout -- <file1> <file2>
```

## Restore
**git restore** is a brand new Git command that helps with undoing operations. It was introduced alongside **git switch** as alternatives to some of the uses for **checkout**.<br>
To restore the file to the contents in the HEAD, use **git restore filename**, and note that this command is not "undoable" if you have uncommitted changes in the file, they will be lost!
```
git restore <filename>
```
**git restore filename** restores using HEAD as the default source, but we can change that using the **--source** option.
```
git restore --source HEAD~1 app.js
```
We will restore the contents of app.js to its state from the commit prior to HEAD.

## Unstaging
If you have accidently added a file to your staging area with **git add** and you don't wish to include it in the next commit, you can use **git restore** with **--staged** option to remove it from staging.
```
git restore --staged <filename>
```
**Note the difference**:
- For changes to be commited, use **git restore --staged file** to unstage
- For changes not staged for commit, use **git restore file** to discard changes in working directory

## Git Reset
You can use **git reset** to reset the repo back to a specific commit. The commits are gone.
```
git reset <commit-hash>
```
If you want to undo both the commits **and the actual changes** in your files, you can use the **--hard** option. For example, **git reset --hard HEAD~1** will delete the last commit and associated changes.
```
git reset --hard <commit>
```

## Git Revert
**git reset** actually moves the branch pointer backwards, eliminating commits.<br>
**git revert** instead creates a brand new commit which reverses the changes from a commit. Because it results in a new commit, you will be prompted to enter a commit message<br>
<br>
There is a significant difference when it comes to **collaboration**.<br>
- If you want to reverse some commits that other people already have on their machines, you should use revert.
- If you want to reverse commits that you haven't shared with others, use reset and no one will ever know.



