# VS Code

VS Code is a text editor with some extra features, such as integrated source control and a file browser. Moreover, extensions are available to add functionality to VS Code.

## Installation

VS Code can be downloaded from [here](https://code.visualstudio.com). The installation is fairly simple and won't be covered here.

## Extensions

When working with Jupyter Book (or Notebooks in general), these extensions are highly recommended:

- [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) - for obvious reasons. Also includes Jupyter Notebook rendering.
- [MyST-Markdown](https://marketplace.visualstudio.com/items?itemName=ExecutableBookProject.myst-highlight) - adds support for MyST markdown, including previews.
- [YAML](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml) - enables validation of `.yml` files (the format of the Jupyter Book configuration files).

## Getting Anaconda to work in the VS Code terminal
```{tab} Windows
On Windows, Anaconda usually does not work in the integrated VS Code terminal (Powershell). To check if it works for you, open a new terminal in VS Code by going clicking **View > Terminal** in the top menu bar. In the terminal window that appears, type `conda` and execute. If you get help page for `conda`, you're all set. If instead you get something like:

    conda : the term 'conda' is not recognized ...

then do the following steps:

1. Open Anaconda prompt **as administrator**.
2. Execute the following command:

        conda init --all

3. Close the Anaconda prompt. Then, open a Powershell window **as administrator** (go to the Start menu, type Powershell, then open Windows Powershell as administrator).
4. In the Powershell window, execute the following command: 
   
        Set-ExecutionPolicy -ExecutionPolicy RemoteSigned

5. The command will ask you for some permissions. To do so, type `A`, then press enter.
6. Restart VS Code, then test by executing `conda` again. This time, it should give you the help page. You now have access to you Anaconda environments in the VS Code terminal.
```
```{tab} MacOS
Usually, Anaconda works by default in the MacOS terminal. To check if it works for you, open a new terminal in VS Code by going clicking **View > Terminal** in the top menu bar. In the terminal window that appears, type `conda` and execute. If you get help page for `conda`, you're all set. If instead you get something like:

    zsh: command not found: conda

then do the following:

1. Find out where Anaconda is installed on your system. If you left everything as default during the installation, Anaconda is installed in `/Users/<username>/anaconda3` if you used the install script, or in `/Users/<username>/opt` if you used the graphical interface to install Anaconda.

2. Execute the following line:

        source <anaconda-installation-dir>/bin/activate

3. Then:

        conda init zsh

4. Restart VS Code, then test by executing `conda` again. This time, it should give you the help page. You now have access to you Anaconda environments in the VS Code terminal.
```