# Git


## Installation

First, we need to install Git itself. 

````{tab} Windows
1. Go to [this webpage](https://git-scm.com/download/win) and download the correct version of Git for your system.
2. Execute the installer and go through it. You can leave all options to the default values, **but make sure the option "Git from the command line and also from 3rd-party software" is selected**. Without this option, we won't be able to use Git from VS Code.
3. Once the installation is finished, check if everything works. Open the start menu, then type `git`. From the search results, open the application `Git Bash`. This will open a terminal window, in which you can execute commands. Type in the command `git`, and execute it by pressing enter. If Git is installed correctly, you should see some sort of help page. If it outputs an error, then something may went wrong with the installation (you may have selected a wrong option).
````
````{tab} MacOS
Open up a terminal window (*Command + Space*, type in `terminal`). Then, type the command `git`. If Git has been installed already, it will output some help. If Git has not been installed, you will get a pop-up that looks something like this:

```{figure} ../images/install-Xcode-CLT.png
```

Click on `install`. The installation may take a couple of minutes. Once it's finished, check if everything has been installed correctly by exectuting `git` again.
````

## Setting up SSH-keys

When we want to visit repositories on GitLab, we need to log in. The same holds if we want to interact with these repositories with Git from VS Code. This means that everytime we make a commit, pull, et cetera, we need to provide our password, which becomes very tedious. Alternatively, we can provide GitLab with an SSH-key of our sytem, so that GitLab knows it is indeed us that are making the changes to the repository, removing the need to provide a password. 

1. Open up a terminal window (Git Bash on Windows). Next, type (or copy and paste) the following command:

        ssh-keygen -t ed25519 -C "GitLab"

2. You will get output that looks something like this:
    
        Generating public/private ed25519 key pair.
        Enter file in which to save the key (/Users/<user>/.ssh/id_ed25519):

    Press enter to use the default path (the one between parenthesis). Keep note of this path, as we will need to visit it later on.

3. You will now be asked to enter a passphrase. You can give one, but you will be asked for it everytime you make a commit, so it's better to leave this field emtpy and use this key only for GitLab. After the command is done executing, it will generate two files: `id_ed25519` and `id_ed25519.pub`. The `.pub` file is the public part of the SSH-Key which we need.


4. Go to [GitLab](https://gitlab.tudelft.nl) and log in using your NetID. Click on your profile icon on the top-right of the page, then go to Preferences. In the menu on the left, go to SSH-Keys. You are now greeted with a screen that looks like this:

```{figure} ../images/gitlab-ssh-screen.png
```

5. Navigate to the `id_ed25519.pub` file that we generated in step 2. Open the file with a text editor (Notepad on Windows, textEdit on Mac). Copy its contents and paste it in the 'Key' field of SSH-Keys menu. Give the key a Title and click 'Add key'. 

    ```{note}
    On MacOS, the `.ssh/` folder is hidden by default, so you won't be able to find it in finder. To show hidden files and folders, press **Command + Shift + .**
    ```

6. Now test the connection. Go to the terminal (Git Bash on windows) and type:

        ssh -vT git@gitlab.tudelft.nl

    You should get a huge output, but somewhere at the end of that output it should say something like:

        Welcome to GitLab, <netid>!

## Updating the local Git environment

The final step is to provide a username and email address to Git, so our commits can be identified. To do this, in the terminal (Git Bash on Windows) type in the following command for the username:

    git config --global user.name "<first name> <last name>"

And type the following command to set the email address:

    git config --global user.email "<your TU Delft email>"