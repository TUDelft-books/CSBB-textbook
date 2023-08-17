(git-clone)=
# Cloning a repository

Before we can start working on our Jupyter Book, we of course need to have the repository on our own system. This is done by *cloning* the repository, and here's how you do it with VS Code:

1. On GitLab, go to the repository of your book. Click on the blue button that says "Clone" ({numref}`gitlab-clone`), and copy the link under "Clone with SSH".

```{figure} ../images/gitlab-clone.png
:name: gitlab-clone

The cloning menu.
```

2. Open a new VS Code window. You should be greeted with a welcome page ({numref}`vscode-welcome`). On this page, click "Clone Git Repository". Alternatively, open the Source Control menu from the left side bar, and click on "Clone Repository".

```{figure} ../images/vscode-welcome.png
:name: vscode-welcome

The VS Code welcome screen.
```

3. On the top of your screen, you should get a prompt asking you for a URL. In this field, paste the link you copied from GitLab and press enter. It will ask you to choose the location of the repository. After you've chosen a location, a final prompt will show up asking if you want to open the repository. Click on "Open".

4. You now have a local copy of the repository. Next, {ref}`make a new branch <git-branch>` for your work.