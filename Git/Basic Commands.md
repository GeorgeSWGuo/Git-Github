# Basic Commands about Git

## Status
**git status** gives information on the current status of a git repository and its contents.
```
git status
```
Use **git status** constantly to verify what changes are staged and not staged.

## Initialization
Use **git init** to create a new git repository. We should initialize the repo in the top-level folder containing our project.
```
git init
```
**Note:** Do not init a repo inside of a repo!!

## .git
To **delete a repo**, locate the associated .git directory and delete it.<br>
In the top level folder, do:
```
ls -a
rm -rf .git
```

## Adding
We use the **git add** commands to stage changes to be committed.<br>
Use git add to add specific files to the staging area. Seperate files with spaces to add multiple at once.
```
get add file1 file2
```
Use **git add .** to stage all changes at once.
```
git add .
```

## Committing
Making a commit is similar to making a save in a file. When saving a file, we are saving the state of a single file. 
With Git, we can save the state of multiple files and folders together.<br>
We use the **git commit** command to actually commit changes from the staging area.<br>
```
git commit
```
When making a commit, we need to provide **a commit message** that summarizes the changes and work snapshotted in the commit.<br>
Running **git commit** will open up a text editor and prompt you for a commit message.<br>
```
git commit -m "my message"
```
The **-m** flag allows us pass in an inline commit message, rather than launching a text editor.

## Configuring Git's Default Editor
Open up a text editor only when we need to write a long message.<br>
For example, use VScode:
```
git config --global core.editor "code --wait"
```
**Note:** We might need to install "code" command in path in VScode.

## Atomic Commits
Try to keep each commit focused on a single thing.<br>
This makes it easier to undo or roolback changes later on. It also makes your code or project easier to review.

## Amending Commits
Suppose we made a typo in the commit message that we want to correct. Or we realized that we forgot to include a file in the last commit.<br>
Rather than making a brand new separate commit, we can "redo" the previous commit using the **--amend** option.
```
git commit --amend
```

## Log
```
git log
```
```
git log --pretty=oneline
```
```
git log --pretty=oneline --abbrev-commit
git log --oneline
```

## Ignoring Files
We can tell Git which files and directories to ignore in a given directory, using a **.gitignore** file.
This is useful for files that we never want to commit.<br>
Create a file called **.gitignore** in the root of a repository. Inside the file, we can write patterns to tell Git which files & folders to ignore, for example:
- folderName/
- fileName
- .DS_Store
- *.log

## Git GUI
**GitKraken**
