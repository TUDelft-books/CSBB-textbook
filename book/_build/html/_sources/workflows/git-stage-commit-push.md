(stage-commit-push)=
# Staging, committing and pushing

Suppose we are writing a new chapter, or are updating an existing chapter for our Jupyter Book. We've created a new branch on which we are going to make the changes, and we've checked out this branch (make sure this is really the case by checking the name of the current branch in the bottom-left corner of your VS Code window!).

## Staging
For demonstration purposes, we have created a new Markdown file called `new-chapter.md`, which we want to add to the book. Since this is a new file, Git has no knowledge about its existence yet. I.e., the file is *untracked*. To add new files to our repository, we need to *stage* and *commit* them. To do this, open the Source Control menu in the left side bar. Our new file should appear in this menu:

```{figure} ../images/git-new-file.png

The new file appears in the Source Control menu.
```

Notice that there is a green letter U placed besides the file, meaning that our file is untracked. To add a file to the *staging area*, click on the + that appears when you hover over the file. 

## Committing
Next, in the field that says "Message", write a short description of the changes you have made. This message is what is called the *Commit Message*. After we've done this, the menu should now look something like this:

```{figure} ../images/git-file-added.png

The new file has been staged, and we've written a Commit Message.
```

Now, we are ready to add the changes to the repository. This is done by *committing* the staged changes. To do this, simply press the big, blue "Commit" button in the Source Control menu. 

```{tip}
Unlike this example, you do not have to stage and commit every file individually. In a real case, a chapter may consist of multiple files (and images!), and it makes sense to add them in the same commit. 
```

## Pushing the changes
Are we done now? No! Up to now, we have only made changes and committed to the *local* copy of the repository. We still need to *push* our changes to the *remote* repository (the one that is on the TU Delft GitLab), so that others can see our changes and interact with them. In the bottom left corner, next to the branch name, click the "Synchronize Changes" button (the one that looks like this: 🔄, highlighted in the image below) to push the changes to GitLab.

```{figure} ../images/git-push.png

After committing, click the 🔄 button to push our changes to the remote repository.
```

## Summary
In short, the Git workflow consists of the following steps:

1. Staging new and modified files
2. Writing a commit message
3. Committing the changes
4. Pushing the new changes to GitLab