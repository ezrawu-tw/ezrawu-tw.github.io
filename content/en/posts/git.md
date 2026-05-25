---
slug: git
title: git
date: 2025-10-28 12:25:03
tags:
- git
- version_control
categories:
  - Note
---
slug: git

# git 

Introduction to Git - Brief History, Reasons for Use, and What is Version Control?
==
* History: Released under the GPL license in 2005, created by Linus Torvalds.
* Reason for use: When collaborating as a team, using git commands enables real-time updates without the hassle of the traditional method of uploading to the cloud and then downloading again.
* Version control: Software that helps track code changes over a period of time.

Explanation of Version Control Logic
==
![](https://i.imgur.com/Sokaxmb.png)

![](https://i.imgur.com/dRboRYj.png)



1. Configure your Git
```
Since every commit records the author's information, you must first set your Name and E-mail.
git config --global user.name "xxxxxxx"
git config --global user.email "xxxx@xxxx"
After configuration, you can check the settings:
git config --list
```
2. Create a new Repository
```
git init
```
1. Clone someone else's Repository from GitHub
* GitHub provides two path options: https and ssh. The official recommendation is https; the difference is that ssh requires setting up a key pair first.
```
git clone (url https://github.com/monosparta/eason-git-practice.git)
```
1. Add modified files to version control
```
git add file.txt  // add file.txt
git add .         // add all files
```
1. Commit modified files
```
Remember you must first run $ git add to add the modified files to version control before committing.
git commit               
git commit -m "modified content of file.txt"  
// you can include the commit message at the same time
```

1. View past commit history

```
git log
git log --stat // --stat shows detailed content
git log -p     // -p shows more detailed file change content
```
7. Create a branch
```
git branch <branch-name>
```

8. Switch branch
```
git checkout <branch-name>
```
9. Merge branch
```
git merge <branch-name>
```
10. Pull remote updates to local
```
git pull
```
11. Check current Git status
```
git status
```
12. Revert to previous commit and cancel current commit
```
git reset HEAD^ --hard
```

Common Git Commands Overview
==
Workflow steps:
1. git clone - Clone the collaborative project you're working on
>Copy someone's homework
2. git pull - Sync with the remote project
>Like a shared Google Doc, this ensures your notes are in sync rather than everyone working on their own isolated version
3. git status - Check the current state of changes in the local project
>Git is like your butler - always ask it and you won't go wrong; this is an extremely useful feature, check it anytime
4. git add <filename>
>Announce to the world what you've done!
5. git branch - Check which branch you're currently on
>Before submitting your assignment, you should know which teacher it's for, right?
6. git branch <branch-name>
>Create a new branch. Just like having a school folder, and inside the school folder there are folders for different subjects - how meticulous!
7. git checkout <branch-name>
>Switch to the branch you want to push to. Before making a commit, you must switch first, otherwise you'll be a homeless child
8. git commit -m "comment"
>Maybe you remember what you had for breakfast yesterday, but you definitely won't remember what you had for breakfast two years ago today. Add a comment so you can look back at what (silly) features you implemented
9. git push --set-upstream origin <branch-name>
 >Assignment submitted successfully! Congratulations on breaking through the git muggle training!

.gitignore Configuration
==
* All blank lines or lines starting with # will be ignored by Git.
* You can use standard glob patterns for matching.
* Patterns can start with (/) to prevent recursion.
* Patterns can end with (/) to specify a directory.
* To ignore all files except those matching a specified pattern, prefix the pattern with an exclamation mark (!).
  
How to Use Branches
==

1. List branches
   Basic command to list branches:
```
git branch
```
* Without parameters, git branch lists your local branches.

```
git branch
* master
```


2. Delete a branch
Command to delete a branch:

git branch -d (branchname)
For example, to delete the testing branch:
```
git branch
* master
  testing
git branch -d testing
Deleted branch testing (was 85fc7e7).
git branch
* master
```

3. Merge branches
Once a branch has independent content, you will eventually want to merge it back into your main branch. You can use the following command to merge any branch into the current branch:
```
git merge
```

Introduction and Usage of Commit
==

##### git commit: Commit the contents of the staging area to the Repository for preservation
git commit -m "change log"
```
git commit -m"init commit" # Describe what this commit does
```
The git commit command is often paired with -m"change log", where the quoted text is the comment telling us what this Git update or addition was to the local copy.

Note: Comments can be in Chinese or English, but the most important thing is that they are **"clear"**. The purpose is for yourself or other collaborators to understand what was done this time, so a simple text description is sufficient.

💡 When using the git commit command, always add the -m"change log" message.

If the -m parameter description is not entered, Git's default behavior will not allow you to execute the Commit action. The purpose of this action is to tell yourself and others "what was changed in this modification."

GitHub Usage: push and pull Walkthrough
==
![](https://i.imgur.com/v4RAFuJ.png)

## push
Steps to add to local repository:

1. Create a new local repository (Local Repository only needs to be created once)
```
git init
```
2. Move files into the index
```
git add .
```
3. Commit files in the index to the local repository
```
git commit -m "message"
```
4. Steps to add to the remote repository (GitHub):
First create a GitHub Repository yourself, open the terminal, and type the following command in that directory:
```
This line only needs to be entered once
git remote add origin <your url>
```

5. Branch
```   
git branch -M main
git push -u origin main
```

![](https://i.imgur.com/HNm5gcC.png)
![](https://i.imgur.com/yiAQOJ7.png)
## pull
* The pull command pulls updates back to local

fork = git clone to local
* First clone the files then use pull to sync and update

![](https://i.imgur.com/f1VB1yX.png)


GitFlow Introduction
==
Gitflow is a convention, a recommended implementation method. This also means teams can adjust it according to their needs. Since it is a convention, there are several key points, introduced one by one here:

Gitflow's concept is composed of five branches: master, developer, hotfixes, release, and feature.
In Gitflow, master and developer are permanent branches that will not be deleted.
In Gitflow, hotfixes, release, and feature are temporary branches that will be merged back into permanent branches after completing specific tasks.
These five branches each handle the following responsibilities:

Developer:
The Dev branch is the core of development. In practice it works similarly to master - developers do not actively develop on the Dev branch directly; instead, a Feature branch is created from Dev to complete requirements, and only after the Feature branch is complete does it merge back into Dev.

The Dev branch usually has a Webhook attached to it that triggers automated compilation, testing, packaging, and deployment - typically deploying to a SIT environment for the team to validate directly.

Feature:
Feature branches are created from Dev and used to complete specific feature development. When complete, they are merged back into Dev. Generally, each Feature's lifecycle aligns with a Sprint cycle. The Product Owner defines the Sprint goals, and the Features opened for that sprint are the functionalities needed to achieve those goals.

When a Feature cannot be completed within the Sprint deadline, the Product Owner should investigate whether the team needs assistance, or review whether the Feature contains too many functions. When the team reaches a certain scale, multiple Features can be opened in parallel within the same Sprint to complete multiple functions concurrently.

Features typically correspond to individual developers' computers - code is tested locally and then pushed.

Release:
Release is a branch opened from Developer when the Developer branch has reached a state that can fulfill a series of requirements, used for further testing. In some cases, Release also corresponds to a temporary environment, such as a simulated load testing environment.

When Release testing is complete, it is merged into the master branch; if Release testing discovers some issues and fixes them on the branch, in addition to merging into master, it is also merged into developer.

Master:
Master holds the most stable version of the code and is deployable at any time (when an unfortunate problem occurs, you can immediately roll back to the previous master version to stop the bleeding). For this reason, code must complete verification in other branches before being merged into master - developers will never directly modify and commit on master (as this may skip validation and cause issues to compound).

Typically, we attach Webhooks to permanent branches so that when the branch's code is updated, certain events are triggered. When master is updated, it can be configured to automatically deploy the new version to the production environment. This does not necessarily involve compilation and packaging; instead it pulls the image and corresponding deployment configuration files and environment configuration files for deployment.

hotfixes:
When master (i.e., the live product) has a bug, master rolls back to the previous version to stop the bleeding. However, we obviously cannot add this bug fix to the next sprint's Feature and merge it all the way back into master. Facing this situation, a hotfixes branch is opened to fix the bug, and after the fix is complete it is merged back into both master and Developer, so that both permanent branches are fixed simultaneously.
