# Advance about Git

## Git Tags
Tags are pointers that refer to particular points in Git history. We can mark a particular moment in time with a tag. Tags are most often used to mark version releases in projects.<br>
There are two types of Git tags we can use:
- **lightweight tags**: They are just a name/label that points to a particular commit
- **annotated tags**: They store extra meta data including the author's name and email, the date, and a tagging message (like a commit message)

**Viewing Tags**:<br>
**git tag** will print a list of all the tags in the current repo.<br>
We can search for tags that match a particular pattern by using **git tag -l** and then passing a wildcard pattern. 
```
git tag
git tag -l "*beta*"
git show <tagname>
```
**Checking Out Tags**:<br>
To view the state of a repo at a particular tag, we can use **git checkout**. This puts us in detached HEAD.
```
git checkout <tag>
```
**Comparing Tags With Git Diff**:<br>
```
git diff v16.14.0 v17.0.0
```
**Creating Lightweight Tags**:<br>
To create a lightweight tag, use **git tag \<tagname\>**. By default, Git will create the tag referring to the commit that HEAD is referencing.
```
git tag <tagname>
```
**Creating Annotated Tags**:<br>
Use **git tag -a** to create a new annotated tag. Git will then open your default text editor and prompt you for additional information. Similar to git commit, we can also use the **-m** option to pass a message directly and forgo the opening of the text editor.
```
git tag -a <tagname>
```
**Tagging Previous Commits**:<br>
So far we've seen how to tag the commit that HEAD references. We can also tag an older commit by providing the commit hash:
```
git tag <tagname> <commit>
git tag -a <tagname> <commit>
```
**Forcing Tags**:<br>
To reuse a tag that is already referring to a commit, we can use the **-f** option to force our tag through.
```
git tag -f <tagname>
git tag <tagname> <commit> -f
```
**Deleting Tags**:<br>
To delete a tag, use:
```
git tag -d <tagname>
```
**Pushing Tags**:<br>
By default, the **git push** command doesn't transfer tags to remote servers. If you have a lot of tags that you want to push up at once, you can use the **--tags** option to the **git push** command. This will transfer all of your tags to the remote server that are not already there.
```
git push origin <tagname>
git push origin --tags
```

## Semantic Versioning
The semantic versioning outlines a standardized versioning system for software releases. It provides a consistent way for developers to give meaning to their software releases.<br>
Versions consist of **three numbers** seperated by periods, for example 2.4.1:
- **Major Release**: Signify significant changes that is no longer backwards compatible. Features may be removed or changed substantially.
- **Minor Release**: Signify that new features or functionality have been added, but the project is still backwards compatible. No breaking changes. The new functionality is optional and should not force users to rewrite their own code.
- **Patch Release**: Normally do not contain new features or significant changes. They typically signify bug fixes and other changes that do not impact how the code is used.

Typically, the first release is 1.0.0

## Config
The config file is for configuration. We've seen how to configure global settings like our name and email across all Git repos, but we can also configure things on a **per-repo** basis.
```
git config --local user.name "pig"
git config --email user.name "pig@gmail.com"
```
We can also update in the "config" file:
```
[color]
    ui = true
[color "branch"]
    local = cyan
    current = yellow bold
[color "diff"]
    old = magenta bold
```

## Refs
Inside of refs, you'll find a heads directory. **refs/heads** contains one file per branch in a repository. Each file is named after a branch and contains the hash of the commit at the tip of the branch.
```
ls .git/refs
```
For example **refs/heads/master** contains the commit hash of the last commit on the master branch.<br>
Refs also contains a **refs/tags** folder which contains one file for each tag in the repo.

## HEAD
HEAD is just a text file that keeps track of where HEAD points. If it contains refs/heads/master, this means that HEAD is pointing to the master branch.<br>
In detached HEAD, the HEAD file contains a commit hash instead of a branch reference.

## Objects
The objects directory contains all the repo files. This is where Git stores the backups of files, the commits in a repo, and more.<br>
The files are all compressed and encrypted, so they won't look like much.

