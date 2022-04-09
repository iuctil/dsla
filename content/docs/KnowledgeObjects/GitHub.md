---
title: "GitHub"
description: "a hosting site where developers and programmers can upload code and work collaboratively"
lead: "GitHub is a hosting site where developers and programmers can upload the code they create and work collaboratively to improve it"
keywords: 
    - code hosting
    - developers
    - programmers
    - collaborative
contributors:
    - Xiaolei Lu
    - Clayton Winders
    - Andra Ferrara
    - Andrew Cruez
date: 2020-11-09T00:00:00+00:00
lastmod: 2022-03-30T00:00:00+00:00
draft: false
toc: true
plotly: false
images: []
weight: 100
menu:
    docs:
        parent: "KnowledgeObjects"
---

# GitHub

## What Is GitHub?
GitHub is a hosting site where developers and programmers can upload the code they create and work collaboratively to improve it. A defining feature of GitHub is its robust version control system. The version control lets coders tweak software, potentially fixing bugs or improving efficiency, without affecting the software itself or risking the experience of any current users. Proposed changes can be easily merged into the live software after the proposals are reviewed and approved.

## Who Should Use GitHub?
GitHub functions as a sort of social media site for developers and programmers. It allows your work to get out in front of the public. It is one of the largest coding communities around, so using it can provide wide exposure for your project. The more people you have to review your project, the more attention and use it is likely to attract. Showcase your work: Are you a developer and wishes to attract recruiters? GitHub is the best tool you can rely on for this. Today, when searching for new recruits for their project, most companies look into the GitHub profiles. If your profile is available, you will have a higher chance of being recruited even if you are not from a great university or college.

## When Should I Use GitHub?
GitHub can integrate with common platforms and services such as Amazon, Google Cloud, and Code Climate. It can highlight syntax in more than 200 different programming languages. Thus, users can share themselves work flexibly. When you post your project on GitHub, the wider community of programmers and hobbyists can download and evaluate your work. They can alert you to possible issues. They may even propose solutions to those problems, saving you the work.

## How Do I Learn About It?
- https://guides.github.com/
- https://lab.github.com/
- https://www.geeksforgeeks.org/list-useful-github-commands/
- https://www.youtube.com/watch?v=RGOj5yH7evk

## Strengths
- The projects on GitHub are a form of open-source code. GitHub provides a community where programmers are constantly working to solve current problems and making solutions available to the public
- GitHub is a repository, what this means that it allows your work to get out there in front of the public. Moreover, GitHub is one of the largest coding communities around right now, so it's wide exposure for your project
- GitHub can integrate with common platforms such as Amazon and Google Cloud, services such as Code Climate to track your feedback, and can highlight syntax in over 200 different programming languages

## Alternatives
- Bitbucket
- Gitlab
- Codecommit

## Common Uses and Commands.
Create a Repository on GitHub
- Click the "New" button and give your repository a name, and optional description.
- This creates a repository in GitHub. From here, you can add files to the repository on GitHub, or download the repository to work on locally and push your changes up to GitHub.

Clone a Repository to Local Machine.
- First ensure Git is installed on your machine. 
- On GitHub, while viewing the Repository you wish to clone, click the green "Clone or Download" button and copy the SSH key.
- 'git clone' - Use this command and paste the SSH key copied from GitHub in your IDE terminal.

Identify Changes and Files to Track
- 'git status' - Shows all files in the repository that have been updated/created/deleted but not yet saved in a commit.
- 'git add' - Used to determine which files to track changes with git. 'git add .' will track all files in the repository, alternatively instead of using '.' you can specificy the name of the file you want to track.

Commit Changes (This saves the changes to the git log file.)
- 'git commit -m' - This command commits your changes and '-m' allows you to enter a short title for the changes that were made. A second '-m' after this can be used for a more detailed description of changes. 

Push Local Repository to GitHub (To do this you will first need to connect your local machine to the GitHub repository via SSH key)
- 'git push' - This command is used with additional details to specify where the repository is pushed to. 'git push origin master' is an example where 'origin' specifies the location of the git repository, and 'master' is the name of the branch that we are pushing to. 

To Create a Repository Locally 
 - 'git init' - This initializes the local directory as a git project. 
 
Push a Repository Created Locally to GitHub
- Once a locally created repository has been created, it has to be connected to a GitHub repository before it can be pushed.
- An empty repository must be created on GitHub. While viewing the Repository you wish to clone, click the green "Clone or Download" button and copy the SSH key.
- 'git remote add origin' - Use this command with the SSH key from the GitHub repository to specificy which GitHub repository to connect to.
- After this, normal 'git push' commands can be used to push changes to GitHub.

Branching 
- Branching creates a branch (or copy) of the master branch and allows you to make changes to the new branches without changing the master branch.
- Multiple branches can be created and worked on at once, and when ready, the branches can be merged back into the master branch. 
- 'git branch' - Use this command to view all branches of the current repository.
- 'git checkout -b' - This command, followed by your desired branch name, will create a new branch of your repository, and make the new branch the active branch you are in.
- 'git checkout' - This command, followed by the name of the branch you wish to be working in, will change the active branch you are in to the one specified. 
- 'git diff' - This command, followed by the name of the branch you wish to compare to, will show all differenecs between your active branch and the branch specified. 
- 'git merge' - This command , follwed by the name of the branch you wish to merge your changes with, will merge your changes with the repository. You must have full access to the repository you wish to merge with to use this command. A more common workflow is to use a pull request to ensure code is reviewed and approved before merging.

Forking
- This is making a copy of a repository that you don't have full access to.
- To do this, when you find a repository on GitHub you wish to work on, click the "fork" button, to create a copy of the repository in your GitHub account.

Pull Request (PR)
- This is a request to have your code pulled into another branch, typically the master branch.
- When a pull request is made, your code can be reviewed and commented on before merging onto the branch.
- To do this, once your local repository has been pushed to GitHub, click the "Pull Requests" tab and specificy which repository you want to merge your changes into. 
- You will have the chance to make your own comments to accompany the changes you are proposing.