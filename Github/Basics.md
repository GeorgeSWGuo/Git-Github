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
