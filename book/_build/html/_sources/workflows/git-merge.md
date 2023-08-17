(git-merge)=
# Merging

We're finished with our chapter, and now it's time to include all of our commits in the `main` branch.

1. Make sure that you've committed all your new sections and changes, and that they're pushed to the remote repository.

2. Go the repository overview on GitLab. In the left menu bar, go to "Merge requests". On the Merge requests page, click "New merge request". 

3. You can now choose a source branch and a target branch. Since we want to merge our changes from `chapter-2` *into* `main`, `chapter-2` is the source branch and `main` is the target branch ({numref}`gitlab-merge-request`) . Once you've selected the correct branches, click "Compare branches and continue".

```{figure} ../images/gitlab-merge-request.png
:name: gitlab-merge-request

Creating a new merge request to merge `chapter-2` into `main`.
```

4. On the next page, you can give your merge request a name, and provide a description of your changes ({numref}`gitlab-merge-request-description`). If somebody has to review your changes, you can add them in the "Reviewer menu". They will then be notified via email that they need to review your work. Finally, watch out for the option "Delete source branch when merge request is accepted". If you want to keep working on the same branch, even after your previous work has been merged, make sure you untick the box! Once everything is filled in, click "Create merge request".

```{figure} ../images/gitlab-merge-request-description.png
:name: gitlab-merge-request-description

Example of a filled-in merge request.
```

5. On the page of our merge request ({numref}`gitlab-finished-merge-request`), we're greeted with some more information. On top, you can read the description we just provided when creating the merge request. We can also see an "Approve" button, which you may or may not see, depending on your repository rights. Next, we can see a green checkmark, with a "Merge" button. This is good news: our changes do not conflict with existing files on the `main` branch, and we can merge our changes directly by clicking the button (if applicable: only after somebody else approved the request). If this isn't the case, you'll see a red cross instead of the green checkmark, and GitLab will tell that you've run into a *merge conflict*. You'll need to figure out which file(s) are causing this, and fix it. You can read more on this in the {ref}`section on merge conflicts <merge-conflicts>`.


```{figure} ../images/gitlab-finished-merge-request.png
:name: gitlab-finished-merge-request

The finished merge request.
```