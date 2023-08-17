# Working with Git in VS Code

In this section you will learn how to perform basic Git actions in VS Code. Courses on Git usually make use of the command line interface to do these actions, but this introduces a steep learning curve. Instead, using Git from VS Code is much more visual (i.e., more "clicky"), and therefore easier to use for those inexperienced with the command line. 

## What is Git?
Git is a version control system (VCS). In short, a VCS is a tool that helps you keep track of changes to you codebase (e.g., a Jupyter Book project!) over time. It allows you to keep track of the history of changes made to your code, work collaboratively with others, and revert to a previous version of the code if needed. 

## What is GitLab?
GitLab is platform that hosts Git repositories, which can also be accessed through a web interface. Essentially, GitLab hosts the main repository that the members of a project interact with. Additionally, GitLab has plenty of other useful features such as issue tracking and code review. A selection of these features that are particularly useful for us as Jupyter Book developers will be highlighted in a {ref}`later section <gitlab>.

## Terminology
This is a (non-exhaustive) list of terminology that will be used throughout this section:

- Repository: a collection of files and folders, along with a history of their changes and who made them. 
- Commit: a snapshot of the current state of the repository.
- Staging: preparation of files to be committed. During staging, we propose files to be committed.
- Branch: a development line.
- Local: on your own computer.
- Remote: on someone elses computer.
- Pushing: uploading new commits to the remote repository.
- Pulling: downloading new commits from the remote repository to your local repository.
- Tracked (files): files that Git knows about and keeps track of their history.
- Untracked (files): files that Git does not yet know about.