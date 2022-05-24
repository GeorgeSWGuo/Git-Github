# Introduction to Git & Github

## Birth of Git
**Linus Torvalds** is the creator and main developer behind Linux and Git.<br>
Birth year of Git: 2005

## Difference between Git and Github
**Git** is the version control software that runs locally on our machine. We don't need to register for an account. We don't need the internet to use it.<br>
**Github** is a service that hosts Git repositories in the cloud and makes it easier to collaborate with other people. We need to sign up for an account to use Github.

## Git Installation
check to see if we have Git installed already<br>
```
git --version
```

## Configuring Git
Though we do not need to register for an account or anything, we do need to provide:
- name
- email
```
git config --global user.name "name"
git config --global user.email "email"
```
git check configuration settings:
```
git config --list
```

## Repository
A Git **Repo** is a workspace which tracks and manages files within a folder. Anytime we want to use Git we need to creat a new git repository.

