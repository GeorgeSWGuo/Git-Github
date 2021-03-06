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

## Config File
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

## Refs Directory
Inside of refs, you'll find a heads directory. **refs/heads** contains one file per branch in a repository. Each file is named after a branch and contains the hash of the commit at the tip of the branch.
```
ls .git/refs
```
For example **refs/heads/master** contains the commit hash of the last commit on the master branch.<br>
Refs also contains a **refs/tags** folder which contains one file for each tag in the repo.

## HEAD File
HEAD is just a text file that keeps track of where HEAD points. If it contains refs/heads/master, this means that HEAD is pointing to the master branch.<br>
In detached HEAD, the HEAD file contains a commit hash instead of a branch reference.

## Objects Directory
The objects directory contains all the repo files. This is where Git stores the backups of files, the commits in a repo, and more.<br>
The files are all compressed and encrypted, so they won't look like much.

## SHA-1
Git uses a hashing function called SHA-1 (this is set to change eventually).<br>
SHA-1 always generates 40-digit hexadecimal numbers.<br>
The commit hashes we've seen a million times are the output of SHA-1.

## Git Database
Git is a **key-value data store**. We can insert any kind of content into a Git repository, and Git will hand us back a unique key we can later use to retrieve that content. These keys that we get back are SHA-1 checksums.<br>
<br>
The **git hash-object** command takes some data, stores in our .git/objects directory and gives us back the unique SHA-1 hash that refers to that data object.<br>
In the simplest form, Git simply takes some content and returns the unique key that would be used to store our object. But it does not actually store anything.
```
git hash-object <file>
git hash-object pigs.txt
echo 'hello' | git hash-object --stdin
```
Rather than simply outputting the key that git would store our object under, we can use the **-w** option to tell git to actually write the object to the database.
```
git hash-object pigs.txt -w
echo 'hello' | git hash-object --stdin -w
```
Now that we have data stored in our Git object database, we can try retrieving it using the **git cat-file** command.<br>
The **-t** option tells Git to return the type of the object. The **-p** option tells Git to print the contents of the object based on its type.
```
git cat-file -t <object-hash>
git cat-file -p <object-hash>
```

## Git Objects
**Blobs:** <br>
Git blobs (binary large object) are the object type Git uses to store the **contents of files** in a given repository. Blobs don't even include the filenames of each file or any other data. They just store the contents of a file!<br>
<br>
**Trees:** <br>
Trees are Git objects used to store the contents of a directory. Each tree contains pointers that can refer to blobs and to other trees. Each entry in a tree contains the SHA-1 hash of a blob or tree, as well as the mode, type, and filename.<br>
To **view trees**:
```
git cat-file -p master^{tree}
```
Remember that **git cat-file** prints out Git objects. In this example, the **master^{tree}** syntax specifies the tree object that is pointed to by the tip of our master branch.<br>
<br>
**Commits:** <br>
Commits objects combine a tree object along with information about the context that led to the current tree. Commits store a reference to parent commit(s), the author, the commiter, and of course the commit message.

## Reflogs
Git keeps a record of when the tips of branches and other references were updated in the repo. We can view and update these reference logs using the **git reflog** command.<br>
The git reflog command accepts subcommands **show, expire, delete**, and **exists**. **Show** is the only command used variant, and it is the default subcommand. **git reflog show** will show the log of a specific reference (it defaults to HEAD).
```
git reflog show HEAD
git reflog show main
```
**Limitation**:<br>
- Git only keeps reflogs on your **local** activity. They are not shared with collaborators.
- Reflogs also expire. Git cleans out old entries after around 90 days, though this can be configured.

## Reflog References
We can access specific git refs using **name@{qualifier}**. We can use this syntax to access specific ref pointers and can pass them to other commands including checkout, reset, merge.<br>
Every entry in the reference logs has a **timestamp** associated with it. We can filter reflogs entries by time/date by using time qualifiers like:
```
git reflog master@{one.week.ago}
git checkout bugfix@{2.days.ago}
git diff main@{0} main@{yesterday}
```

## Reflogs Rescue
We can sometimes use reflog entries to access commits that seem lost and are not appearing in git log.<br>
**Undo a reset**:
```
git reset --hard <commit>
git reflog show master
git reset --hard master@{1}
```
**Undo a rebase**:
```
git reset --hard <commit>
```
The commit could be a commit that has been rebased.

## Global Git Config
Git looks for the global config file at either **~/.gitconfig** or **~/.config/git/config**. Any configuration variables that we change in the file will be applied across all Git repos.<br>
We can also alter configuration variables from the command line if preferred.

## Aliases
We can easily set up Git aliases to make our Git experience a bit simpler and faster.
```
[alias]
    s = status
    l = log
```
We can also set aliases from the command line.
```
git config --global alias.s status
git config --global alias.l log
```
Aliases with arguments:
```
[alias]
    cm = commit -m   
```
Must have git aliases:<br>
https://www.durdn.com/blog/2012/11/22/must-have-git-aliases-advanced-examples/
