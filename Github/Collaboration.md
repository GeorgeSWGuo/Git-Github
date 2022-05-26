# Github Collaboration

## Public Vs. Private Repos
Public repos are accessible to everyone on the internet. Anyone can see the repo on Github.<br>
Private repos are only accessible to the owner and people who have been granted access.<br>
> **To change**: Settings -> Danger Zone

## Adding Collaborators
Settings -> Manage access

## README File
READMEs are Markdown files, ending with the .md extension.
It is used to communicate important information about a repo including:
+ What the project does
+ How to run the project
+ Why it's noteworthy
+ Who maintains the project

## Markdown
Markdown is a convenient syntax to generate formatted text.

## Github Gists
Github Gists are a simple way to share code snippets and useful fragments with others. Gists are much easier to create, but offer far fewer features than a typical Github repository.

## Github Pages
Github Pages are public webpages that are hosted and published via Github. They allow you to create a website simply by pushing your code to Github.<br>
Github Pages is a hosting service for **static** webpages, so it does not support server-side code like Python, Ruby, or Node. Just HTML/CSS/JS!
- User Site: You get one user site per Github account, following this pattern: **username.github.io**
- Project Sites: You get unlimited project sites, following this pattern: **username.github.io/repo-name**

## Centralized Workflow
The simplest collaborative workflow is to have everyone work on the master branch. While it's nice and easy to only work on the master branch, this leads to some serious issues:
- Lots of time spent resolving conflicts and merging code.
- No one can work on anything without disturbing the main codebase.
- The only way to collaborate on a feature together with another teammate is to push incomplete code to master.

## Feature Branches
Rather than working directly on master, all new development should be done on separate branches!
- Treat master branch as the official project history
- Multiple teammates can collaborate on a single feature and share code back and forth without polluting the master branch
- Master branch won't contain broken code.

## Pull Requests
> Right option for **Merging in feature branches**

They allow developers to alert team-members to new work that needs to be reviewed. They provide a mechanism to approve or reject the work on a given branch. They also help facilitate discussion and feedback on the specified commits.<br>
<br>
The **work flow**:
1. Do some work locally on a feature branch
2. Push up the feature branch to Github
3. Open a pull request using the feature branch just pushed up to Github
4. Wait for the PR to be approved and merged. Start a discussion on the PR. This part depends on the team structure.

Just like any other merge, **sometimes there are conflicts** that need to be resolved when merging a pull request. You can perform the merge and fix the conflicts on the command line like normal, or you can use Github's interactive editor. <br>
**Github gives you instructions** if you forget what to do!

## Configuring Branch Protection Rules
> Settings -> Branches -> Branch protection rules

## Forking
Github allow us to create personal copies of other peoples' repos. We call those copies a "fork" of the original. As with pull requests, forking is not a Git feature. The ability to fork is implemented by Github.<br>

## Fork & Clone Workflow
Instead of just one centralized Github repo, every developer has their own Github repository in addition to the "main" repo. Developers make changes and push to their own forks before making pull requests.<br>
<br>
**The workflow** should be:
1. I fork the original project repo on Github.
2. I clone my fork to my local machine.
3. I add a remote pointing to the original project repo. This remote is often named upstream.
4. I make changes and add/commit on a feature branch on my local machine.
5. I push up my new feature branch to my forked repo, usually called origin.
6. I open a pull request to the original project repo containing the new work on my forked repo.
7. Hopefully the pull request is accepted and my changes are merged in.

**A briefer summary**:
1. Fork the project
2. Clone the fork
3. Add upstream remote
4. Do some work
5. Push to origin
6. Open PR

