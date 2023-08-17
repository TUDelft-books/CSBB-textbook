(git-branch)=
# Branches

Branches are a very useful feature of Git. Branches allow you to work on multiple versions of your codebase simultaneously; you create a copy of your codebase, on which you can work independently of the main codebase. Some advantages of working with branches are:

- Isolation: when you work on your own branch, your changes are isolated from the main codebase. Unfinished or unreviewed parts of your book are "hidden". 
- Collaboration: branches make it easier for multiple project members to work on the same codebase simultaneously. If every member works on their own branch, they can make their changes without having to worry about interfering with another members' changes.

## How to make a branch

The act of making a new branch from an existing one is called *branching*. Usually, you want to branch from the `main` branch, but you can of course also choose to branch from another branch. The branch from which you create a new branch is called the *source* branch.

1. On GitLab, navigate to the repository of your project. Under the project description, you should see a menu button with a "+" in it (see {numref}`new-branch-button`). Click this button, then click on "New branch".

```{figure} ../images/gitlab-branch.png
:name: new-branch-button

Click the highlighted button to make a new branch.
```

2. A new page opens ({numref}`new-branch-menu`), on which you can specify the name of your branch and the source branch. Try to think of a good name for your branch. For example, `chapter-2` is a suitable name if we're going to be working on Chapter 2 of our book. After you've made sure that the selected source branch is correct, click "Create branch".

```{figure} ../images/gitlab-branch-name.png
:name: new-branch-menu

We're making a new branch called `chapter-2` from the `main` branch.
```

3. You should be sent back to an overview page of your repository. In the branch selection menu (see {numref}`new-branch-repo`), it should now say `chapter-2` instead of `main`. 

```{figure} ../images/gitlab-new-branch-repo.png
:name: new-branch-repo

The circled menu is the branch selection menu. 
```

4. The final step is to *check out* our new branch in VS Code. *Checking out* means that we're changing our working branch (i.e., the one to which we will be committing our changes) from one to the other. In VS Code, open the branch menu from the bottom left (see {numref}`git-branch-menu-main`). You'll be be greeted with a menu that looks like the one in {numref}`git-branch-selection-menu`. In this menu, we get an overview of the branches of our repository. Notice that our new branch `chapter-2` appears as `origin/chapter-2`, and has a cloud icon in front of it. This means that the branch only exists on the remote repository. Check out the branch by simply clicking on it. Check that the branch is indeed checked out by looking at the branch menu button in the bottom left again; it should now say the name of your branch instead of `main` (in our case `chapter-2`). 

```{figure} ../images/git-branch-menu-main.png
:name: git-branch-menu-main

Location of the branch menu.
```

```{figure} ../images/git-branch-selection-menu.png
:name: git-branch-selection-menu

The branch selection menu, where our new branch has shown up.
```

5. Now that we've created and checked out our new branch, we can start {ref}`making and committing changes <stage-commit-push>`.

## Predefined branches

If your repository is located in the [Interactive Textbooks CiTG](https://gitlab.tudelft.nl/interactivetextbooks-citg) group on GitLab, it is likely that it already has some predefined branches in addition to `main`, namely `publish` and `publish-html`. These branches serve the following purposes:

- `main`: this is the main development branch on which new changes are collected. If you're working on 
- `publish`: this is the version of the book that is visible to the public (i.e., the version that the students will see). Again, you cannot push directly to this branch. 
- `publish-html`: this branch contains the HTML of the version of the book that lives on the `publish` branch. When a new version of the book is merged in the `publish` branch, the new book is built using the `jupyter book build` command and the HTML is uploaded to `publish-html`. The webserver is constantly fetching this branch and pulling any incoming changes.