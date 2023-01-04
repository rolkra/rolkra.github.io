---
layout: post
title:  Git Basics!
---

Git Basics you should know:

## Setup

* ```git status``` shows the current state of your Git working directory and staging area.
* ```git config --list``` lists the git configuration
* ```git config --global user.name "MyLastname MyFirstname"``` set config for user name
* ```git config --global user.email "myemail@adress.com"``` set config for user email

## Clone repo

* ```git clone https://myadress``` cloning a repo stored on Github/Bitbucket/...

## Set branch

* ```git checkout <branchname>``` will change to other branch

## Update repo

* ```git add myfilename``` adds a change in a file to the staging area
* ```git commit -m "this has changed"``` commit staged changes (add message)
* ```git push``` push changes to repo

## Troubleshooting

* ```git reset``` will unstage all changes
* ```git reset HEAD^``` to uncommit latest commit, keep file changes
* ```git reset --hard HEAD^``` to remove latest commit and corresponding file changes
* If ```git config --list``` shows some entries you want to delete: use ```git config --unset-all <name>```
