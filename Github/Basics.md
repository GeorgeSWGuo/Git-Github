# Basics about Github

## Cloning
Very often we want to get a local copy of an existing repository. To do this, we can clone a remote repository hosted on Github or similar website.<br>
All we need is a **URL** that we can tell Git to clone for use.
```
git clone <url>
```
It is not tied specifically to Github. We can use it to clone repositories that are hosted anywhere.

## Configuring SSH Keys
We need to be authenticated on Github to do certain operations, like pushing up code from our local machine.<br>
Generate and configure on SSH key! Once configured, we can connect to Github without having to supply our username/password.<br>
Follow: https://docs.github.com/en/authentication/connecting-to-github-with-ssh

## How to Get Code on Github
### Existing Repo
If we already have an existing repo locally that we want to get on Github.
- Create a new repo on Github
- Connect our local repo (add a remote)
- Push up our changes to Github
### Start from Scratch
If we haven't begun work on our local repo.
- Create a brand new repo on Github
- Clone it down to our machine
- Do some work locally
- Push up our changes to Github

## Remote
Before we can push anything up to Github, we need to tell Git about remote repository on Github.<br>
In Git, we refer to these "destinations" as **remotes**. Each remote is simply a URL where a hosted repository lives.<br>
To view any existing remotes for our repositories:
```
git remote
git remote -v
```
To add a new remote:
```
git remote add <name> <url>
git remote add origin https://github.com/xxxxx
```
**Origin** is a conventional Git remote name. It's just a name for a URL.<br>
When we clone a Github repo, the default remote name setup for us is called origin.<br>
Other commands:
```
git remote rename <old> <new>
get remote remove <name>
```

## Pushing
We need to specify the remote we want to push up to and the specific local branch we want to push up to that remote.
```
git push <remote> <branch>
```
For example **git push origin master** tells git to push up the master branch to our origin remote.
```
git push origin master
```
While we often want to push a local branch up to a remote branch of the same name, we don't have to!<br>
To push our local apple branch up to a remote branch called banana we could do:
```
git push origin apple:banana
git push <remote> <local-branch>:<remote-branch>
```
The **-u** option allows us to set the upstream of the branch we're pushing. You can think of this as a link connecting our local branch to a branch on Github.
```
git push -u origin master
git push --set-upstream origin master
```
Once we've set the upstream for a branch, we can use the **git push** shorthand which will push our current branch to the upstream.

## Remote Tracking Branch
It is a reference to the state of the master branch on the remote. I can't move this myself. It's like a bookmark pointing to the last known commit on the master branch on origin.<br>
<br>
Once you've cloned a repository, we have all the data and Git history for the project at that moment in time. However, that does not mean it's all in your workspace.<br>
Suppose he github repo has a branch called **pigs**, but when we run **git branch** we don't see it on our machine! All we see is the master branch.<br>
```
git branch
:*master
```
Run **git branch -r** to view the remote branches our local repository knows about.
```
git branch -r
:origin/master
:origin/pigs
```
By default, my master branch is already tracking origin/master. What if I want my own local branch called **pigs**, and I want it to be connected to **origin/pigs**. just like my local **master** branch is connected to **origin/master**.<br>
Run **git switch remote-branch-name** to create a new local branch from the remote branch of the same name. It will make me a local pigs branch and sets it up to **track the remote branch origin/pigs**.
```
git switch <remote-branch-name>
git switch pigs
```
Use **git checkout** is slightly more complicated.
```
git checkout --track origin/pigs
```

## Git Fetch
Fetching allows us to download changes from a remote repo, but those changes will not be automatically integrated into our working files. It lets you see what others have been working on, without having to merge those changes into your local repo.


